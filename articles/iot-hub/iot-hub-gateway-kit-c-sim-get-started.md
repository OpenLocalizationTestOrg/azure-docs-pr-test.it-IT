---
title: 'Dispositivo simulato e gateway Azure IoT: introduzione | Documentazione Microsoft'
description: Introduzione a IoT Gateway Starter Kit, creare l'hub IoT di Azure e collegare Gateway toohello IoT hub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot hub iot gateway, Guida introduttiva a hello internet delle cose, iot toolkit
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
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="59ec8-104">Introduzione allo starter kit per il gateway IoT con un dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="59ec8-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="59ec8-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="59ec8-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="59ec8-106">Dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="59ec8-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="59ec8-107">In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="59ec8-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="59ec8-108">Si userà Intel NUC che esegue Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="59ec8-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="59ec8-109">Si apprenderà come tooseamleesly connettersi cloud toohello di dispositivi con Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="59ec8-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="59ec8-110">**Non si dispone ancora di un kit?** Fare clic [qui](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="59ec8-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="59ec8-111">Lezione 1: Configurare NUC</span><span class="sxs-lookup"><span data-stu-id="59ec8-111">Lesson 1: Configure your NUC</span></span>
![Diagramma di flusso della lezione 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="59ec8-113">In questa lezione, è possibile impostare NUC Intel (successivo unità di elaborazione) in hello Kit come gateway IoT di Azure, installare il pacchetto di Azure IoT Edge hello in NUC ed eseguire una funzionalità di gateway hello tooverify app di esempio.</span><span class="sxs-lookup"><span data-stu-id="59ec8-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="59ec8-114">*Toocomplete tempo stimato: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="59ec8-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="59ec8-115">Andare troppo[impostare NUC Intel come gateway IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="59ec8-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="59ec8-116">Lezione 2. Creare l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="59ec8-116">Lesson 2: Create your IoT Hub</span></span>
![Diagramma di flusso della lezione 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="59ec8-118">In questa lezione, si installa strumenti hello e software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="59ec8-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="59ec8-119">Quindi creare l'account gratuito di Azure, eseguire il provisioning dell'hub IoT di Azure e creare il primo dispositivo nell'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="59ec8-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="59ec8-120">Prima di iniziare questa lezione, completare la lezione 1.</span><span class="sxs-lookup"><span data-stu-id="59ec8-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="59ec8-121">Ottenere strumenti hello</span><span class="sxs-lookup"><span data-stu-id="59ec8-121">Get hello tools</span></span>
<span data-ttu-id="59ec8-122">Installare strumenti di hello e software nel computer host.</span><span class="sxs-lookup"><span data-stu-id="59ec8-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="59ec8-123">*Toocomplete tempo stimato: 20 minuti*</span><span class="sxs-lookup"><span data-stu-id="59ec8-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="59ec8-124">Andare troppo[strumenti hello](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="59ec8-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="59ec8-125">Creare un hub IoT ed effettuare la registrazione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="59ec8-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="59ec8-126">Creare il gruppo di risorse, l'hub IoT Azure prima di eseguire il provisioning e aggiungere primo dispositivo toohello IoT hub utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="59ec8-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="59ec8-127">*Toocomplete tempo stimato: 10 minuti*</span><span class="sxs-lookup"><span data-stu-id="59ec8-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="59ec8-128">Andare troppo[creare un hub IoT e registrare il dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="59ec8-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="59ec8-129">Lezione 3: Ricevere messaggi da dispositivo simulato hello e leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="59ec8-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="59ec8-130">In questa lezione si utilizzerà script tooautomate hello configurazione ed esecuzione di un'app dispositivo simulato nel gateway.</span><span class="sxs-lookup"><span data-stu-id="59ec8-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="59ec8-131">Genera dati di esempio temperatura app dispositivo simulato Hello e lo invia tooan modulo di hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59ec8-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="59ec8-132">Hello pacchetti ricevuti dati hello e lo invia hub IoT tooyour tramite il framework di gateway hello fornito in Azure IoT Edge di IoT hub modulo.</span><span class="sxs-lookup"><span data-stu-id="59ec8-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagramma di flusso della lezione 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="59ec8-134">Configurare ed eseguire un dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="59ec8-134">Configure and run a simulated device</span></span>
<span data-ttu-id="59ec8-135">Preparare i codici di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="59ec8-135">Prepare hello sample codes.</span></span> <span data-ttu-id="59ec8-136">Quindi Configura ed Esegui applicazione di esempio dispositivo simulato hello.</span><span class="sxs-lookup"><span data-stu-id="59ec8-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="59ec8-137">*Toocomplete tempo stimato: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="59ec8-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="59ec8-138">Andare troppo[configurare ed eseguire un dispositivo simulato](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="59ec8-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="59ec8-139">Leggere messaggi dall'hub IoT</span><span class="sxs-lookup"><span data-stu-id="59ec8-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="59ec8-140">Eseguire un codice di esempio nei messaggi di hello tooread computer host dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="59ec8-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="59ec8-141">*Toocomplete tempo stimato: 15 minuti*</span><span class="sxs-lookup"><span data-stu-id="59ec8-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="59ec8-142">Andare troppo[leggere messaggi dall'hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="59ec8-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="59ec8-143">Lezione 4: Salvare i messaggi di archiviazione tabelle tooAzure</span><span class="sxs-lookup"><span data-stu-id="59ec8-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="59ec8-144">Creare un'app di Azure di funzione che ottiene i messaggi in arrivo dall'hub IoT e li scrive archiviazione tabella tooAzure.</span><span class="sxs-lookup"><span data-stu-id="59ec8-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagramma di flusso della lezione 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="59ec8-146">Creare un'app per le funzioni di Azure e un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="59ec8-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="59ec8-147">Un'app di Azure (funzione) e un account di archiviazione di Azure, utilizzare un toocreate modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="59ec8-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="59ec8-148">*Toocomplete tempo stimato: 10 minuti*</span><span class="sxs-lookup"><span data-stu-id="59ec8-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="59ec8-149">Andare troppo[creare un account di archiviazione di Azure e l'app di Azure (funzione)](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="59ec8-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="59ec8-150">Leggere i messaggi persistenti nell'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="59ec8-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="59ec8-151">Monitorare i messaggi hello gateway-to-cloud quando vengono scritti nel servizio di archiviazione tabelle tooAzure.</span><span class="sxs-lookup"><span data-stu-id="59ec8-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="59ec8-152">*Toocomplete tempo stimato: 5 minuti*</span><span class="sxs-lookup"><span data-stu-id="59ec8-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="59ec8-153">Andare troppo[leggere messaggi persistenti nell'archiviazione tabelle Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="59ec8-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="59ec8-154">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="59ec8-154">Troubleshooting</span></span>
<span data-ttu-id="59ec8-155">Se si verificano problemi durante lezioni hello, cercare soluzioni in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="59ec8-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="59ec8-156">Scopri di più</span><span class="sxs-lookup"><span data-stu-id="59ec8-156">Explore more</span></span>
<span data-ttu-id="59ec8-157">Visitare hello [zona di Intel IoT Gateway Kit per sviluppatori](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="59ec8-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
