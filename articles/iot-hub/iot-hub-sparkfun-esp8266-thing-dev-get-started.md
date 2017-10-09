---
title: aaaESP8266 toocloud - connettersi Sparkfun ESP8266 cosa Dev tooAzure IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi tooAzure Sparkfun ESP8266 cosa Dev IoT Hub per tale piattaforma cloud di Azure di toosend dati toohello in questa esercitazione.
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
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="6d6b2-103">Connettersi tooAzure Sparkfun ESP8266 cosa Dev IoT Hub nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="6d6b2-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![connessione tra DHT22, Thing Dev e hub IoT](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="6d6b2-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6d6b2-105">What you will do</span></span>

<span data-ttu-id="6d6b2-106">La connessione verrà creato l'hub IoT tooan Sparkfun ESP8266 cosa Dev.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="6d6b2-107">Quindi eseguire un'applicazione di esempio sui dati di temperatura e umidità toocollect ESP8266 da un sensore DHT22.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="6d6b2-108">Infine, inviare l'hub IoT hello sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="6d6b2-109">Se si usano altri lavagne ESP8266, è comunque possibile eseguire questi passaggi tooconnect è tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="6d6b2-110">A seconda della Lavagna hello ESP8266 in uso, potrebbe essere necessario hello tooreconfigure `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="6d6b2-111">Ad esempio, se si utilizza ESP8266 da AI Thinker, è possibile modificare tale da `0` troppo`2`.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="6d6b2-112">Non si dispone ancora di un kit? Fare clic [qui](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6d6b2-113">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="6d6b2-113">What you will learn</span></span>

* <span data-ttu-id="6d6b2-114">Come toocreate un hub IoT e registrare un dispositivo per scopi di sviluppo cosa</span><span class="sxs-lookup"><span data-stu-id="6d6b2-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="6d6b2-115">Come tooconnect cosa Dev con sensore hello e il computer.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="6d6b2-116">Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su cosa scopi di sviluppo</span><span class="sxs-lookup"><span data-stu-id="6d6b2-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="6d6b2-117">Come toosend hello hub IoT tooyour di dati del sensore.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="6d6b2-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6d6b2-118">What you will need</span></span>

