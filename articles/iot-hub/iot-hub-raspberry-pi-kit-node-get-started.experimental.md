---
title: Raspberry Pi al cloud (Node. js) - Connettere Raspberry Pi ad Azure IoT Hub | Microsoft Docs
description: Connettere Raspberry Pi ad Azure IoT Hub per permettere a Raspberry Pi di inviare dati al cloud di Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: azure iot raspberry pi, raspberry pi iot hub, raspberry pi invio dati al cloud, da raspberry pi al cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="5d558-104">Connettere Raspberry Pi ad Azure IoT Hub (Node. js)</span><span class="sxs-lookup"><span data-stu-id="5d558-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="5d558-105">Questa esercitazione illustra le nozioni di base sull'uso di Raspberry Pi con il sistema operativo Raspbian.</span><span class="sxs-lookup"><span data-stu-id="5d558-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="5d558-106">Viene poi illustrato come connettere i dispositivi al cloud usando l'[hub IoT di Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5d558-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="5d558-107">Per esempi di Windows 10 IoT Core, vedere [Windows Dev Center](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="5d558-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="5d558-108">Se non si ha ancora un kit,</span><span class="sxs-lookup"><span data-stu-id="5d558-108">Don't have a kit yet?</span></span> <span data-ttu-id="5d558-109">provare l'[emulatore Raspberry Pi 3](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="5d558-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="5d558-110">In alternativa, acquistare un nuovo kit [qui](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="5d558-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="5d558-111">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="5d558-111">What you do</span></span>

* <span data-ttu-id="5d558-112">Installare Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="5d558-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="5d558-113">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d558-113">Create an IoT hub.</span></span>
* <span data-ttu-id="5d558-114">Registrare un dispositivo per Pi nel proprio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d558-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="5d558-115">Eseguire un'applicazione di esempio in Pi per inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d558-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="5d558-116">Connettere Raspberry Pi a un hub IoT creato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="5d558-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="5d558-117">Dopodiché, eseguire un'applicazione di esempio in Pi per raccogliere i dati di temperatura e umidità da un sensore BME280.</span><span class="sxs-lookup"><span data-stu-id="5d558-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="5d558-118">Infine inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d558-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="5d558-119">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5d558-119">What you learn</span></span>

* <span data-ttu-id="5d558-120">Come creare un hub IoT di Azure e ottenere la stringa di connessione del nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5d558-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="5d558-121">Come connettere Pi con un sensore BME280.</span><span class="sxs-lookup"><span data-stu-id="5d558-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="5d558-122">Come raccogliere i dati del sensore eseguendo un'applicazione di esempio in Pi.</span><span class="sxs-lookup"><span data-stu-id="5d558-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="5d558-123">Come inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d558-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5d558-124">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="5d558-124">What you need</span></span>

