---
title: 'M0 toocloud: la connessione Wi-Fi M0 sfumatura tooAzure IoT Hub | Documenti Microsoft'
description: Informazioni su come tooset backup e la connessione Wi-Fi M0 di sfumatura Adafruit tooAzure la piattaforma cloud di Azure IoT Hub toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="5acc2-103">La connessione Wi-Fi M0 di sfumatura Adafruit tooAzure IoT Hub nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="5acc2-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connessione tra BME280, Feather M0 Wi-Fi e l'hub IoT](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="5acc2-105">In questa esercitazione, è necessario innanzitutto hello nozioni fondamentali sulle operazioni con la scheda Arduino di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="5acc2-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="5acc2-106">Si apprenderà quindi la modalità di connessione cloud toohello dispositivi utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5acc2-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="5acc2-107">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="5acc2-107">What you do</span></span>

<span data-ttu-id="5acc2-108">La connessione Wi-Fi M0 di sfumatura Adafruit tooan IoT hub creato.</span><span class="sxs-lookup"><span data-stu-id="5acc2-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="5acc2-109">Quindi eseguire un'applicazione di esempio in Wi-Fi M0 toocollect hello temperatura e umidità dati da un BME280.</span><span class="sxs-lookup"><span data-stu-id="5acc2-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="5acc2-110">Infine, si invia l'hub IoT hello sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="5acc2-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="5acc2-111">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5acc2-111">What you learn</span></span>

* <span data-ttu-id="5acc2-112">Come toocreate un hub IoT e registrare un dispositivo per Wi-Fi M0 sfumatura</span><span class="sxs-lookup"><span data-stu-id="5acc2-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="5acc2-113">Come tooconnect Wi-Fi M0 sfumatura con sensore hello e il computer</span><span class="sxs-lookup"><span data-stu-id="5acc2-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="5acc2-114">Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su Wi-Fi M0 sfumatura</span><span class="sxs-lookup"><span data-stu-id="5acc2-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="5acc2-115">Come toosend hello hub IoT tooyour di sensore dati</span><span class="sxs-lookup"><span data-stu-id="5acc2-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5acc2-116">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="5acc2-116">What you need</span></span>

