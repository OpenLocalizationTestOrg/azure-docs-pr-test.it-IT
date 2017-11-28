---
title: Da ESP8266 al cloud - Connettere Sparkfun ESP8266 Thing Dev all'hub IoT di Azure | Microsoft Docs
description: Informazioni su come configurare e connettere Sparkfun ESP8266 Thing Dev all'hub IoT in modo che invii i dati alla piattaforma cloud di Azure in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="3db6f-103">Connettere Sparkfun ESP8266 Thing Dev all'hub IoT di Azure nel cloud</span><span class="sxs-lookup"><span data-stu-id="3db6f-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![connessione tra DHT22, Thing Dev e hub IoT](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="3db6f-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3db6f-105">What you will do</span></span>

<span data-ttu-id="3db6f-106">Connettere Sparkfun ESP8266 Thing Dev a un hub IoT che l'utente creerà.</span><span class="sxs-lookup"><span data-stu-id="3db6f-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="3db6f-107">Quindi eseguire un'applicazione di esempio in ESP8266 per raccogliere dati di temperatura e umidità da un sensore DHT22.</span><span class="sxs-lookup"><span data-stu-id="3db6f-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="3db6f-108">Infine inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3db6f-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="3db6f-109">Se si usano altre schede ESP8266, è comunque possibile seguire questi passaggi per connetterle all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3db6f-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="3db6f-110">A seconda della scheda ESP8266 in uso, potrebbe essere necessario riconfigurare il `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="3db6f-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="3db6f-111">Ad esempio, se si usa ESP8266 da AI-Thinker, è possibile modificarlo da `0` a `2`.</span><span class="sxs-lookup"><span data-stu-id="3db6f-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="3db6f-112">Non si dispone ancora di un kit? Fare clic [qui](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="3db6f-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3db6f-113">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3db6f-113">What you will learn</span></span>

* <span data-ttu-id="3db6f-114">Come creare un hub IoT e registrare un dispositivo per Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3db6f-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="3db6f-115">Come connettere Thing Dev con il sensore e il computer.</span><span class="sxs-lookup"><span data-stu-id="3db6f-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="3db6f-116">Come raccogliere i dati del sensore eseguendo un'applicazione di esempio in Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3db6f-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="3db6f-117">Come inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3db6f-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="3db6f-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3db6f-118">What you will need</span></span>

