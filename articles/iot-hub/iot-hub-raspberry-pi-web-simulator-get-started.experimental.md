---
title: aaaSimulated Raspberry Pi toocloud (Node.js) - connessione Raspberry l'installazione guidata piattaforma web simulatore tooAzure IoT Hub | Documenti Microsoft
description: Connettersi Raspberry Pi web simulatore tooAzure IoT Hub per Pi Raspberry toosend dati toohello cloud di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: pi al lampone simulatore, azure al lampone pi greco, al lampone pi iot hub iot, pi al lampone invia dati toocloud, al lampone pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="4046a-104">Connettersi Pi Raspberry simulatore online tooAzure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="4046a-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="4046a-105">In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con simulatore online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4046a-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="4046a-106">Si apprenderà quindi la modalità di connessione cloud toohello di hello Pi simulatore utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="4046a-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="4046a-107">Se si dispone di dispositivi fisici, visitare [tooAzure connettersi Pi Raspberry IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget avviato.</span><span class="sxs-lookup"><span data-stu-id="4046a-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="4046a-108">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="4046a-108">What you do</span></span>

* <span data-ttu-id="4046a-109">Nozioni di base hello del simulatore online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4046a-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="4046a-110">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4046a-110">Create an IoT hub.</span></span>
* <span data-ttu-id="4046a-111">Registrare un dispositivo per Pi nel proprio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4046a-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="4046a-112">Eseguire un'applicazione di esempio Pi toosend simulato sensore dati tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4046a-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="4046a-113">Connettere hub IoT tooan simulato Pi Raspberry creati.</span><span class="sxs-lookup"><span data-stu-id="4046a-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="4046a-114">Quindi si esegue un'applicazione di esempio con i dati del sensore toogenerate hello simulatore.</span><span class="sxs-lookup"><span data-stu-id="4046a-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="4046a-115">Infine, si invia l'hub IoT hello sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="4046a-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="4046a-116">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="4046a-116">What you learn</span></span>

* <span data-ttu-id="4046a-117">Come toocreate un hub IoT di Azure e ottenere la stringa di connessione nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4046a-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="4046a-118">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4046a-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="4046a-119">Come toowork con simulatore online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4046a-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="4046a-120">Come l'hub IoT toosend sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="4046a-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="4046a-121">Panoramica del simulatore Web Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="4046a-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="4046a-122">Fare clic su simulatore online Pi Raspberry hello pulsante toolaunch.</span><span class="sxs-lookup"><span data-stu-id="4046a-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="4046a-123">Avviare il simulatore Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="4046a-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="4046a-124">Esistono tre aree nel simulatore di hello web.</span><span class="sxs-lookup"><span data-stu-id="4046a-124">There are three areas in hello web simulator.</span></span>
* <span data-ttu-id="4046a-125">Area di assembly: circuito predefinito hello è che un Pi si connette con un sensore BME280 e un LED.</span><span class="sxs-lookup"><span data-stu-id="4046a-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="4046a-126">area Hello è bloccata nella versione di anteprima così attualmente non è possibile eseguire la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="4046a-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="4046a-127">Per la codifica - un editor di codice in linea per toocode con Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4046a-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="4046a-128">applicazione di esempio Hello predefinita consente di dati del sensore toocollect dal sensore BME280 e invia tooyour IoT Hub di Azure.</span><span class="sxs-lookup"><span data-stu-id="4046a-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="4046a-129">un'applicazione Hello è completamente compatibile con dispositivi Pi.</span><span class="sxs-lookup"><span data-stu-id="4046a-129">hello application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="4046a-130">Finestra di console integrata - Mostra output di hello del codice.</span><span class="sxs-lookup"><span data-stu-id="4046a-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="4046a-131">Nella parte superiore di hello di questa finestra, sono disponibili tre pulsanti.</span><span class="sxs-lookup"><span data-stu-id="4046a-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="4046a-132">**Eseguire** -esecuzione di un'applicazione hello in hello per la codifica.</span><span class="sxs-lookup"><span data-stu-id="4046a-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="4046a-133">**Reimpostare** -hello la reimpostazione della codifica di applicazione di esempio di area toohello predefinito.</span><span class="sxs-lookup"><span data-stu-id="4046a-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="4046a-134">**Riduzione o espansione** - in hello destra lato vi è un pulsante per si toofold/espandere hello finestra della console.</span><span class="sxs-lookup"><span data-stu-id="4046a-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="4046a-135">simulatore di web Pi Raspberry Hello è ora disponibile nella versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="4046a-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="4046a-136">Desideriamo toohear il tono di voce hello [Gitter chat](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="4046a-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="4046a-137">codice sorgente Hello è public su [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="4046a-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Panoramica del simulatore online Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="4046a-139">Eseguire un'applicazione di esempio nel simulatore Web Pi</span><span class="sxs-lookup"><span data-stu-id="4046a-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="4046a-140">Nell'area di codifica, assicurarsi che si lavora sull'applicazione di esempio hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="4046a-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="4046a-141">Sostituire i segnaposto hello nella riga 15 con hello stringa di connessione di Azure IoT hub dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4046a-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="4046a-142">![Sostituire una stringa di connessione del dispositivo hello](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="4046a-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="4046a-143">Fare clic su **eseguire** o tipo `npm start` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="4046a-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="4046a-144">Verrà visualizzato l'output di hello seguente che mostra i dati del sensore hello e i messaggi hello inviati hub IoT tooyour ![Output - i dati del sensore inviati dall'hub IoT di pi greco Raspberry tooyour](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="4046a-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="4046a-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4046a-145">Next steps</span></span>

<span data-ttu-id="4046a-146">È stato eseguito dati sensore toocollect di applicazione di esempio e inviarlo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4046a-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