![Parti necessarie per l'esercitazione hello](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="6d6b2-120">toocomplete questa operazione, è necessario hello dallo Starter Kit di sviluppo cosa le seguenti parti:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="6d6b2-121">Hello Sparkfun ESP8266 cosa Dev Lavagna.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="6d6b2-122">Un tooType USB Micro cavo USB A.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="6d6b2-123">Esempio hello è inoltre necessario per l'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="6d6b2-124">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-124">An active Azure subscription.</span></span> <span data-ttu-id="6d6b2-125">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="6d6b2-126">Mac o PC che esegue Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="6d6b2-127">Rete wireless per tooconnect Sparkfun ESP8266 cosa Dev per.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="6d6b2-128">Strumento di configurazione hello toodownload connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="6d6b2-129">[IDE Arduino](https://www.arduino.cc/en/main/software) versione 1.6.8 (o versione successiva), le versioni precedenti non funzioneranno con libreria AzureIoT hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="6d6b2-130">Hello gli elementi seguenti sono facoltativi nel caso in cui non si dispone di un sensore.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="6d6b2-131">È anche possibile hello utilizzando i dati del sensore simulato.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="6d6b2-132">Un sensore di temperatura e umidità Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="6d6b2-133">Una basetta sperimentale.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-133">A breadboard.</span></span>
* <span data-ttu-id="6d6b2-134">Cavi ponticello M/M.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="6d6b2-135">Connessione ESP8266 cosa Dev con sensore hello e il computer</span><span class="sxs-lookup"><span data-stu-id="6d6b2-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="6d6b2-136">Connettersi a un sensore di temperatura e umidità DHT22 tooESP8266 cosa Dev</span><span class="sxs-lookup"><span data-stu-id="6d6b2-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="6d6b2-137">Utilizzare hello breadboard e ponticelli cavi toomake hello connessione come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="6d6b2-138">Se non si dispone di un sensore, ignorare questa sezione in quanto è possibile usare i dati di sensori simulati.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Riferimento per le connessioni](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="6d6b2-140">Per i codici PIN sensore, verrà utilizzato hello seguente collegamento:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="6d6b2-141">Inizio (sensore)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-141">Start (Sensor)</span></span>           | <span data-ttu-id="6d6b2-142">Fine (scheda)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-142">End (Board)</span></span>           | <span data-ttu-id="6d6b2-143">Colore del cavo</span><span class="sxs-lookup"><span data-stu-id="6d6b2-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="6d6b2-144">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="6d6b2-145">3V (Pin 8A)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="6d6b2-146">Cavo rosso</span><span class="sxs-lookup"><span data-stu-id="6d6b2-146">Red cable</span></span>     |
| <span data-ttu-id="6d6b2-147">DATA (Pin 28F)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="6d6b2-148">GPIO 2 (Pin 9A)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="6d6b2-149">Cavo bianco</span><span class="sxs-lookup"><span data-stu-id="6d6b2-149">White cable</span></span>    |
| <span data-ttu-id="6d6b2-150">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="6d6b2-151">GND (Pin 7J)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="6d6b2-152">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="6d6b2-152">Black cable</span></span>   |


- <span data-ttu-id="6d6b2-153">Per altre informazioni, vedere: [installazione del sensore DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) e [specifiche di Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="6d6b2-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="6d6b2-154">Ora Sparkfun ESP8266 Thing Dev è connesso con un sensore funzionante.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![collegare DHT22 con ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="6d6b2-156">Connettere computer tooyour Sparkfun ESP8266 cosa Dev</span><span class="sxs-lookup"><span data-stu-id="6d6b2-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="6d6b2-157">Utilizzare hello USB Micro tooType A USB cable tooconnect Sparkfun ESP8266 cosa Dev tooyour computer come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![connettere computer tooyour huzzah di sfumatura](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="6d6b2-159">Aggiungere le autorizzazioni per la porta seriale: solo in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6d6b2-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="6d6b2-160">Se si utilizza Ubuntu, assicurarsi che un utente normale ha toooperate autorizzazioni hello in hello USB porta di Sparkfun ESP8266 cosa scopi di sviluppo</span><span class="sxs-lookup"><span data-stu-id="6d6b2-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="6d6b2-161">autorizzazioni di porta seriale tooadd per un utente normale, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="6d6b2-162">Eseguire hello seguenti comandi in un terminal:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="6d6b2-163">Viene visualizzato uno dei hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="6d6b2-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="6d6b2-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="6d6b2-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="6d6b2-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="6d6b2-166">Si noti nell'output di hello, `uucp` o `dialout` ovvero hello proprietario nome del gruppo di hello porta USB.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="6d6b2-167">Aggiungi gruppo toohello hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="6d6b2-168">`<group-owner-name>`è nome del proprietario del gruppo hello ottenuto nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="6d6b2-169">`<username>` è il nome utente di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="6d6b2-170">Disconnettersi Ubuntu e ripetere l'accesso, per effetto di tootake modifica hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="6d6b2-171">Raccogliere dati del sensore e inviarle tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="6d6b2-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="6d6b2-172">In questa sezione si distribuisce e si esegue un'applicazione di esempio in Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="6d6b2-173">applicazione di esempio Hello lampeggia hello LED su Sparkfun ESP8266 cosa Dev e invia la temperatura hello e umidità raccolti da hello DHT22 sensore tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="6d6b2-174">Ottenere l'applicazione di esempio hello da GitHub</span><span class="sxs-lookup"><span data-stu-id="6d6b2-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="6d6b2-175">applicazione di esempio Hello è ospitata in GitHub.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="6d6b2-176">Clonare il repository di esempio hello che contiene l'applicazione di esempio hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="6d6b2-177">repository di esempio hello tooclone, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="6d6b2-178">Aprire un prompt dei comandi o una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="6d6b2-179">Passare tooa cartella in cui si desidera toobe applicazione di esempio hello archiviati.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="6d6b2-180">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="6d6b2-181">Installare il pacchetto di hello per Sparkfun ESP8266 cosa Dev nell'IDE Arduino:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="6d6b2-182">Aprire hello cartella dove si trova l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="6d6b2-183">Aprire il file di app.ino hello nella cartella dell'applicazione hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![Aprire l'applicazione di esempio hello in arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="6d6b2-185">In hello Arduino IDE, fare clic su **File** > **preferenze**.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="6d6b2-186">In hello **preferenze** finestra di dialogo fare clic su hello icona Avanti toohello **URL di gestione aggiuntivi lavagne** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="6d6b2-187">Nella finestra popup hello immettere hello URL seguente e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![url del pacchetto nell'ide arduino tooa punto](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="6d6b2-189">In hello **preferenza** la finestra di dialogo, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="6d6b2-190">Fare clic su **Strumenti** > **Bacheca** > **Boards Manager** (Gestione bacheche) e quindi cercare esp8266.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="6d6b2-191">Deve essere installato ESP8266 versione 2.2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![installazione del pacchetto esp8266 Hello](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="6d6b2-193">Fare clic su **Strumenti** > **Scheda** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="6d6b2-194">Installare le librerie necessarie</span><span class="sxs-lookup"><span data-stu-id="6d6b2-194">Install necessary libraries</span></span>

1. <span data-ttu-id="6d6b2-195">In hello Arduino IDE, fare clic su **Sketch** > **libreria includono** > **Gestisci raccolte**.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="6d6b2-196">Ricerca di hello seguente i nomi delle librerie uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="6d6b2-197">Per ogni libreria hello desiderati, fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="6d6b2-198">Non si dispone di un sensore DHT22 reale?</span><span class="sxs-lookup"><span data-stu-id="6d6b2-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="6d6b2-199">applicazione di esempio Hello possibile simulare la temperatura e umidità dati nel caso in cui non si dispone di un sensore DHT22 reale.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="6d6b2-200">dati toouse simulate dell'applicazione di esempio hello di tooenable, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="6d6b2-201">Aprire hello `config.h` file hello `app` cartella.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="6d6b2-202">Individuare hello successiva riga di codice e modificare il valore di hello da `false` troppo`true`:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurare i dati simulati toouse dell'applicazione di esempio hello](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="6d6b2-204">Salvare con `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="6d6b2-205">Distribuire tooSparkfun applicazione di esempio hello ESP8266 cosa Dev</span><span class="sxs-lookup"><span data-stu-id="6d6b2-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="6d6b2-206">In hello Arduino IDE, fare clic su **strumento** > **porta**, quindi fare clic su porta seriale hello per scopi di sviluppo cosa ESP8266 Sparkfun</span><span class="sxs-lookup"><span data-stu-id="6d6b2-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="6d6b2-207">Fare clic su **Sketch** > **caricare** toobuild e distribuire tooSparkfun applicazione di esempio hello ESP8266 cosa scopi di sviluppo</span><span class="sxs-lookup"><span data-stu-id="6d6b2-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="6d6b2-208">Se si utilizza macOS che è probabilmente possibile vedere hello seguendo i messaggi durante il caricamento.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="6d6b2-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="6d6b2-210">Aprire la finestra ternimal e fine toosolve azioni di sotto di questo problema.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="6d6b2-211">Immettere le credenziali</span><span class="sxs-lookup"><span data-stu-id="6d6b2-211">Enter your credentials</span></span>

<span data-ttu-id="6d6b2-212">Dopo aver completato il caricamento di hello, seguire le credenziali tooenter passaggi hello:</span><span class="sxs-lookup"><span data-stu-id="6d6b2-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="6d6b2-213">In hello Arduino IDE, fare clic su **strumenti** > **monitoraggio seriale**.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="6d6b2-214">Nella finestra di monitoraggio seriale hello, noti elenchi a discesa hello due su hello nell'angolo inferiore destro.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="6d6b2-215">Selezionare **alcuna terminazione di riga** per l'elenco a discesa sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="6d6b2-216">Selezionare **115200 baud** per l'elenco a discesa a destra hello.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="6d6b2-217">Nella casella di input hello nella parte superiore di hello della finestra di monitoraggio seriale hello, immettere le seguenti informazioni se viene chiesto tooprovide hello, quindi fare clic su **inviare**.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="6d6b2-218">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="6d6b2-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="6d6b2-219">Password Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="6d6b2-219">Wi-Fi password</span></span>
   * <span data-ttu-id="6d6b2-220">Stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="6d6b2-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="6d6b2-221">informazioni sulle credenziali Hello viene archiviati in hello EEPROM di Sparkfun ESP8266 cosa scopi di sviluppo</span><span class="sxs-lookup"><span data-stu-id="6d6b2-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="6d6b2-222">Se si fa clic su pulsante Reimposta hello in hello Lavagna Sparkfun ESP8266 cosa Dev, applicazione di esempio hello viene chiesto se si desiderano che le informazioni di hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="6d6b2-223">Immettere `Y` informazioni hello toohave cancellati e viene richiesto di informazioni di hello tooprovide nuovamente.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="6d6b2-224">Verificare l'applicazione di esempio hello venga eseguita correttamente</span><span class="sxs-lookup"><span data-stu-id="6d6b2-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="6d6b2-225">Se viene visualizzato seguito hello output della finestra di monitoraggio seriale hello e hello lampeggiante LED su Sparkfun ESP8266 cosa Dev, applicazione di esempio hello venga eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![Output finale nell'IDE di Arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="6d6b2-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6d6b2-227">Next steps</span></span>

<span data-ttu-id="6d6b2-228">Connesso a un hub IoT di tooyour Sparkfun ESP8266 cosa Dev e inviati hello acquisita l'hub IoT tooyour sensore dati completata.</span><span class="sxs-lookup"><span data-stu-id="6d6b2-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