![Elementi necessari](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="5d558-126">La scheda di Raspberry Pi 2 o di Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="5d558-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="5d558-127">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="5d558-127">An active Azure subscription.</span></span> <span data-ttu-id="5d558-128">Se non si ha un account di Azure, [creare un account di Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="5d558-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="5d558-129">Un monitor, una tastiera USB e un mouse da collegare a Pi.</span><span class="sxs-lookup"><span data-stu-id="5d558-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="5d558-130">Un Mac o PC che esegue Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="5d558-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="5d558-131">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="5d558-131">An Internet connection.</span></span>
* <span data-ttu-id="5d558-132">Una scheda microSD da 16 GB o più.</span><span class="sxs-lookup"><span data-stu-id="5d558-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="5d558-133">Una scheda microSD o un adattatore USB-SD con cui masterizzare l'immagine del sistema operativo nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="5d558-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="5d558-134">Un alimentatore da 5 V/2 A con cavo micro USB da 1,8 metri circa.</span><span class="sxs-lookup"><span data-stu-id="5d558-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="5d558-135">Gli elementi seguenti sono opzionali:</span><span class="sxs-lookup"><span data-stu-id="5d558-135">The following items are optional:</span></span>

* <span data-ttu-id="5d558-136">Un sensore Adafruit BME280 assemblato per rilevare umidità, temperatura e pressione.</span><span class="sxs-lookup"><span data-stu-id="5d558-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="5d558-137">Una basetta sperimentale.</span><span class="sxs-lookup"><span data-stu-id="5d558-137">A breadboard.</span></span>
* <span data-ttu-id="5d558-138">6 cavi ponticello F/M.</span><span class="sxs-lookup"><span data-stu-id="5d558-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="5d558-139">Un LED da 10 mm a luce diffusa.</span><span class="sxs-lookup"><span data-stu-id="5d558-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="5d558-140">Questi elementi sono opzionali, poiché l'esempio di codice supporta i dati del sensore simulati.</span><span class="sxs-lookup"><span data-stu-id="5d558-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="5d558-141">Installare Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="5d558-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="5d558-142">Installare il sistema operativo Raspbian per Pi</span><span class="sxs-lookup"><span data-stu-id="5d558-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="5d558-143">Preparare la scheda microSD per l'installazione dell'immagine di Raspbian.</span><span class="sxs-lookup"><span data-stu-id="5d558-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="5d558-144">Scaricare Raspbian.</span><span class="sxs-lookup"><span data-stu-id="5d558-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="5d558-145">[Scaricare Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (file .zip).</span><span class="sxs-lookup"><span data-stu-id="5d558-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="5d558-146">Estrarre l'immagine di Raspbian in una cartella nel computer.</span><span class="sxs-lookup"><span data-stu-id="5d558-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="5d558-147">Installare Raspbian nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="5d558-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="5d558-148">[Scaricare e installare l'utilità di masterizzazione Etcher per schede SD](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="5d558-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="5d558-149">Eseguire Etcher e selezionare l'immagine di Raspbian estratta nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="5d558-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="5d558-150">Selezionare l'unità della scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="5d558-150">Select the microSD card drive.</span></span> <span data-ttu-id="5d558-151">Si noti che Etcher potrebbe avere già selezionato l'unità corretta.</span><span class="sxs-lookup"><span data-stu-id="5d558-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="5d558-152">Fare clic su Flash per installare Raspbian nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="5d558-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="5d558-153">Rimuovere la scheda microSD dal computer al termine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="5d558-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="5d558-154">È possibile rimuovere direttamente la scheda microSD perché viene espulsa o smontata automaticamente da Etcher al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="5d558-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="5d558-155">Inserire la scheda microSD in Pi.</span><span class="sxs-lookup"><span data-stu-id="5d558-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="5d558-156">Abilitare SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="5d558-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="5d558-157">Collegare Pi al monitor, alla tastiera e al mouse, avviare Pi e accedere a Raspbian usando `pi` come nome utente e `raspberry` come password.</span><span class="sxs-lookup"><span data-stu-id="5d558-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="5d558-158">Fare clic sull'icona di Raspberry > **Preferenze** > **Raspberry Pi Configuration** (Configurazione di Raspberry Pi).</span><span class="sxs-lookup"><span data-stu-id="5d558-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Il menu Preferenze di Raspbian](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="5d558-160">Nella scheda **Interfacce** impostare **I2C** e **SSH** su **Abilita**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d558-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="5d558-161">Se non si hanno sensori fisici e si vogliono usare i dati di sensori simulati, questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="5d558-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Abilitare I2C e SSH su Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="5d558-163">Per abilitare SSH e I2C è possibile trovare più documenti di riferimento su [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="5d558-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="5d558-164">Connettere il sensore a Pi</span><span class="sxs-lookup"><span data-stu-id="5d558-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="5d558-165">Usare i cavi ponticello e la basetta sperimentale per connettere un LED e un sensore BME280 a Pi, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="5d558-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="5d558-166">Se non si dispone di sensori, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="5d558-166">If you don’t have the sensor, skip this section.</span></span>

![La connessione di Raspberry Pi e del sensore](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="5d558-168">Il sensore BME280 può raccogliere i dati relativi a temperatura e umidità.</span><span class="sxs-lookup"><span data-stu-id="5d558-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="5d558-169">Il LED sarà intermittente se viene stabilita una comunicazione tra il dispositivo e il cloud.</span><span class="sxs-lookup"><span data-stu-id="5d558-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="5d558-170">Per i pin dei sensori usare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d558-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="5d558-171">Inizio (sensore e LED)</span><span class="sxs-lookup"><span data-stu-id="5d558-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="5d558-172">Fine (scheda)</span><span class="sxs-lookup"><span data-stu-id="5d558-172">End (Board)</span></span>            | <span data-ttu-id="5d558-173">Colore del cavo</span><span class="sxs-lookup"><span data-stu-id="5d558-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="5d558-174">VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="5d558-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="5d558-175">3,3 V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="5d558-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="5d558-176">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="5d558-176">White cable</span></span>   |
| <span data-ttu-id="5d558-177">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="5d558-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="5d558-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="5d558-178">GND (Pin 6)</span></span>            | <span data-ttu-id="5d558-179">Cavo marrone</span><span class="sxs-lookup"><span data-stu-id="5d558-179">Brown cable</span></span>   |
| <span data-ttu-id="5d558-180">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="5d558-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="5d558-181">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="5d558-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="5d558-182">Cavo arancione</span><span class="sxs-lookup"><span data-stu-id="5d558-182">Orange cable</span></span>  |
| <span data-ttu-id="5d558-183">SDI (Pin 10G)</span><span class="sxs-lookup"><span data-stu-id="5d558-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="5d558-184">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="5d558-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="5d558-185">Cavo rosso</span><span class="sxs-lookup"><span data-stu-id="5d558-185">Red cable</span></span>     |
| <span data-ttu-id="5d558-186">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="5d558-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="5d558-187">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="5d558-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="5d558-188">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="5d558-188">White cable</span></span>   |
| <span data-ttu-id="5d558-189">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="5d558-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="5d558-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="5d558-190">GND (Pin 20)</span></span>           | <span data-ttu-id="5d558-191">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="5d558-191">Black cable</span></span>   |

<span data-ttu-id="5d558-192">Fare clic per visualizzare i [mapping Pin di Raspberry Pi 2 e 3](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) come riferimento.</span><span class="sxs-lookup"><span data-stu-id="5d558-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="5d558-193">Dopo aver correttamente collegato BME280 a Raspberry Pi, dovrebbe apparire come mostrato nell'immagine di seguito.</span><span class="sxs-lookup"><span data-stu-id="5d558-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi e BME280 connessi](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="5d558-195">Connettere Pi alla rete</span><span class="sxs-lookup"><span data-stu-id="5d558-195">Connect Pi to the network</span></span>

<span data-ttu-id="5d558-196">Accendere Pi usando il cavo micro USB e l'alimentatore.</span><span class="sxs-lookup"><span data-stu-id="5d558-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="5d558-197">Usare il cavo Ethernet per connettere Pi alla rete cablata oppure seguire le [istruzioni riportate nella Guida di Raspberry Pi](https://www.raspberrypi.org/learning/software-guide/wifi/) per connettere Pi alla rete wireless.</span><span class="sxs-lookup"><span data-stu-id="5d558-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="5d558-198">Dopo aver connesso Pi alla rete, è necessario annotarne [l'indirizzo IP](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="5d558-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Connesso alla rete cablata](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="5d558-200">Verificare che Pi sia connesso alla stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="5d558-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="5d558-201">Se il computer è connesso a una rete wireless mentre il dispositivo Pi è connesso a una rete cablata, ad esempio, l'indirizzo IP potrebbe non essere incluso nell'output di devdisco.</span><span class="sxs-lookup"><span data-stu-id="5d558-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="5d558-202">Eseguire un'applicazione di esempio in Pi</span><span class="sxs-lookup"><span data-stu-id="5d558-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="5d558-203">Clonare l'applicazione di esempio e installare i pacchetti di prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5d558-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="5d558-204">Per connettersi a Raspberry Pi, usare uno dei client SSH seguenti dal computer host.</span><span class="sxs-lookup"><span data-stu-id="5d558-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="5d558-205">[PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="5d558-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="5d558-206">Per connettersi con SSH, è necessario l'indirizzo IP di Pi.</span><span class="sxs-lookup"><span data-stu-id="5d558-206">You need the IP address of your Pi to connect it via SSH.</span></span>
    - <span data-ttu-id="5d558-207">Il client SSH incorporato in Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="5d558-207">The built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="5d558-208">Potrebbe essere necessario eseguire `ssh pi@<ip address of pi>` per connettere Pi tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="5d558-208">You might need run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="5d558-209">Il nome utente predefinito è `pi` e la password è `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="5d558-209">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="5d558-210">Installare Node.js e NPM in Pi.</span><span class="sxs-lookup"><span data-stu-id="5d558-210">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="5d558-211">Prima di tutto, è necessario controllare la versione di Node.js eseguendo il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5d558-211">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="5d558-212">Se la versione è precedente a 4.x o non è presente alcuna versione di Node.js in Pi, eseguire il comando seguente per installare o aggiornare Node.js.</span><span class="sxs-lookup"><span data-stu-id="5d558-212">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="5d558-213">Clonare l'applicazione di esempio tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5d558-213">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="5d558-214">Installare tutti i pacchetti con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5d558-214">Install all packages by the following command.</span></span> <span data-ttu-id="5d558-215">Include Azure IoT SDK per dispositivi, la libreria del sensore BME280 e libreria di Pi per i collegamenti.</span><span class="sxs-lookup"><span data-stu-id="5d558-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="5d558-216">A seconda della connessione di rete disponibile potrebbero occorrere alcuni minuti per portare a termine l'installazione.</span><span class="sxs-lookup"><span data-stu-id="5d558-216">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="5d558-217">Configurare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="5d558-217">Configure the sample application</span></span>

1. <span data-ttu-id="5d558-218">Aprire il file di configurazione eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d558-218">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![File di configurazione](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="5d558-220">Questo file contiene due elementi configurabili.</span><span class="sxs-lookup"><span data-stu-id="5d558-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="5d558-221">Il primo è `interval`, che definisce l'intervallo di tempo tra due messaggi inviati al cloud.</span><span class="sxs-lookup"><span data-stu-id="5d558-221">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="5d558-222">La seconda è `simulatedData`, ossia un valore booleano che indica se usare o no i dati del sensore simulato.</span><span class="sxs-lookup"><span data-stu-id="5d558-222">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="5d558-223">Se **non si dispone del sensore**, impostare il valore `simulatedData` su `true` per permettere all'applicazione di esempio di creare e usare i dati del sensore simulati.</span><span class="sxs-lookup"><span data-stu-id="5d558-223">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="5d558-224">Salvare e uscire premendo CTRL-O > Invio > CTRL-X.</span><span class="sxs-lookup"><span data-stu-id="5d558-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="5d558-225">Eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="5d558-225">Run the sample application</span></span>

1. <span data-ttu-id="5d558-226">Eseguire l'applicazione di esempio tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5d558-226">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="5d558-227">Assicurarsi di copiare e incollare la stringa di connessione del dispositivo tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="5d558-227">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="5d558-228">Dovrebbe essere visibile l'output seguente che mostra i dati del sensore e i messaggi inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d558-228">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - dati del sensore inviati da Raspberry Pi all'hub IoT](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="5d558-230">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d558-230">Next steps</span></span>

<span data-ttu-id="5d558-231">È stata eseguita un'applicazione di esempio per raccogliere i dati del sensore da inviare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5d558-231">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]