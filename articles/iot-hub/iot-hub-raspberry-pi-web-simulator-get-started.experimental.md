---
title: Raspberry Pi simulato al cloud (Node.js) - Connettere il simulatore Web Raspberry Pi all'hub IoT di Azure | Microsoft Docs
description: Connettere il simulatore Web Raspberry Pi all'hub IoT di Azure per permettere a Raspberry Pi di inviare dati al cloud di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: simulatore raspberry pi, azure iot raspberry pi, raspberry pi hub iot, raspberry pi invia dati al cloud, raspberry pi al cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 5b7e209b65ccf6edb32d211797663e5e5b170df8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="6e58a-104">Connettore il simulatore online Raspberry Pi all'hub IoT di Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="6e58a-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="6e58a-105">Questa esercitazione illustra le nozioni di base relative all'uso del simulatore online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6e58a-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="6e58a-106">In seguito illustra come connettere in modo trasparente il simulatore al cloud usando l'[hub IoT di Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="6e58a-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="6e58a-107">Se si dispone di dispositivi fisici, per iniziare visitare [Connettere Raspberry Pi all'hub IoT di Azure](iot-hub-raspberry-pi-kit-node-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e58a-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="6e58a-108">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="6e58a-108">What you do</span></span>

* <span data-ttu-id="6e58a-109">Apprendere le nozioni base del simulatore online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6e58a-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="6e58a-110">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6e58a-110">Create an IoT hub.</span></span>
* <span data-ttu-id="6e58a-111">Registrare un dispositivo per Pi nel proprio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6e58a-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="6e58a-112">Eseguire un'applicazione di esempio in Pi per inviare i dati del sensore simulato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6e58a-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="6e58a-113">Connettere il connettore Raspberry Pi simulato a un hub IoT creato.</span><span class="sxs-lookup"><span data-stu-id="6e58a-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="6e58a-114">Eseguire un'applicazione di esempio con il simulatore per generare i dati del sensore.</span><span class="sxs-lookup"><span data-stu-id="6e58a-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="6e58a-115">Infine inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6e58a-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6e58a-116">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6e58a-116">What you learn</span></span>

* <span data-ttu-id="6e58a-117">Come creare un hub IoT di Azure e ottenere la stringa di connessione del nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6e58a-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="6e58a-118">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6e58a-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="6e58a-119">Come utilizzare il simulatore online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6e58a-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="6e58a-120">Come inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6e58a-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="6e58a-121">Panoramica del simulatore Web Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="6e58a-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="6e58a-122">Fare clic sul pulsante per avviare il simulatore online Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6e58a-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="6e58a-123">Avviare il simulatore Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="6e58a-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="6e58a-124">Esistono tre aree nel simulatore Web.</span><span class="sxs-lookup"><span data-stu-id="6e58a-124">There are three areas in the web simulator.</span></span>
* <span data-ttu-id="6e58a-125">Area dell'assembly: nel circuito predefinito un Pi si connette a un sensore BME280 e a un LED.</span><span class="sxs-lookup"><span data-stu-id="6e58a-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="6e58a-126">L'area è bloccata nella versione di anteprima, pertanto non è attualmente possibile eseguire la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="6e58a-126">The area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="6e58a-127">Area della codifica: un editor di codice online da usare con Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6e58a-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="6e58a-128">L'applicazione di esempio predefinita consente di raccogliere i dati del sensore BME280 e di inviarli all'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="6e58a-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="6e58a-129">L'applicazione è completamente compatibile con dispositivi Pi effettivi.</span><span class="sxs-lookup"><span data-stu-id="6e58a-129">The application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="6e58a-130">Finestra della console integrata: mostra l'output del codice.</span><span class="sxs-lookup"><span data-stu-id="6e58a-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="6e58a-131">Nella parte superiore di questa finestra sono disponibili tre pulsanti.</span><span class="sxs-lookup"><span data-stu-id="6e58a-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="6e58a-132">**Esegui**: eseguire l'applicazione nell'area di codifica.</span><span class="sxs-lookup"><span data-stu-id="6e58a-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="6e58a-133">**Reimposta**: reimposta l'area di codifica sull'applicazione di esempio predefinita.</span><span class="sxs-lookup"><span data-stu-id="6e58a-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="6e58a-134">**Comprimi/Espandi**: sul lato destro è disponibile un pulsante per comprimere/espandere la finestra della console.</span><span class="sxs-lookup"><span data-stu-id="6e58a-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="6e58a-135">Il simulatore Web Raspberry Pi è ora disponibile nella versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="6e58a-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="6e58a-136">Vorremmo sentire la tua voce nella [chat Gitter](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="6e58a-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="6e58a-137">Il codice sorgente è pubblico in [GitHub](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="6e58a-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Panoramica del simulatore online Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="6e58a-139">Eseguire un'applicazione di esempio nel simulatore Web Pi</span><span class="sxs-lookup"><span data-stu-id="6e58a-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="6e58a-140">Nell'area di codifica assicurarsi di lavorare nell'applicazione di esempio predefinita.</span><span class="sxs-lookup"><span data-stu-id="6e58a-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="6e58a-141">Sostituire il segnaposto nella riga 15 con la stringa di connessione del dispositivo hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="6e58a-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="6e58a-142">![Sostituire la stringa di connessione del dispositivo](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="6e58a-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="6e58a-143">Fare clic su **Esegui** o digita `npm start` per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6e58a-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="6e58a-144">Dovrebbe venire visualizzato l'output seguente che mostra i dati del sensore e i messaggi inviati all'hub IoT ![Output: dati del sensore inviati da Raspberry Pi all'hub IoT](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="6e58a-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="6e58a-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6e58a-145">Next steps</span></span>

<span data-ttu-id="6e58a-146">È stata eseguita un'applicazione di esempio per raccogliere i dati del sensore da inviare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6e58a-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
