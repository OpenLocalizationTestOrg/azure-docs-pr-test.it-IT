---
title: aaaRaspberry Pi toocloud (Python) - connessione Pi Raspberry tooAzure IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi Pi Raspberry tooAzure IoT Hub per la piattaforma cloud di Azure Pi Raspberry toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot al lampone pi greco, al lampone pi iot hub, al lampone pi trasmissione dati toocloud, al lampone pi toocloud
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a><span data-ttu-id="6a276-104">Connettersi Pi Raspberry tooAzure IoT Hub (Python)</span><span class="sxs-lookup"><span data-stu-id="6a276-104">Connect Raspberry Pi tooAzure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="6a276-105">In questa esercitazione, è necessario innanzitutto apprendimento hello nozioni fondamentali sulle operazioni con Pi Raspberry Raspbian in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6a276-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="6a276-106">Si apprenderà quindi la modalità di connessione cloud toohello dispositivi utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="6a276-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="6a276-107">Per esempi di Windows 10 IoT Core, vedere toohello [Windows Dev Center](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="6a276-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="6a276-108">Se non si ha ancora un kit,</span><span class="sxs-lookup"><span data-stu-id="6a276-108">Don't have a kit yet?</span></span> <span data-ttu-id="6a276-109">Provare il [simulatore online Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6a276-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="6a276-110">In alternativa, acquistare un nuovo kit [qui](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="6a276-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6a276-111">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="6a276-111">What you do</span></span>

* <span data-ttu-id="6a276-112">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6a276-112">Create an IoT hub.</span></span>
* <span data-ttu-id="6a276-113">Registrare un dispositivo per Pi nel proprio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6a276-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="6a276-114">Installare Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="6a276-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="6a276-115">Eseguire un'applicazione di esempio nell'hub IoT di pi greco toosend sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="6a276-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="6a276-116">Connettersi Pi Raspberry tooan l'hub IoT creati.</span><span class="sxs-lookup"><span data-stu-id="6a276-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="6a276-117">Quindi eseguire un'applicazione di esempio in dati di temperatura e umidità toocollect Pi da un sensore BME280.</span><span class="sxs-lookup"><span data-stu-id="6a276-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="6a276-118">Infine, si invia l'hub IoT hello sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="6a276-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6a276-119">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6a276-119">What you learn</span></span>

* <span data-ttu-id="6a276-120">Come toocreate un hub IoT di Azure e ottenere la stringa di connessione nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6a276-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="6a276-121">Come tooconnect Pi con un sensore BME280.</span><span class="sxs-lookup"><span data-stu-id="6a276-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="6a276-122">Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su Pi.</span><span class="sxs-lookup"><span data-stu-id="6a276-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="6a276-123">Come l'hub IoT toosend sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="6a276-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6a276-124">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="6a276-124">What you need</span></span>

