---
title: 'Raspberry Pi al cloud (C): connettere Raspberry Pi ad Azure IoT Hub | Microsoft Docs'
description: "Informazioni su come configurare e connettere Raspberry Pi all'hub IoT di Azure perché Raspberry Pi invii i dati alla piattaforma cloud di Azure in questa esercitazione."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: azure iot raspberry pi, raspberry pi iot hub, raspberry pi invio dati al cloud, da raspberry pi al cloud
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b8fda17a8d1d1796d5299e3aba4b0fd5e719a4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-c"></a><span data-ttu-id="25921-104">Connettere Raspberry Pi ad Azure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="25921-104">Connect Raspberry Pi to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="25921-105">Questa esercitazione illustra le nozioni di base sull'uso di Raspberry Pi con il sistema operativo Raspbian.</span><span class="sxs-lookup"><span data-stu-id="25921-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="25921-106">Viene poi illustrato come connettere i dispositivi al cloud usando l'[hub IoT di Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="25921-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="25921-107">Per esempi di Windows 10 IoT Core, vedere [Windows Dev Center](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="25921-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="25921-108">Se non si ha ancora un kit,</span><span class="sxs-lookup"><span data-stu-id="25921-108">Don't have a kit yet?</span></span> <span data-ttu-id="25921-109">Provare il [simulatore online Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="25921-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="25921-110">In alternativa, acquistare un nuovo kit [qui](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="25921-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="25921-111">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="25921-111">What you do</span></span>

* <span data-ttu-id="25921-112">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25921-112">Create an IoT hub.</span></span>
* <span data-ttu-id="25921-113">Registrare un dispositivo per Pi nel proprio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25921-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="25921-114">Installare Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="25921-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="25921-115">Eseguire un'applicazione di esempio in Pi per inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25921-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="25921-116">Connettere Raspberry Pi a un hub IoT creato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="25921-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="25921-117">Dopodiché, eseguire un'applicazione di esempio in Pi per raccogliere i dati di temperatura e umidità da un sensore BME280.</span><span class="sxs-lookup"><span data-stu-id="25921-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="25921-118">Infine inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25921-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="25921-119">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="25921-119">What you learn</span></span>

* <span data-ttu-id="25921-120">Come creare un hub IoT di Azure e ottenere la stringa di connessione del nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="25921-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="25921-121">Come connettere Pi con un sensore BME280.</span><span class="sxs-lookup"><span data-stu-id="25921-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="25921-122">Come raccogliere i dati del sensore eseguendo un'applicazione di esempio in Pi.</span><span class="sxs-lookup"><span data-stu-id="25921-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="25921-123">Come inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25921-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="25921-124">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="25921-124">What you need</span></span>

![Elementi necessari](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="25921-126">La scheda di Raspberry Pi 2 o di Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="25921-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="25921-127">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="25921-127">An active Azure subscription.</span></span> <span data-ttu-id="25921-128">Se non si ha un account di Azure, [creare un account di Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="25921-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="25921-129">Un monitor, una tastiera USB e un mouse da collegare a Pi.</span><span class="sxs-lookup"><span data-stu-id="25921-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="25921-130">Un Mac o PC che esegue Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="25921-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="25921-131">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="25921-131">An Internet connection.</span></span>
* <span data-ttu-id="25921-132">Una scheda microSD da 16 GB o più.</span><span class="sxs-lookup"><span data-stu-id="25921-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="25921-133">Una scheda microSD o un adattatore USB-SD con cui masterizzare l'immagine del sistema operativo nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="25921-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="25921-134">Un alimentatore da 5 V/2 A con cavo micro USB da 1,8 metri circa.</span><span class="sxs-lookup"><span data-stu-id="25921-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="25921-135">Gli elementi seguenti sono opzionali:</span><span class="sxs-lookup"><span data-stu-id="25921-135">The following items are optional:</span></span>

* <span data-ttu-id="25921-136">Un sensore Adafruit BME280 assemblato per rilevare umidità, temperatura e pressione.</span><span class="sxs-lookup"><span data-stu-id="25921-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="25921-137">Una basetta sperimentale.</span><span class="sxs-lookup"><span data-stu-id="25921-137">A breadboard.</span></span>
* <span data-ttu-id="25921-138">6 cavi ponticello F/M.</span><span class="sxs-lookup"><span data-stu-id="25921-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="25921-139">Un LED da 10 mm a luce diffusa.</span><span class="sxs-lookup"><span data-stu-id="25921-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="25921-140">Questi elementi sono opzionali, poiché l'esempio di codice supporta i dati del sensore simulati.</span><span class="sxs-lookup"><span data-stu-id="25921-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="25921-141">Installare Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="25921-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="25921-142">Installare il sistema operativo Raspbian per Pi</span><span class="sxs-lookup"><span data-stu-id="25921-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="25921-143">Preparare la scheda microSD per l'installazione dell'immagine di Raspbian.</span><span class="sxs-lookup"><span data-stu-id="25921-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="25921-144">Scaricare Raspbian.</span><span class="sxs-lookup"><span data-stu-id="25921-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="25921-145">[Scaricare Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (file ZIP).</span><span class="sxs-lookup"><span data-stu-id="25921-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="25921-146">Estrarre l'immagine di Raspbian in una cartella nel computer.</span><span class="sxs-lookup"><span data-stu-id="25921-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="25921-147">Installare Raspbian nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="25921-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="25921-148">[Scaricare e installare l'utilità di masterizzazione Etcher per schede SD](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="25921-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="25921-149">Eseguire Etcher e selezionare l'immagine di Raspbian estratta nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="25921-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="25921-150">Selezionare l'unità della scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="25921-150">Select the microSD card drive.</span></span> <span data-ttu-id="25921-151">Si noti che Etcher potrebbe avere già selezionato l'unità corretta.</span><span class="sxs-lookup"><span data-stu-id="25921-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="25921-152">Fare clic su Flash per installare Raspbian nella scheda microSD.</span><span class="sxs-lookup"><span data-stu-id="25921-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="25921-153">Rimuovere la scheda microSD dal computer al termine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="25921-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="25921-154">È possibile rimuovere direttamente la scheda microSD perché viene espulsa o smontata automaticamente da Etcher al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="25921-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="25921-155">Inserire la scheda microSD in Pi.</span><span class="sxs-lookup"><span data-stu-id="25921-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="25921-156">Abilitare SSH e SPI</span><span class="sxs-lookup"><span data-stu-id="25921-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="25921-157">Collegare Pi al monitor, alla tastiera e al mouse, avviare Pi e accedere a Raspbian usando `pi` come nome utente e `raspberry` come password.</span><span class="sxs-lookup"><span data-stu-id="25921-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="25921-158">Fare clic sull'icona di Raspberry > **Preferenze** > **Raspberry Pi Configuration** (Configurazione di Raspberry Pi).</span><span class="sxs-lookup"><span data-stu-id="25921-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Il menu Preferenze di Raspbian](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="25921-160">Nella scheda **Interfacce** impostare **SPI** e **SSH** su **Abilita**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="25921-160">On the **Interfaces** tab, set **SPI** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="25921-161">Se non si hanno sensori fisici e si vogliono usare i dati di sensori simulati, questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="25921-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Abilitare SPI e SSH su Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="25921-163">Per abilitare SSH e SPI è possibile trovare più documenti di riferimento su [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="25921-163">To enable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="25921-164">Connettere il sensore a Pi</span><span class="sxs-lookup"><span data-stu-id="25921-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="25921-165">Usare i cavi ponticello e la basetta sperimentale per connettere un LED e un sensore BME280 a Pi, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="25921-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="25921-166">In assenza di un sensore, [ignorare questa sezione](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="25921-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![La connessione di Raspberry Pi e del sensore](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="25921-168">Il sensore BME280 può raccogliere i dati relativi a temperatura e umidità.</span><span class="sxs-lookup"><span data-stu-id="25921-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="25921-169">Il LED sarà intermittente se viene stabilita una comunicazione tra il dispositivo e il cloud.</span><span class="sxs-lookup"><span data-stu-id="25921-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="25921-170">Per i pin dei sensori usare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="25921-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="25921-171">Inizio (sensore e LED)</span><span class="sxs-lookup"><span data-stu-id="25921-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="25921-172">Fine (scheda)</span><span class="sxs-lookup"><span data-stu-id="25921-172">End (Board)</span></span>            | <span data-ttu-id="25921-173">Colore del cavo</span><span class="sxs-lookup"><span data-stu-id="25921-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="25921-174">LED VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="25921-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="25921-175">GPIO 4 (Pin 7)</span><span class="sxs-lookup"><span data-stu-id="25921-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="25921-176">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="25921-176">White cable</span></span>   |
| <span data-ttu-id="25921-177">LED GND (Pin 6G)</span><span class="sxs-lookup"><span data-stu-id="25921-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="25921-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="25921-178">GND (Pin 6)</span></span>            | <span data-ttu-id="25921-179">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="25921-179">Black cable</span></span>   |
| <span data-ttu-id="25921-180">VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="25921-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="25921-181">3,3 V PWR (Pin 17)</span><span class="sxs-lookup"><span data-stu-id="25921-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="25921-182">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="25921-182">White cable</span></span>   |
| <span data-ttu-id="25921-183">GND (Pin 20F)</span><span class="sxs-lookup"><span data-stu-id="25921-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="25921-184">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="25921-184">GND (Pin 20)</span></span>           | <span data-ttu-id="25921-185">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="25921-185">Black cable</span></span>   |
| <span data-ttu-id="25921-186">SCK (Pin 21F)</span><span class="sxs-lookup"><span data-stu-id="25921-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="25921-187">SPI0 SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="25921-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="25921-188">Cavo arancione</span><span class="sxs-lookup"><span data-stu-id="25921-188">Orange cable</span></span>  |
| <span data-ttu-id="25921-189">SDO (Pin 22F)</span><span class="sxs-lookup"><span data-stu-id="25921-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="25921-190">SPI0 MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="25921-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="25921-191">Cavo giallo</span><span class="sxs-lookup"><span data-stu-id="25921-191">Yellow cable</span></span>  |
| <span data-ttu-id="25921-192">SDI (Pin 23F)</span><span class="sxs-lookup"><span data-stu-id="25921-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="25921-193">SPI0 MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="25921-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="25921-194">Cavo verde</span><span class="sxs-lookup"><span data-stu-id="25921-194">Green cable</span></span>   |
| <span data-ttu-id="25921-195">CS (Pin 24F)</span><span class="sxs-lookup"><span data-stu-id="25921-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="25921-196">SPI0 CS (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="25921-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="25921-197">Cavo blu</span><span class="sxs-lookup"><span data-stu-id="25921-197">Blue cable</span></span>    |

<span data-ttu-id="25921-198">Fare clic per visualizzare i [mapping Pin di Raspberry Pi 2 e 3](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) come riferimento.</span><span class="sxs-lookup"><span data-stu-id="25921-198">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="25921-199">Dopo aver correttamente collegato BME280 a Raspberry Pi, dovrebbe apparire come mostrato nell'immagine di seguito.</span><span class="sxs-lookup"><span data-stu-id="25921-199">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi e BME280 connessi](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="25921-201">Connettere Pi alla rete</span><span class="sxs-lookup"><span data-stu-id="25921-201">Connect Pi to the network</span></span>

<span data-ttu-id="25921-202">Accendere Pi usando il cavo micro USB e l'alimentatore.</span><span class="sxs-lookup"><span data-stu-id="25921-202">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="25921-203">Usare il cavo Ethernet per connettere Pi alla rete cablata oppure seguire le [istruzioni riportate nella Guida di Raspberry Pi](https://www.raspberrypi.org/learning/software-guide/wifi/) per connettere Pi alla rete wireless.</span><span class="sxs-lookup"><span data-stu-id="25921-203">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="25921-204">Dopo aver connesso Pi alla rete, è necessario annotarne [l'indirizzo IP](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="25921-204">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Connesso alla rete cablata](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="25921-206">Eseguire un'applicazione di esempio in Pi</span><span class="sxs-lookup"><span data-stu-id="25921-206">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="25921-207">Installare i pacchetti prerequisiti</span><span class="sxs-lookup"><span data-stu-id="25921-207">Install the prerequisite packages</span></span>

1. <span data-ttu-id="25921-208">Per connettersi a Raspberry Pi, usare uno dei client SSH seguenti dal computer host.</span><span class="sxs-lookup"><span data-stu-id="25921-208">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="25921-209">**Utenti Windows**</span><span class="sxs-lookup"><span data-stu-id="25921-209">**Windows Users**</span></span>
   1. <span data-ttu-id="25921-210">Scaricare e installare [PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="25921-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="25921-211">Copiare l'indirizzo IP di Pi nella sezione relativa a nome host o indirizzo IP e selezionare SSH come tipo di connessione.</span><span class="sxs-lookup"><span data-stu-id="25921-211">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="25921-213">**Utenti Mac e Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="25921-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="25921-214">Usare il client SSH predefinito in Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="25921-214">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="25921-215">Per connettere Pi tramite SSH potrebbe essere necessario eseguire `ssh pi@<ip address of pi>`.</span><span class="sxs-lookup"><span data-stu-id="25921-215">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="25921-216">Il nome utente predefinito è `pi` e la password è `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="25921-216">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="25921-217">Installare i pacchetti di prerequisiti per Azure IoT SDK per dispositivi di Microsoft Azure per C e Cmake eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="25921-217">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C and Cmake by running the following commands:</span></span>

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-the-sample-application"></a><span data-ttu-id="25921-218">Configurare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="25921-218">Configure the sample application</span></span>

1. <span data-ttu-id="25921-219">Clonare l'applicazione di esempio eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="25921-219">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="25921-220">Aprire il file di configurazione eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="25921-220">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![File di configurazione](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="25921-222">Questo file contiene due macro configurabili.</span><span class="sxs-lookup"><span data-stu-id="25921-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="25921-223">La prima è `INTERVAL`, che definisce l'intervallo di tempo (in millisecondi) tra due messaggi inviati al cloud.</span><span class="sxs-lookup"><span data-stu-id="25921-223">The first one is `INTERVAL`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="25921-224">La seconda è `SIMULATED_DATA`, ossia un valore booleano che indica se usare o no i dati del sensore simulato.</span><span class="sxs-lookup"><span data-stu-id="25921-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="25921-225">Se **non si dispone del sensore**, impostare il valore `SIMULATED_DATA` su `1` per permettere all'applicazione di esempio di creare e usare i dati del sensore simulati.</span><span class="sxs-lookup"><span data-stu-id="25921-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="25921-226">Salvare e uscire premendo CTRL-O > Invio > CTRL-X.</span><span class="sxs-lookup"><span data-stu-id="25921-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="25921-227">Compilare ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="25921-227">Build and run the sample application</span></span>

1. <span data-ttu-id="25921-228">Compilare l'applicazione di esempio eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="25921-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Output della compilazione](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="25921-230">Eseguire l'applicazione di esempio tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="25921-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="25921-231">Assicurarsi di copiare e incollare la stringa di connessione del dispositivo tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="25921-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="25921-232">Dovrebbe essere visibile l'output seguente che mostra i dati del sensore e i messaggi inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25921-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - dati del sensore inviati da Raspberry Pi all'hub IoT](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="25921-234">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25921-234">Next steps</span></span>

<span data-ttu-id="25921-235">È stata eseguita un'applicazione di esempio per raccogliere i dati del sensore da inviare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="25921-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="25921-236">Per visualizzare i messaggi inviati da Raspberry Pi all'hub IoT o per inviare messaggi a Raspberry Pi in un'interfaccia della riga di comando, vedere l'[esercitazione sulla gestione della messaggistica tra cloud e dispositivo con iothub-explorer](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="25921-236">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