![Parti necessarie per l'esercitazione](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="3db6f-120">Per completare questa operazione, è necessario disporre dei componenti seguenti dello starter kit di Thing Dev:</span><span class="sxs-lookup"><span data-stu-id="3db6f-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="3db6f-121">La scheda Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3db6f-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="3db6f-122">Un cavo USB Micro/tipo A.</span><span class="sxs-lookup"><span data-stu-id="3db6f-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="3db6f-123">Per l'ambiente di sviluppo sono necessari anche gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3db6f-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="3db6f-124">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="3db6f-124">An active Azure subscription.</span></span> <span data-ttu-id="3db6f-125">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="3db6f-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="3db6f-126">Mac o PC che esegue Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3db6f-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="3db6f-127">Rete wireless per Sparkfun ESP8266 Thing Dev a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="3db6f-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="3db6f-128">Connessione Internet per scaricare lo strumento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="3db6f-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="3db6f-129">[IDE di Arduino](https://www.arduino.cc/en/main/software) versione 1.6.8 (o successive), le versioni precedenti non funzioneranno con la libreria AzureIoT.</span><span class="sxs-lookup"><span data-stu-id="3db6f-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="3db6f-130">Gli elementi seguenti sono facoltativi nel caso in cui non si disponga di un sensore.</span><span class="sxs-lookup"><span data-stu-id="3db6f-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="3db6f-131">È possibile anche usare dati di sensori simulati.</span><span class="sxs-lookup"><span data-stu-id="3db6f-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="3db6f-132">Un sensore di temperatura e umidità Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="3db6f-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="3db6f-133">Una basetta sperimentale.</span><span class="sxs-lookup"><span data-stu-id="3db6f-133">A breadboard.</span></span>
* <span data-ttu-id="3db6f-134">Cavi ponticello M/M.</span><span class="sxs-lookup"><span data-stu-id="3db6f-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="3db6f-135">Connettere ESP8266 Thing Dev con il sensore e il computer</span><span class="sxs-lookup"><span data-stu-id="3db6f-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="3db6f-136">Connettere un sensore di temperatura e umidità DHT22 a ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="3db6f-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="3db6f-137">Usare la basetta sperimentale e i cavi ponticello per stabilire la connessione come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3db6f-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="3db6f-138">Se non si dispone di un sensore, ignorare questa sezione in quanto è possibile usare i dati di sensori simulati.</span><span class="sxs-lookup"><span data-stu-id="3db6f-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Riferimento per le connessioni](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="3db6f-140">Per i pin dei sensori verranno usati i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3db6f-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="3db6f-141">Inizio (sensore)</span><span class="sxs-lookup"><span data-stu-id="3db6f-141">Start (Sensor)</span></span>           | <span data-ttu-id="3db6f-142">Fine (scheda)</span><span class="sxs-lookup"><span data-stu-id="3db6f-142">End (Board)</span></span>           | <span data-ttu-id="3db6f-143">Colore del cavo</span><span class="sxs-lookup"><span data-stu-id="3db6f-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="3db6f-144">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="3db6f-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="3db6f-145">3V (Pin 8A)</span><span class="sxs-lookup"><span data-stu-id="3db6f-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="3db6f-146">Cavo rosso</span><span class="sxs-lookup"><span data-stu-id="3db6f-146">Red cable</span></span>     |
| <span data-ttu-id="3db6f-147">DATA (Pin 28F)</span><span class="sxs-lookup"><span data-stu-id="3db6f-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="3db6f-148">GPIO 2 (Pin 9A)</span><span class="sxs-lookup"><span data-stu-id="3db6f-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="3db6f-149">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="3db6f-149">White cable</span></span>    |
| <span data-ttu-id="3db6f-150">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="3db6f-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="3db6f-151">GND (Pin 7J)</span><span class="sxs-lookup"><span data-stu-id="3db6f-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="3db6f-152">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="3db6f-152">Black cable</span></span>   |


- <span data-ttu-id="3db6f-153">Per altre informazioni, vedere: [installazione del sensore DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) e [specifiche di Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="3db6f-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="3db6f-154">Ora Sparkfun ESP8266 Thing Dev è connesso con un sensore funzionante.</span><span class="sxs-lookup"><span data-stu-id="3db6f-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![collegare DHT22 con ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="3db6f-156">Collegare Sparkfun ESP8266 Thing Dev al computer</span><span class="sxs-lookup"><span data-stu-id="3db6f-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="3db6f-157">Usare il cavo USB Micro/tipo A per connettere Sparkfun ESP8266 Thing Dev al computer come segue.</span><span class="sxs-lookup"><span data-stu-id="3db6f-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![Connettere Feather HUZZAH al computer](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="3db6f-159">Aggiungere le autorizzazioni per la porta seriale: solo in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3db6f-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="3db6f-160">Se si usa Ubuntu, assicurarsi che un normale utente abbia le autorizzazioni per operare sulla porta USB di Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3db6f-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="3db6f-161">Per aggiungere autorizzazioni sulla porta seriale per un utente normale, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="3db6f-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="3db6f-162">Eseguire i comandi seguenti in un terminale:</span><span class="sxs-lookup"><span data-stu-id="3db6f-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="3db6f-163">Si ottiene uno degli output seguenti:</span><span class="sxs-lookup"><span data-stu-id="3db6f-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="3db6f-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="3db6f-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="3db6f-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="3db6f-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="3db6f-166">Nell'output si osservi `uucp` o `dialout` che rappresenta il nome del proprietario gruppo della porta USB.</span><span class="sxs-lookup"><span data-stu-id="3db6f-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="3db6f-167">Aggiungere l'utente al gruppo eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3db6f-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="3db6f-168">`<group-owner-name>` è il nome del proprietario gruppo ottenuto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="3db6f-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="3db6f-169">`<username>` è il nome utente di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3db6f-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="3db6f-170">Eseguire la disconnessione da Ubuntu e quindi un nuovo accesso per rendere effettive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="3db6f-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="3db6f-171">Raccogliere i dati del sensore e inviarli all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="3db6f-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="3db6f-172">In questa sezione si distribuisce e si esegue un'applicazione di esempio in Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3db6f-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="3db6f-173">L'applicazione di esempio fa lampeggiare il LED in Sparkfun ESP8266 Thing Dev e invia i dati di temperatura e umidità raccolti dal sensore DHT22 all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3db6f-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="3db6f-174">Ottenere l'applicazione di esempio da Github</span><span class="sxs-lookup"><span data-stu-id="3db6f-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="3db6f-175">L'applicazione di esempio è ospitata in GitHub.</span><span class="sxs-lookup"><span data-stu-id="3db6f-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="3db6f-176">Clonare il repository di esempio che contiene l'applicazione di esempio da GitHub.</span><span class="sxs-lookup"><span data-stu-id="3db6f-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="3db6f-177">Per clonare il repository di esempio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="3db6f-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="3db6f-178">Aprire un prompt dei comandi o una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="3db6f-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="3db6f-179">Passare alla cartella in cui archiviare l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="3db6f-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="3db6f-180">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3db6f-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="3db6f-181">Installare il pacchetto per Sparkfun ESP8266 Thing Dev nell'IDE di Arduino:</span><span class="sxs-lookup"><span data-stu-id="3db6f-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="3db6f-182">Aprire la cartella in cui è archiviata l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="3db6f-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="3db6f-183">Aprire il file app.ino nella cartella dell'app nell'IDE di Arduino.</span><span class="sxs-lookup"><span data-stu-id="3db6f-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![Aprire l'applicazione di esempio nell'IDE di Arduino](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="3db6f-185">Nell'IDE di Arduino fare clic su **File** > **Preferenze**.</span><span class="sxs-lookup"><span data-stu-id="3db6f-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="3db6f-186">Nella finestra di dialogo **Preferenze** fare clic sull'icona accanto alla casella di testo **Additional Boards Manager URLs** (URL di gestione bacheche aggiuntivo).</span><span class="sxs-lookup"><span data-stu-id="3db6f-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="3db6f-187">Nella finestra a comparsa immettere l'URL seguente e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3db6f-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Puntare all'URL di un pacchetto nell'IDE di Arduino](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="3db6f-189">Nella finestra di dialogo **Preferenza** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3db6f-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="3db6f-190">Fare clic su **Strumenti** > **Bacheca** > **Boards Manager** (Gestione bacheche) e quindi cercare esp8266.</span><span class="sxs-lookup"><span data-stu-id="3db6f-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="3db6f-191">Deve essere installato ESP8266 versione 2.2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="3db6f-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Il pacchetto esp8266 è installato](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="3db6f-193">Fare clic su **Strumenti** > **Scheda** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="3db6f-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="3db6f-194">Installare le librerie necessarie</span><span class="sxs-lookup"><span data-stu-id="3db6f-194">Install necessary libraries</span></span>

1. <span data-ttu-id="3db6f-195">Nell'IDE di Arduino fare clic su **Schizzo** > **Include Library** (Includi libreria)  > **Gestisci librerie**.</span><span class="sxs-lookup"><span data-stu-id="3db6f-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="3db6f-196">Cercare i seguenti nomi di libreria uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="3db6f-196">Search for the following library names one by one.</span></span> <span data-ttu-id="3db6f-197">Per ciascuna delle librerie individuate fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="3db6f-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="3db6f-198">Non si dispone di un sensore DHT22 reale?</span><span class="sxs-lookup"><span data-stu-id="3db6f-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="3db6f-199">L'applicazione di esempio consente di simulare i dati di temperatura e umidità nel caso non si disponga di un sensore DHT22 reale.</span><span class="sxs-lookup"><span data-stu-id="3db6f-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="3db6f-200">Per abilitare l'applicazione di esempio all'uso di dati simulati, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="3db6f-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="3db6f-201">Aprire il file `config.h` nella cartella `app`.</span><span class="sxs-lookup"><span data-stu-id="3db6f-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="3db6f-202">Individuare la seguente riga di codice e modificare il valore da `false` a `true`:</span><span class="sxs-lookup"><span data-stu-id="3db6f-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurare l'applicazione di esempio per l'uso di dati simulati](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="3db6f-204">Salvare con `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="3db6f-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="3db6f-205">Distribuire l'applicazione di esempio in Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="3db6f-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="3db6f-206">Nell'IDE di Arduino fare clic su **Strumento** > **Porta** e quindi fare clic sulla porta seriale di Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3db6f-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="3db6f-207">Fare clic su **Schizzo** > **Carica** per compilare e distribuire l'applicazione di esempio in Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3db6f-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="3db6f-208">Se si usa macOS è possibile visualizzare i messaggi seguenti durante il caricamento.</span><span class="sxs-lookup"><span data-stu-id="3db6f-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="3db6f-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="3db6f-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="3db6f-210">Aprire la finestra del terminal e completare le azioni riportate di seguito per risolvere questo problema.</span><span class="sxs-lookup"><span data-stu-id="3db6f-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="3db6f-211">Immettere le credenziali</span><span class="sxs-lookup"><span data-stu-id="3db6f-211">Enter your credentials</span></span>

<span data-ttu-id="3db6f-212">Dopo aver completato il caricamento, seguire i passaggi per immettere le credenziali:</span><span class="sxs-lookup"><span data-stu-id="3db6f-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="3db6f-213">Nell'IDE di Arduino fare clic su **Strumenti** > **Serial Monitor** (Monitoraggio seriale).</span><span class="sxs-lookup"><span data-stu-id="3db6f-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="3db6f-214">Nella finestra del monitoraggio seriale notare i due elenchi a discesa nella parte inferiore destra.</span><span class="sxs-lookup"><span data-stu-id="3db6f-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="3db6f-215">Selezionare **No line ending** (Senza terminazione di riga) per la casella di riepilogo a discesa a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3db6f-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="3db6f-216">Selezionare **115200 baud** per la casella di riepilogo a discesa a destra.</span><span class="sxs-lookup"><span data-stu-id="3db6f-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="3db6f-217">Nella casella di input nella parte superiore della finestra del monitoraggio seriale immettere le informazioni seguenti, se viene richiesto di fornirle, e quindi fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="3db6f-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="3db6f-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="3db6f-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="3db6f-219">Password Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="3db6f-219">Wi-Fi password</span></span>
   * <span data-ttu-id="3db6f-220">Stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="3db6f-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="3db6f-221">Le informazioni sulle credenziali sono archiviate in EEPROM di Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3db6f-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="3db6f-222">Se si fa clic sul pulsante di reset della scheda di Sparkfun ESP8266 Thing Dev, l'applicazione di esempio chiede se si desidera cancellare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="3db6f-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="3db6f-223">Immettere `Y` per cancellare le informazioni e verrà chiesto di fornirle nuovamente.</span><span class="sxs-lookup"><span data-stu-id="3db6f-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="3db6f-224">Verificare che l'applicazione di esempio venga eseguita correttamente</span><span class="sxs-lookup"><span data-stu-id="3db6f-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="3db6f-225">Se si vede il seguente output dalla finestra di monitoraggio seriale e il LED di Sparkfun ESP8266 Thing Dev lampeggia, significa che l'applicazione di esempio viene eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="3db6f-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![Output finale nell'IDE di Arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="3db6f-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3db6f-227">Next steps</span></span>

<span data-ttu-id="3db6f-228">Sparkfun ESP8266 Thing Dev si è connessa correttamente all'hub IoT e i dati acquisiti dal sensore sono stati inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3db6f-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