![Elementi necessari](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="6a276-126">Hello Raspberry Pi 2 o 3 Pi Raspberry Lavagna.</span><span class="sxs-lookup"><span data-stu-id="6a276-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="6a276-127">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="6a276-127">An active Azure subscription.</span></span> <span data-ttu-id="6a276-128">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6a276-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="6a276-129">Un monitoraggio, una tastiera e mouse che si connettono tooPi.</span><span class="sxs-lookup"><span data-stu-id="6a276-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="6a276-130">Un Mac o PC che esegue Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="6a276-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="6a276-131">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="6a276-131">An Internet connection.</span></span>
* <span data-ttu-id="6a276-132">Una scheda microSD da 16 GB o più.</span><span class="sxs-lookup"><span data-stu-id="6a276-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="6a276-133">Un USB SD adapter o microSD card tooburn hello immagine del sistema operativo nella scheda microSD hello.</span><span class="sxs-lookup"><span data-stu-id="6a276-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="6a276-134">Alimentatore di 2 amp 5 volt con il cavo USB micro di hello 6 piedi.</span><span class="sxs-lookup"><span data-stu-id="6a276-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="6a276-135">Hello seguenti elementi è facoltativo:</span><span class="sxs-lookup"><span data-stu-id="6a276-135">hello following items are optional:</span></span>

* <span data-ttu-id="6a276-136">Un sensore Adafruit BME280 assemblato per rilevare umidità, temperatura e pressione.</span><span class="sxs-lookup"><span data-stu-id="6a276-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="6a276-137">Una basetta sperimentale.</span><span class="sxs-lookup"><span data-stu-id="6a276-137">A breadboard.</span></span>
* <span data-ttu-id="6a276-138">6 cavi ponticello F/M.</span><span class="sxs-lookup"><span data-stu-id="6a276-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="6a276-139">Un LED da 10 mm a luce diffusa.</span><span class="sxs-lookup"><span data-stu-id="6a276-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="6a276-140">Poiché il supporto di esempio di codice hello simulati i dati del sensore, questi elementi sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="6a276-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="6a276-141">Installare Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="6a276-141">Set up Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="6a276-142">Installazione del sistema operativo di hello Raspbian per Pi</span><span class="sxs-lookup"><span data-stu-id="6a276-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="6a276-143">Preparare una scheda microSD hello per l'installazione dell'immagine Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="6a276-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="6a276-144">Scaricare Raspbian.</span><span class="sxs-lookup"><span data-stu-id="6a276-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="6a276-145">[Scaricare Raspbian Jessie con Desktop](https://www.raspberrypi.org/downloads/raspbian/) (file con estensione zip hello).</span><span class="sxs-lookup"><span data-stu-id="6a276-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="6a276-146">Estrarre la cartella di hello Raspbian immagine tooa nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6a276-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="6a276-147">Installare una scheda microSD di Raspbian toohello.</span><span class="sxs-lookup"><span data-stu-id="6a276-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="6a276-148">[Scaricare e installare hello Etcher SD card masterizzatore utilità](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="6a276-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="6a276-149">Eseguire Etcher e selezionare l'immagine Raspbian hello estratta nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="6a276-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="6a276-150">Selezionare un'unità scheda microSD hello.</span><span class="sxs-lookup"><span data-stu-id="6a276-150">Select hello microSD card drive.</span></span> <span data-ttu-id="6a276-151">Si noti che Etcher potrebbe essere stata già selezionata unità corretta hello.</span><span class="sxs-lookup"><span data-stu-id="6a276-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="6a276-152">Fare clic sulla scheda microSD toohello Raspbian di tooinstall Flash.</span><span class="sxs-lookup"><span data-stu-id="6a276-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="6a276-153">Rimuovi scheda microSD hello dal computer al termine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="6a276-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="6a276-154">Scheda microSD di hello tooremove provvisoria è direttamente perché Etcher Smonta scheda microSD hello dopo il completamento o rimuove automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6a276-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="6a276-155">Inserire scheda microSD hello Pi.</span><span class="sxs-lookup"><span data-stu-id="6a276-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="6a276-156">Abilitare SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="6a276-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="6a276-157">Collegare monitor toohello Pi, tastiera e mouse, avviare l'installazione guidata piattaforma e l'accesso Raspbian utilizzando `pi` come nome utente hello e `raspberry` come password hello.</span><span class="sxs-lookup"><span data-stu-id="6a276-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="6a276-158">Fare clic sull'icona al lampone hello > **preferenze** > **Raspberry Pi configurazione**.</span><span class="sxs-lookup"><span data-stu-id="6a276-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menu Preferenze Raspbian Hello](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="6a276-160">In hello **interfacce** scheda, impostare **I2C** e **SSH** troppo**abilitare**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a276-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="6a276-161">Se non hai sensori fisici e desidera toouse simulato sensore dati, questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="6a276-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Abilitare I2C e SSH su Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="6a276-163">tooenable SSH e I2C, è possibile trovare più documenti di riferimento su [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="6a276-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="6a276-164">Connettersi hello sensore tooPi</span><span class="sxs-lookup"><span data-stu-id="6a276-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="6a276-165">Utilizzare hello breadboard e ponticelli cavi tooconnect un LED e un tooPi BME280 come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6a276-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="6a276-166">Se non si dispone di sensore hello, [ignorare questa sezione](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="6a276-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hello Raspberry Pi e sensore connessione](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="6a276-168">sensore Hello BME280 possibile raccogliere dati di temperatura e umidità.</span><span class="sxs-lookup"><span data-stu-id="6a276-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="6a276-169">E hello LED lampeggia se esiste una comunicazione tra i dispositivi e hello cloud.</span><span class="sxs-lookup"><span data-stu-id="6a276-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="6a276-170">Per i codici PIN sensore, utilizzare hello seguente collegamento:</span><span class="sxs-lookup"><span data-stu-id="6a276-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="6a276-171">Inizio (sensore e LED)</span><span class="sxs-lookup"><span data-stu-id="6a276-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="6a276-172">Fine (scheda)</span><span class="sxs-lookup"><span data-stu-id="6a276-172">End (Board)</span></span>            | <span data-ttu-id="6a276-173">Colore del cavo</span><span class="sxs-lookup"><span data-stu-id="6a276-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="6a276-174">VDD (Pin 5G)</span><span class="sxs-lookup"><span data-stu-id="6a276-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="6a276-175">3,3 V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="6a276-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="6a276-176">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="6a276-176">White cable</span></span>   |
| <span data-ttu-id="6a276-177">GND (Pin 7G)</span><span class="sxs-lookup"><span data-stu-id="6a276-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="6a276-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="6a276-178">GND (Pin 6)</span></span>            | <span data-ttu-id="6a276-179">Cavo marrone</span><span class="sxs-lookup"><span data-stu-id="6a276-179">Brown cable</span></span>   |
| <span data-ttu-id="6a276-180">SDI (Pin 10G)</span><span class="sxs-lookup"><span data-stu-id="6a276-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="6a276-181">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="6a276-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="6a276-182">Cavo rosso</span><span class="sxs-lookup"><span data-stu-id="6a276-182">Red cable</span></span>     |
| <span data-ttu-id="6a276-183">SCK (Pin 8G)</span><span class="sxs-lookup"><span data-stu-id="6a276-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="6a276-184">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="6a276-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="6a276-185">Cavo arancione</span><span class="sxs-lookup"><span data-stu-id="6a276-185">Orange cable</span></span>  |
| <span data-ttu-id="6a276-186">LED VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="6a276-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="6a276-187">GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="6a276-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="6a276-188">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="6a276-188">White cable</span></span>   |
| <span data-ttu-id="6a276-189">LED GND (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="6a276-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="6a276-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="6a276-190">GND (Pin 20)</span></span>           | <span data-ttu-id="6a276-191">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="6a276-191">Black cable</span></span>   |

<span data-ttu-id="6a276-192">Fare clic su tooview [Raspberry Pi 2 e 3 mapping Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) per riferimento.</span><span class="sxs-lookup"><span data-stu-id="6a276-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="6a276-193">Dopo aver collegato correttamente BME280 tooyour Raspberry Pi, dovrebbe essere sotto l'immagine.</span><span class="sxs-lookup"><span data-stu-id="6a276-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi e BME280 connessi](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="6a276-195">Connessione di rete toohello Pi</span><span class="sxs-lookup"><span data-stu-id="6a276-195">Connect Pi toohello network</span></span>

<span data-ttu-id="6a276-196">Attivare Pi tramite cavo USB micro hello e alimentatore hello.</span><span class="sxs-lookup"><span data-stu-id="6a276-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="6a276-197">Utilizzare hello Ethernet via cavo tooconnect Pi tooyour cablate di rete o seguire hello [istruzioni hello Foundation Pi Raspberry](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour rete.</span><span class="sxs-lookup"><span data-stu-id="6a276-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="6a276-198">Dopo l'installazione guidata piattaforma toohello connessione rete, è necessario annotare hello tootake [indirizzo IP del pi greco](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="6a276-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Rete toowired connesso](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="6a276-200">Assicurarsi che l'installazione guidata piattaforma sia connesso toohello stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="6a276-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="6a276-201">Ad esempio, se il computer è connesso tooa rete wireless mentre Pi è connesso tooa rete cablata, si potrebbe visualizzare non hello IP indirizzo nell'output di hello devdisco.</span><span class="sxs-lookup"><span data-stu-id="6a276-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="6a276-202">Eseguire un'applicazione di esempio in Pi</span><span class="sxs-lookup"><span data-stu-id="6a276-202">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="6a276-203">Installare i pacchetti dei prerequisiti hello</span><span class="sxs-lookup"><span data-stu-id="6a276-203">Install hello prerequisite packages</span></span>

<span data-ttu-id="6a276-204">Utilizzare uno dei seguenti client SSH dagli tooyour di tooconnect computer host Pi Raspberry hello.</span><span class="sxs-lookup"><span data-stu-id="6a276-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="6a276-205">**Utenti Windows**</span><span class="sxs-lookup"><span data-stu-id="6a276-205">**Windows Users**</span></span>
   1. <span data-ttu-id="6a276-206">Scaricare e installare [PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="6a276-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="6a276-207">Copiare l'indirizzo IP hello della sezione Pi in nome Host di hello (o indirizzo IP) e selezionare il tipo di connessione hello SSH.</span><span class="sxs-lookup"><span data-stu-id="6a276-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   
   <span data-ttu-id="6a276-208">**Utenti Mac e Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="6a276-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="6a276-209">Utilizzare client SSH incorporato hello in Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="6a276-209">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="6a276-210">Potrebbe essere necessario toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="6a276-210">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="6a276-211">nome utente predefinito Hello `pi` , e la password di hello è `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="6a276-211">hello default username is `pi` , and hello password is `raspberry`.</span></span>


### <a name="configure-hello-sample-application"></a><span data-ttu-id="6a276-212">Configurare l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="6a276-212">Configure hello sample application</span></span>

1. <span data-ttu-id="6a276-213">Clonare l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6a276-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="6a276-214">Aprire il file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="6a276-214">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="6a276-215">Questo file contiene 5 macro configurabili.</span><span class="sxs-lookup"><span data-stu-id="6a276-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="6a276-216">Hello prima uno è `MESSAGE_TIMESPAN`, che definisce l'intervallo di tempo hello (in millisecondi) tra i due messaggi che inviano toocloud.</span><span class="sxs-lookup"><span data-stu-id="6a276-216">hello first one is `MESSAGE_TIMESPAN`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="6a276-217">Hello secondo `SIMULATED_DATA`, ovvero un valore booleano per se toouse sensore dati simulati o non.</span><span class="sxs-lookup"><span data-stu-id="6a276-217">hello second one `SIMULATED_DATA`, which is a Boolean value for whether toouse simulated sensor data or not.</span></span> <span data-ttu-id="6a276-218">`I2C_ADDRESS`è in indirizzo hello I2C che è connesso il sensore BME280.</span><span class="sxs-lookup"><span data-stu-id="6a276-218">`I2C_ADDRESS` is hello I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="6a276-219">`GPIO_PIN_ADDRESS`è l'indirizzo GPIO hello per il LED.</span><span class="sxs-lookup"><span data-stu-id="6a276-219">`GPIO_PIN_ADDRESS` is hello GPIO address for your LED.</span></span> <span data-ttu-id="6a276-220">Hello ultimo uno è `BLINK_TIMESPAN`, cui definito timespan hello quando il LED è attivata in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="6a276-220">hello last one is `BLINK_TIMESPAN`, which defined hello timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="6a276-221">Se si **non dispone di sensore hello**, hello impostare `SIMULATED_DATA` valore troppo`True` applicazione di esempio hello toomake creare e utilizzare dati del sensore simulato.</span><span class="sxs-lookup"><span data-stu-id="6a276-221">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`True` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="6a276-222">Salvare e uscire premendo CTRL-O > Invio > CTRL-X.</span><span class="sxs-lookup"><span data-stu-id="6a276-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="6a276-223">Compilare ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="6a276-223">Build and run hello sample application</span></span>

1. <span data-ttu-id="6a276-224">Compilare l'applicazione di esempio hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6a276-224">Build hello sample application by running hello following command.</span></span> <span data-ttu-id="6a276-225">Poiché hello Azure IoT SDK per Python sono wrapper su hello Azure IoT dispositivo C SDK, sarà necessario librerie hello C toocompile se è preferibile o necessario toogenerate hello Python di librerie da codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="6a276-225">Because hello Azure IoT SDKs for Python are wrappers on top of hello Azure IoT Device C SDK, you will need toocompile hello C libraries if you want or need toogenerate hello Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="6a276-226">È inoltre possibile specificare la versione di hello da eseguendo `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="6a276-226">You can also specify hello version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="6a276-227">Se si esegue uno script senza parametri, script hello rileverà automaticamente versione hello di python installato (sequenza di ricerca 2.7 -> 3.4 -> 3.5).</span><span class="sxs-lookup"><span data-stu-id="6a276-227">If you run script without parameter, hello script will automatically detect hello version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="6a276-228">Assicurarsi che la versione di Python rimanga coerente durante la compilazione e l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6a276-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="6a276-229">Sulla compilazione libreria client Python di hello (iothub_client.so) nei dispositivi Linux con meno di 1GB di RAM, può vedere compilare accumulano durante la compilazione iothub_client_python.cpp, come illustrato di seguito al 98% `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="6a276-229">On building hello Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="6a276-230">Se si esegue questo problema, controllare il consumo di memoria hello di hello dispositivo utilizzando `free -m command` in un'altra finestra terminal questo periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="6a276-230">If you run into this issue, check hello memory consumption of hello device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="6a276-231">Se si utilizza memoria insufficiente durante la compilazione di file iothub_client_python.cpp, potrebbe essere tootemporarily aumentare tooget spazio di swapping hello è più disponibile memoria toosuccessfully compilare libreria SDK del dispositivo hello del client Python.</span><span class="sxs-lookup"><span data-stu-id="6a276-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have tootemporarily increase hello swap space tooget more available memory toosuccessfully build hello Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="6a276-232">Eseguire l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6a276-232">Run hello sample application by running hello following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="6a276-233">Assicurarsi copiare e incollare stringa di connessione del dispositivo hello in virgolette hello.</span><span class="sxs-lookup"><span data-stu-id="6a276-233">Make sure you copy-paste hello device connection string into hello single quotes.</span></span> <span data-ttu-id="6a276-234">E, se si usa python hello 3, è possibile utilizzare hello comando `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="6a276-234">And if you use hello python 3, then you can use hello command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="6a276-235">Verrà visualizzato l'output seguente hello che mostra hello sensore dati e hello i messaggi vengono inviati tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a276-235">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

   ![Output - sensore dati vengono inviati da tooyour Raspberry Pi hub IoT](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="6a276-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a276-237">Next steps</span></span>

<span data-ttu-id="6a276-238">È stato eseguito dati sensore toocollect di applicazione di esempio e inviarlo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6a276-238">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="6a276-239">messaggi hello toosee che l'installazione guidata piattaforma Raspberry ha inviato IoT tooyour hub o trasmissione tooyour messaggi Pi Raspberry in un'interfaccia della riga di comando, vedere hello [dispositivo cloud Gestione messaggistica esercitazione hub IOT Esplora](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="6a276-239">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
