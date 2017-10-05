---
title: Da ESP8266 al cloud - Connettere Feather HUZZAH ESP8266 ad Azure IoT Hub | Documentazione Microsoft
description: Informazioni su come configurare e connettere Adafruit Feather HUZZAH ESP8266 all'hub IoT in modo che invii i dati alla piattaforma cloud di Azure in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="b62ab-103">Connettere Adafruit Feather HUZZAH ESP8266 ad Azure IoT Hub nel cloud</span><span class="sxs-lookup"><span data-stu-id="b62ab-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connessione tra DHT22, Feather HUZZAH ESP8266 e l'hub IoT](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="b62ab-105">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="b62ab-105">What you do</span></span>


<span data-ttu-id="b62ab-106">Connettere Adafruit Feather HUZZAH ESP8266 a un hub IoT che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="b62ab-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="b62ab-107">Eseguire un'applicazione di esempio in ESP8266 per raccogliere dati di temperatura e umidità da un sensore DHT22.</span><span class="sxs-lookup"><span data-stu-id="b62ab-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="b62ab-108">Infine inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b62ab-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b62ab-109">Se si usano altre schede ESP8266, è comunque possibile seguire questa procedura per connetterle all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b62ab-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="b62ab-110">A seconda della scheda ESP8266 usata, potrebbe essere necessario riconfigurare il `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="b62ab-111">Ad esempio se si usa ESP8266 di AI-Thinker, è possibile modificarne l'impostazione da `0` a `2`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="b62ab-112">Se non si ha ancora un kit,</span><span class="sxs-lookup"><span data-stu-id="b62ab-112">Don't have a kit yet?</span></span> <span data-ttu-id="b62ab-113">è possibile ottenerlo nel [sito Web Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="b62ab-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="b62ab-114">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b62ab-114">What you learn</span></span>

* <span data-ttu-id="b62ab-115">Come creare un hub IoT e registrare un dispositivo per Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b62ab-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="b62ab-116">Come connettere Feather HUZZAH ESP8266 al sensore e al computer</span><span class="sxs-lookup"><span data-stu-id="b62ab-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="b62ab-117">Come raccogliere i dati del sensore eseguendo un'applicazione di esempio in Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b62ab-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="b62ab-118">Come inviare i dati del sensore all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="b62ab-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b62ab-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="b62ab-119">What you need</span></span>

![Componenti necessari per l'esercitazione](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="b62ab-121">Per completare questa operazione è necessario disporre dei componenti seguenti di Feather HUZZAH ESP8266 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="b62ab-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="b62ab-122">Scheda Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b62ab-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="b62ab-123">Cavo USB Micro/tipo A</span><span class="sxs-lookup"><span data-stu-id="b62ab-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="b62ab-124">Per l'ambiente di sviluppo sono necessari anche gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b62ab-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="b62ab-125">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="b62ab-125">An active Azure subscription.</span></span> <span data-ttu-id="b62ab-126">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b62ab-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b62ab-127">Mac o PC che esegue Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b62ab-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="b62ab-128">Rete wireless a cui Feather HUZZAH ESP8266 deve connettersi.</span><span class="sxs-lookup"><span data-stu-id="b62ab-128">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="b62ab-129">Connessione Internet per scaricare lo strumento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b62ab-129">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="b62ab-130">[IDE Arduino](https://www.arduino.cc/en/main/software) 1.6.8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b62ab-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="b62ab-131">Le versioni precedenti non funzionano con la libreria AzureIoT.</span><span class="sxs-lookup"><span data-stu-id="b62ab-131">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="b62ab-132">Gli elementi seguenti sono facoltativi nel caso in cui non si disponga di un sensore.</span><span class="sxs-lookup"><span data-stu-id="b62ab-132">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="b62ab-133">È possibile anche usare dati di sensori simulati.</span><span class="sxs-lookup"><span data-stu-id="b62ab-133">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="b62ab-134">Sensore di temperatura e umidità Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="b62ab-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="b62ab-135">Basetta sperimentale</span><span class="sxs-lookup"><span data-stu-id="b62ab-135">A breadboard</span></span>
* <span data-ttu-id="b62ab-136">Cavi ponticello M/M</span><span class="sxs-lookup"><span data-stu-id="b62ab-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="b62ab-137">Connettere Feather HUZZAH ESP8266 con il sensore e il computer</span><span class="sxs-lookup"><span data-stu-id="b62ab-137">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="b62ab-138">In questa sezione si connettono i sensori alla scheda.</span><span class="sxs-lookup"><span data-stu-id="b62ab-138">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="b62ab-139">Quindi si collega il dispositivo al computer per poterlo usare.</span><span class="sxs-lookup"><span data-stu-id="b62ab-139">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="b62ab-140">Connettere un sensore di temperatura e umidità DHT22 a Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b62ab-140">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="b62ab-141">Usare la basetta sperimentale e i cavi ponticello per stabilire la connessione come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b62ab-141">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="b62ab-142">Se non si dispone di un sensore, ignorare questa sezione in quanto è possibile usare i dati di sensori simulati.</span><span class="sxs-lookup"><span data-stu-id="b62ab-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Riferimento per le connessioni](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="b62ab-144">Per i pin dei sensori usare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b62ab-144">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="b62ab-145">Inizio (sensore)</span><span class="sxs-lookup"><span data-stu-id="b62ab-145">Start (Sensor)</span></span>           | <span data-ttu-id="b62ab-146">Fine (scheda)</span><span class="sxs-lookup"><span data-stu-id="b62ab-146">End (Board)</span></span>           | <span data-ttu-id="b62ab-147">Colore del cavo</span><span class="sxs-lookup"><span data-stu-id="b62ab-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="b62ab-148">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="b62ab-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="b62ab-149">3V (Pin 58H)</span><span class="sxs-lookup"><span data-stu-id="b62ab-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="b62ab-150">Cavo rosso</span><span class="sxs-lookup"><span data-stu-id="b62ab-150">Red cable</span></span>     |
| <span data-ttu-id="b62ab-151">DATI (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="b62ab-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="b62ab-152">GPIO 2 (Pin 46A)</span><span class="sxs-lookup"><span data-stu-id="b62ab-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="b62ab-153">Cavo blu</span><span class="sxs-lookup"><span data-stu-id="b62ab-153">Blue cable</span></span>    |
| <span data-ttu-id="b62ab-154">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="b62ab-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="b62ab-155">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="b62ab-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="b62ab-156">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="b62ab-156">Black cable</span></span>   |

<span data-ttu-id="b62ab-157">Per altre informazioni, vedere la [configurazione del sensore Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) e la [piedinatura di Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="b62ab-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="b62ab-158">Ora Feather Huzzah ESP8266 è connesso con un sensore funzionante.</span><span class="sxs-lookup"><span data-stu-id="b62ab-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Connettere DHT22 a Feather HUZZAH](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="b62ab-160">Connettere Feather HUZZAH ESP8266 al computer</span><span class="sxs-lookup"><span data-stu-id="b62ab-160">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="b62ab-161">Usare il cavo USB Micro/tipo A per connettere Feather HUZZAH ESP8266 al computer.</span><span class="sxs-lookup"><span data-stu-id="b62ab-161">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Connettere Feather HUZZAH al computer](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="b62ab-163">Aggiungere le autorizzazioni per la porta seriale (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b62ab-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="b62ab-164">Se si usa Ubuntu, assicurarsi di avere le autorizzazioni per operare sulla porta USB di Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b62ab-164">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b62ab-165">Per aggiungere autorizzazioni sulla porta seriale, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="b62ab-165">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="b62ab-166">Eseguire i comandi seguenti in un terminale:</span><span class="sxs-lookup"><span data-stu-id="b62ab-166">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="b62ab-167">Si ottiene uno degli output seguenti:</span><span class="sxs-lookup"><span data-stu-id="b62ab-167">You get one of the following outputs:</span></span>

   * <span data-ttu-id="b62ab-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b62ab-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="b62ab-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b62ab-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="b62ab-170">Nell'output osservare che `uucp` o `dialout` è il nome del proprietario del gruppo della porta USB.</span><span class="sxs-lookup"><span data-stu-id="b62ab-170">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="b62ab-171">Aggiungere l'utente al gruppo eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b62ab-171">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="b62ab-172">`<group-owner-name>` è il nome del proprietario gruppo ottenuto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="b62ab-172">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="b62ab-173">`<username>` è il nome utente di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b62ab-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="b62ab-174">Disconnettere Ubuntu, quindi accedere di nuovo per visualizzare la modifica.</span><span class="sxs-lookup"><span data-stu-id="b62ab-174">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="b62ab-175">Raccogliere i dati del sensore e inviarli all'hub IoT</span><span class="sxs-lookup"><span data-stu-id="b62ab-175">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="b62ab-176">In questa sezione si distribuisce un'applicazione di esempio in Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b62ab-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b62ab-177">L'applicazione di esempio fa lampeggiare il LED sulla scheda Feather HUZZAH ESP8266 e invia i dati di temperatura e umidità raccolti dal sensore DHT22 all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b62ab-177">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="b62ab-178">Ottenere l'applicazione di esempio da Github</span><span class="sxs-lookup"><span data-stu-id="b62ab-178">Get the sample application from GitHub</span></span>

<span data-ttu-id="b62ab-179">L'applicazione di esempio è ospitata in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b62ab-179">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="b62ab-180">Clonare il repository di esempio che contiene l'applicazione di esempio da GitHub.</span><span class="sxs-lookup"><span data-stu-id="b62ab-180">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="b62ab-181">Per clonare il repository di esempio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="b62ab-181">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="b62ab-182">Aprire un prompt dei comandi o una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="b62ab-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="b62ab-183">Passare alla cartella in cui archiviare l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="b62ab-183">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="b62ab-184">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b62ab-184">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="b62ab-185">Installare il pacchetto per Feather HUZZAH ESP8266 nell'IDE Arduino:</span><span class="sxs-lookup"><span data-stu-id="b62ab-185">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="b62ab-186">Aprire la cartella in cui è archiviata l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="b62ab-186">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="b62ab-187">Aprire il file app.ino nella cartella dell'app nell'IDE Arduino.</span><span class="sxs-lookup"><span data-stu-id="b62ab-187">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Aprire l'applicazione di esempio nell'IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="b62ab-189">Nell'IDE di Arduino fare clic su **File** > **Preferenze**.</span><span class="sxs-lookup"><span data-stu-id="b62ab-189">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="b62ab-190">Nella finestra di dialogo **Preferences** (Preferenze) fare clic sull'icona accanto alla casella **Additional Boards Manager URLs** (URL di gestione schede aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="b62ab-190">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="b62ab-191">Nella finestra a comparsa immettere l'URL seguente e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b62ab-191">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Puntare all'URL di un pacchetto nell'IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="b62ab-193">Nella finestra di dialogo **Preferenza** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b62ab-193">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="b62ab-194">Fare clic su **Strumenti** > **Bacheca** > **Boards Manager** (Gestione bacheche) e quindi cercare esp8266.</span><span class="sxs-lookup"><span data-stu-id="b62ab-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="b62ab-195">Boards Manager indica che è installata ESP8266 con una versione 2.2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b62ab-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Il pacchetto esp8266 è installato](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="b62ab-197">Fare clic su **Strumenti** > **Bacheca** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="b62ab-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="b62ab-198">Installare le librerie necessarie</span><span class="sxs-lookup"><span data-stu-id="b62ab-198">Install necessary libraries</span></span>

1. <span data-ttu-id="b62ab-199">Nell'IDE di Arduino fare clic su **Schizzo** > **Include Library** (Includi libreria)  > **Gestisci librerie**.</span><span class="sxs-lookup"><span data-stu-id="b62ab-199">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="b62ab-200">Cercare i seguenti nomi di libreria uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="b62ab-200">Search for the following library names one by one.</span></span> <span data-ttu-id="b62ab-201">Per ogni libreria trovata fare clic su **Install** (Installa).</span><span class="sxs-lookup"><span data-stu-id="b62ab-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="b62ab-202">Non si dispone di un sensore DHT22 reale?</span><span class="sxs-lookup"><span data-stu-id="b62ab-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="b62ab-203">L'applicazione di esempio consente di simulare i dati di temperatura e umidità nel caso non si disponga di un sensore DHT22 reale.</span><span class="sxs-lookup"><span data-stu-id="b62ab-203">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="b62ab-204">Per abilitare l'applicazione di esempio all'uso di dati simulati, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b62ab-204">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="b62ab-205">Aprire il file `config.h` nella cartella `app`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-205">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="b62ab-206">Individuare la seguente riga di codice e modificare il valore da `false` a `true`:</span><span class="sxs-lookup"><span data-stu-id="b62ab-206">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurare l'applicazione di esempio per l'uso di dati simulati](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="b62ab-208">Salvare il file con `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-208">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="b62ab-209">Distribuire l'applicazione di esempio in Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b62ab-209">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="b62ab-210">Nell'IDE di Arduino fare clic su **Strumento** > **Porta** e quindi fare clic sulla porta seriale per Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b62ab-210">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="b62ab-211">Fare clic su **Schizzo** > **Carica** per compilare e distribuire l'applicazione di esempio in Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b62ab-211">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="b62ab-212">Immettere le credenziali</span><span class="sxs-lookup"><span data-stu-id="b62ab-212">Enter your credentials</span></span>

<span data-ttu-id="b62ab-213">Una volta completato l'upload, seguire questa procedura per immettere le credenziali:</span><span class="sxs-lookup"><span data-stu-id="b62ab-213">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="b62ab-214">Nell'IDE di Arduino fare clic su **Strumenti** > **Serial Monitor** (Monitoraggio seriale).</span><span class="sxs-lookup"><span data-stu-id="b62ab-214">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="b62ab-215">Nella finestra del monitoraggio seriale notare i due elenchi a discesa nell'angolo inferiore destro.</span><span class="sxs-lookup"><span data-stu-id="b62ab-215">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="b62ab-216">Selezionare **No line ending** (Senza terminazione di riga) per la casella di riepilogo a discesa a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b62ab-216">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="b62ab-217">Selezionare **115200 baud** per la casella di riepilogo a discesa a destra.</span><span class="sxs-lookup"><span data-stu-id="b62ab-217">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="b62ab-218">Nella casella di input nella parte superiore della finestra del monitoraggio seriale immettere le informazioni seguenti, se viene richiesto di fornirle, e quindi fare clic su **Invia**.</span><span class="sxs-lookup"><span data-stu-id="b62ab-218">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="b62ab-219">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="b62ab-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="b62ab-220">Password Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="b62ab-220">Wi-Fi password</span></span>
   * <span data-ttu-id="b62ab-221">Stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="b62ab-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="b62ab-222">Le informazioni sulle credenziali sono archiviate in EEPROM di Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b62ab-222">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b62ab-223">Se si fa clic sul pulsante di reset della scheda Feather HUZZAH ESP8266, l'applicazione di esempio chiede se si vuole cancellare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="b62ab-223">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="b62ab-224">Immettere `Y` per cancellare le informazioni.</span><span class="sxs-lookup"><span data-stu-id="b62ab-224">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="b62ab-225">Viene chiesto di specificare nuovamente le informazioni.</span><span class="sxs-lookup"><span data-stu-id="b62ab-225">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="b62ab-226">Verificare che l'applicazione di esempio venga eseguita correttamente</span><span class="sxs-lookup"><span data-stu-id="b62ab-226">Verify the sample application is running successfully</span></span>

<span data-ttu-id="b62ab-227">Se si vede il seguente output dalla finestra di monitoraggio seriale e il LED di Feather HUZZAH ESP8266 lampeggia, significa che l'applicazione di esempio si esegue correttamente.</span><span class="sxs-lookup"><span data-stu-id="b62ab-227">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Output finale nell'IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="b62ab-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b62ab-229">Next steps</span></span>

<span data-ttu-id="b62ab-230">La scheda Feather HUZZAH ESP8266 è stata connessa all'hub IoT e i dati acquisiti dal sensore sono stati inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b62ab-230">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