![Parti necessarie per l'esercitazione hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="5acc2-118">toocomplete questa operazione, è necessario hello dallo Starter Kit di sfumatura M0 Wi-Fi le seguenti parti:</span><span class="sxs-lookup"><span data-stu-id="5acc2-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="5acc2-119">Hello Wi-Fi M0 sfumatura Lavagna</span><span class="sxs-lookup"><span data-stu-id="5acc2-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="5acc2-120">Un cavo USB A di tooType Micro USB</span><span class="sxs-lookup"><span data-stu-id="5acc2-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="5acc2-121">È inoltre necessario hello seguenti operazioni per l'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="5acc2-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="5acc2-122">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="5acc2-122">An active Azure subscription.</span></span> <span data-ttu-id="5acc2-123">Se non si ha un account di Azure, [creare un account di Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="5acc2-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="5acc2-124">Un Mac o un PC che esegue Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5acc2-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="5acc2-125">Una rete wireless per Wi-Fi M0 sfumatura tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="5acc2-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="5acc2-126">Uno strumento di configurazione hello Internet connessione toodownload.</span><span class="sxs-lookup"><span data-stu-id="5acc2-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="5acc2-127">[IDE Arduino](https://www.arduino.cc/en/main/software) 1.6.8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="5acc2-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="5acc2-128">Le versioni precedenti non funzionano con libreria di Azure IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="5acc2-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="5acc2-129">Se non si dispone di un sensore, hello seguenti elementi è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="5acc2-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="5acc2-130">È anche possibile hello utilizzando i dati del sensore simulato:</span><span class="sxs-lookup"><span data-stu-id="5acc2-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="5acc2-131">Un sensore di temperatura e umidità BME280</span><span class="sxs-lookup"><span data-stu-id="5acc2-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="5acc2-132">Basetta sperimentale</span><span class="sxs-lookup"><span data-stu-id="5acc2-132">A breadboard</span></span>
* <span data-ttu-id="5acc2-133">Cavi ponticello M/M</span><span class="sxs-lookup"><span data-stu-id="5acc2-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="5acc2-134">La connessione Wi-Fi M0 sfumatura con sensore hello e il computer</span><span class="sxs-lookup"><span data-stu-id="5acc2-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="5acc2-135">In questa sezione è connettersi Lavagna tooyour sensori di hello.</span><span class="sxs-lookup"><span data-stu-id="5acc2-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="5acc2-136">Quindi si collega il computer tooyour dispositivo per l'ulteriore utilizzo.</span><span class="sxs-lookup"><span data-stu-id="5acc2-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="5acc2-137">Connettersi a un DHT22 temperatura e umidità sensore tooFeather Wi-Fi M0</span><span class="sxs-lookup"><span data-stu-id="5acc2-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="5acc2-138">Utilizzare hello breadboard e ponticelli cavi toomake hello connessione.</span><span class="sxs-lookup"><span data-stu-id="5acc2-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="5acc2-139">Se non si dispone di un sensore, ignorare questa sezione in quanto è possibile usare i dati di sensori simulati.</span><span class="sxs-lookup"><span data-stu-id="5acc2-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Riferimento per le connessioni](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="5acc2-141">Per i codici PIN sensore, utilizzare hello seguente collegamento:</span><span class="sxs-lookup"><span data-stu-id="5acc2-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="5acc2-142">Inizio (sensore)</span><span class="sxs-lookup"><span data-stu-id="5acc2-142">Start (sensor)</span></span>           | <span data-ttu-id="5acc2-143">Fine (scheda)</span><span class="sxs-lookup"><span data-stu-id="5acc2-143">End (board)</span></span>            | <span data-ttu-id="5acc2-144">Colore del cavo</span><span class="sxs-lookup"><span data-stu-id="5acc2-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="5acc2-145">VDD (Pin 27A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="5acc2-146">3 V (Pin 3A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="5acc2-147">Cavo rosso</span><span class="sxs-lookup"><span data-stu-id="5acc2-147">Red cable</span></span>     |
| <span data-ttu-id="5acc2-148">GND (Pin 29A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="5acc2-149">GND (Pin 6A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="5acc2-150">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="5acc2-150">Black cable</span></span>   |
| <span data-ttu-id="5acc2-151">SCK (Pin 30A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="5acc2-152">SCK (Pin 12A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="5acc2-153">Cavo giallo</span><span class="sxs-lookup"><span data-stu-id="5acc2-153">Yellow cable</span></span>  |
| <span data-ttu-id="5acc2-154">SDO (Pin 31A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="5acc2-155">MI (Pin 14A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="5acc2-156">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="5acc2-156">White cable</span></span>   |
| <span data-ttu-id="5acc2-157">SDI (Pin 32A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="5acc2-158">M0 (Pin 13A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="5acc2-159">Cavo blu</span><span class="sxs-lookup"><span data-stu-id="5acc2-159">Blue cable</span></span>    |
| <span data-ttu-id="5acc2-160">CS (Pin 33A)</span><span class="sxs-lookup"><span data-stu-id="5acc2-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="5acc2-161">GPIO 5 (Pin 15J)</span><span class="sxs-lookup"><span data-stu-id="5acc2-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="5acc2-162">Cavo arancione</span><span class="sxs-lookup"><span data-stu-id="5acc2-162">Orange cable</span></span>  |

<span data-ttu-id="5acc2-163">Per altre informazioni, vedere [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Informazioni sul sensore di temperatura + pressione barometrica + umidità Adafruit BME280) e la [piedinatura di Adafruit Feather M0 Wi-Fi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="5acc2-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="5acc2-164">Ora Feather M0 Wi-Fi è connesso con un sensore funzionante.</span><span class="sxs-lookup"><span data-stu-id="5acc2-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Connettere DHT22 a Feather HUZZAH](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="5acc2-166">La connessione Wi-Fi M0 sfumatura tooyour computer</span><span class="sxs-lookup"><span data-stu-id="5acc2-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="5acc2-167">Utilizzare hello USB Micro tooType A USB cable tooconnect Wi-Fi M0 sfumatura tooyour computer, come illustrato:</span><span class="sxs-lookup"><span data-stu-id="5acc2-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![Connettere computer tooyour Huzzah sfumatura](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="5acc2-169">Aggiungere le autorizzazioni per la porta seriale (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5acc2-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="5acc2-170">Se si utilizza Ubuntu, verificare di che aver toooperate autorizzazioni hello in hello USB porta della sfumatura M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="5acc2-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="5acc2-171">le autorizzazioni della porta seriale tooadd, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="5acc2-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="5acc2-172">Un terminale, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5acc2-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="5acc2-173">Viene visualizzato uno dei hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="5acc2-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="5acc2-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="5acc2-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="5acc2-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="5acc2-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="5acc2-176">Nell'output di hello, si noti che `uucp` o `dialout` è nome del proprietario del gruppo hello di hello porta USB.</span><span class="sxs-lookup"><span data-stu-id="5acc2-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="5acc2-177">tooadd hello toohello gruppo di utenti, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5acc2-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="5acc2-178">Ottenuto nel passaggio precedente hello, nome del proprietario del gruppo hello `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="5acc2-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="5acc2-179">`<username>` il nome utente di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5acc2-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="5acc2-180">Per tooappear modifica hello, disconnettersi da Ubuntu e quindi accedere di nuovo.</span><span class="sxs-lookup"><span data-stu-id="5acc2-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="5acc2-181">Raccogliere dati del sensore e inviarle tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="5acc2-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="5acc2-182">In questa sezione si distribuisce e si esegue un'applicazione di esempio in Feather M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="5acc2-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="5acc2-183">applicazione di esempio Hello rende hello blink LED sul Wi-Fi M0 sfumatura.</span><span class="sxs-lookup"><span data-stu-id="5acc2-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="5acc2-184">Invia quindi temperatura hello e umidità raccolti da hello BME280 sensore tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5acc2-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="5acc2-185">Ottenere l'applicazione di esempio hello da GitHub e preparare hello Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="5acc2-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="5acc2-186">applicazione di esempio Hello è ospitata in GitHub.</span><span class="sxs-lookup"><span data-stu-id="5acc2-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="5acc2-187">Clonare il repository di esempio hello che contiene l'applicazione di esempio hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="5acc2-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="5acc2-188">repository di esempio hello tooclone, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="5acc2-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="5acc2-189">Aprire un prompt dei comandi o una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="5acc2-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="5acc2-190">Passare tooa cartella in cui si desidera toobe applicazione di esempio hello archiviati.</span><span class="sxs-lookup"><span data-stu-id="5acc2-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="5acc2-191">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5acc2-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="5acc2-192">Installare il pacchetto di hello per Wi-Fi M0 sfumatura in hello Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="5acc2-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="5acc2-193">Aprire hello cartella dove si trova l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="5acc2-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="5acc2-194">Aprire il file di app.ino hello nella cartella dell'applicazione hello in hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="5acc2-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Aprire l'applicazione di esempio hello in Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="5acc2-196">Fare clic su **File** > **preferenze** (Windows/Linux) o **Arduino** > **preferenze** (Mac) e copiare e Incolla collegamento hello sotto in hello **URL di gestione aggiuntivi lavagne** opzione hello preferenze Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="5acc2-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="5acc2-197">Fare clic su **strumenti** > **Lavagna** > **Manager lavagne**e quindi installare hello `Arduino SAMD Boards` versione `1.6.2` o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="5acc2-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="5acc2-198">Quindi nella stessa finestra hello, installare `Adafruit SAMD Boards` definizioni del file tooadd hello Lavagna del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5acc2-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![installazione del pacchetto esp8266 Hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="5acc2-200">Fare clic su **Strumenti** > **Schede** > **Adafruit M0 Wi-Fi**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="5acc2-201">Installare i driver (solo per Windows).</span><span class="sxs-lookup"><span data-stu-id="5acc2-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="5acc2-202">Quando si collega Wi-Fi M0 sfumatura, potrebbe essere necessario tooinstall un driver.</span><span class="sxs-lookup"><span data-stu-id="5acc2-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="5acc2-203">Fare clic su [hello collegamento per il download nella pagina Web hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) programma di installazione driver toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="5acc2-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="5acc2-204">Seguire i driver hello tooinstall passaggi hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="5acc2-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="5acc2-205">Installare le librerie necessarie</span><span class="sxs-lookup"><span data-stu-id="5acc2-205">Install necessary libraries</span></span>

1. <span data-ttu-id="5acc2-206">In hello Arduino IDE, fare clic su **Sketch** > **libreria includono** > **Gestisci raccolte**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="5acc2-207">Ricerca di hello seguente i nomi delle librerie uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="5acc2-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="5acc2-208">Per ogni libreria trovata fare clic su **Install** (Installa):</span><span class="sxs-lookup"><span data-stu-id="5acc2-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="5acc2-209">Installare manualmente `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="5acc2-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="5acc2-210">Andare troppo[il sito Web](https://github.com/adafruit/Adafruit_WINC1500) e fare clic su **Clone o download** > **ZIP di Download**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="5acc2-211">L'IDE Arduino, andare troppo**Sketch** > **libreria includono** > **aggiungere ZIP libreria** e aggiungere i file zip hello.</span><span class="sxs-lookup"><span data-stu-id="5acc2-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="5acc2-212">Utilizzare l'applicazione di esempio hello se non si dispone di un sensore BME280 reale</span><span class="sxs-lookup"><span data-stu-id="5acc2-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="5acc2-213">Se non si dispone di un sensore BME280 reale, l'applicazione di esempio hello possibile simulare la temperatura e umidità dati.</span><span class="sxs-lookup"><span data-stu-id="5acc2-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="5acc2-214">tooset dei dati di toouse simulate dell'applicazione di esempio hello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="5acc2-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="5acc2-215">Aprire hello `config.h` file hello `app` cartella.</span><span class="sxs-lookup"><span data-stu-id="5acc2-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="5acc2-216">Individuare hello successiva riga di codice e modificare il valore di hello da `false` troppo`true`:</span><span class="sxs-lookup"><span data-stu-id="5acc2-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurare i dati simulati toouse dell'applicazione di esempio hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="5acc2-218">Salvare file con estensione hello `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="5acc2-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="5acc2-219">Distribuire tooFeather applicazione di esempio hello Wi-Fi M0</span><span class="sxs-lookup"><span data-stu-id="5acc2-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="5acc2-220">In hello Arduino IDE, fare clic su **strumento** > **porta**, quindi fare clic su porta seriale hello per Wi-Fi M0 sfumatura.</span><span class="sxs-lookup"><span data-stu-id="5acc2-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="5acc2-221">Fare clic su **Sketch** > **caricare** toobuild e distribuire tooFeather applicazione di esempio hello Wi-Fi M0.</span><span class="sxs-lookup"><span data-stu-id="5acc2-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="5acc2-222">Immettere le credenziali</span><span class="sxs-lookup"><span data-stu-id="5acc2-222">Enter your credentials</span></span>

<span data-ttu-id="5acc2-223">Dopo aver completato il caricamento di hello, seguire questi passaggi tooenter le credenziali:</span><span class="sxs-lookup"><span data-stu-id="5acc2-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="5acc2-224">In hello Arduino IDE, fare clic su **strumenti** > **monitoraggio seriale**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="5acc2-225">Nell'angolo inferiore destro hello della finestra di monitoraggio seriale hello selezionare **alcuna terminazione di riga** nell'elenco a discesa hello hello sinistra.</span><span class="sxs-lookup"><span data-stu-id="5acc2-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="5acc2-226">Selezionare **115200 baud** nell'elenco a discesa hello hello destra.</span><span class="sxs-lookup"><span data-stu-id="5acc2-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="5acc2-227">Nella casella di input hello nella parte superiore di hello, immettere le seguenti informazioni se si è hello frequenti tooprovide e fare clic su **inviare**:</span><span class="sxs-lookup"><span data-stu-id="5acc2-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="5acc2-228">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="5acc2-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="5acc2-229">Password Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="5acc2-229">Wi-Fi password</span></span>
   * <span data-ttu-id="5acc2-230">Stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5acc2-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="5acc2-231">informazioni sulle credenziali Hello viene archiviati in hello EEPROM di sfumatura M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="5acc2-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="5acc2-232">Se si fa clic su pulsante Reimposta hello in hello Lavagna Wi-Fi M0 sfumatura, applicazione di esempio hello chiede se si desiderano informazioni hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="5acc2-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="5acc2-233">Immettere `Y` informazioni hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="5acc2-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="5acc2-234">Verrà chiesto informazioni hello tooprovide una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="5acc2-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="5acc2-235">Verificare che l'applicazione di esempio hello venga eseguita correttamente</span><span class="sxs-lookup"><span data-stu-id="5acc2-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="5acc2-236">Se viene visualizzato seguito hello output della finestra di monitoraggio seriale hello e hello lampeggiante LED su Wi-Fi M0 sfumatura, applicazione di esempio hello venga eseguita correttamente:</span><span class="sxs-lookup"><span data-stu-id="5acc2-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Output finale nell'IDE Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="5acc2-238">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5acc2-238">Next steps</span></span>

<span data-ttu-id="5acc2-239">Connessione Wi-Fi M0 sfumatura tooyour IoT hub e inviati hello acquisita l'hub IoT tooyour sensore dati completata.</span><span class="sxs-lookup"><span data-stu-id="5acc2-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

