---
title: aaaESP8266 toocloud - connettersi sfumatura HUZZAH ESP8266 tooAzure IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi Adafruit sfumatura HUZZAH ESP8266 tooAzure IoT Hub per tale piattaforma cloud di Azure di toosend dati toohello in questa esercitazione.
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
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="b6451-103">Connettersi Adafruit sfumatura HUZZAH ESP8266 tooAzure IoT Hub nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="b6451-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connessione tra DHT22, Feather HUZZAH ESP8266 e l'hub IoT](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="b6451-105">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="b6451-105">What you do</span></span>


<span data-ttu-id="b6451-106">Connettersi Adafruit sfumatura HUZZAH ESP8266 tooan IoT hub creato.</span><span class="sxs-lookup"><span data-stu-id="b6451-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="b6451-107">Quindi eseguire un'applicazione di esempio in ESP8266 toocollect hello temperatura e umidità dati da un sensore DHT22.</span><span class="sxs-lookup"><span data-stu-id="b6451-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="b6451-108">Infine, si invia l'hub IoT hello sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="b6451-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b6451-109">Se si utilizzano altre schede ESP8266, è comunque possibile eseguire questi passaggi tooconnect è tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b6451-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="b6451-110">A seconda della Lavagna hello ESP8266 in uso, potrebbe essere necessario hello tooreconfigure `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="b6451-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="b6451-111">Ad esempio, se si utilizza ESP8266 da AI Thinker, è possibile modificarlo da `0` troppo`2`.</span><span class="sxs-lookup"><span data-stu-id="b6451-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="b6451-112">Se non si ha ancora un kit,</span><span class="sxs-lookup"><span data-stu-id="b6451-112">Don't have a kit yet?</span></span> <span data-ttu-id="b6451-113">Scaricare il pacchetto hello [sito Web di Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="b6451-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="b6451-114">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b6451-114">What you learn</span></span>

* <span data-ttu-id="b6451-115">Come toocreate un hub IoT e registrare un dispositivo per sfumatura HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b6451-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="b6451-116">Come tooconnect ESP8266 HUZZAH sfumatura con sensore hello e il computer</span><span class="sxs-lookup"><span data-stu-id="b6451-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="b6451-117">Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su ESP8266 HUZZAH sfumatura</span><span class="sxs-lookup"><span data-stu-id="b6451-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="b6451-118">Come toosend hello hub IoT tooyour di sensore dati</span><span class="sxs-lookup"><span data-stu-id="b6451-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b6451-119">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="b6451-119">What you need</span></span>

![Parti necessarie per l'esercitazione hello](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="b6451-121">toocomplete questa operazione, è necessario hello dallo Starter Kit di sfumatura HUZZAH ESP8266 le seguenti parti:</span><span class="sxs-lookup"><span data-stu-id="b6451-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="b6451-122">Hello sfumatura HUZZAH ESP8266 Lavagna</span><span class="sxs-lookup"><span data-stu-id="b6451-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="b6451-123">Un cavo USB A di tooType Micro USB</span><span class="sxs-lookup"><span data-stu-id="b6451-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="b6451-124">È inoltre necessario hello seguenti operazioni per l'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="b6451-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="b6451-125">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="b6451-125">An active Azure subscription.</span></span> <span data-ttu-id="b6451-126">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b6451-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b6451-127">Mac o PC che esegue Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b6451-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="b6451-128">Rete wireless per sfumatura HUZZAH ESP8266 tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="b6451-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="b6451-129">Strumento di configurazione hello toodownload connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="b6451-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="b6451-130">[IDE Arduino](https://www.arduino.cc/en/main/software) 1.6.8 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b6451-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="b6451-131">Le versioni precedenti non funzionano con libreria AzureIoT hello.</span><span class="sxs-lookup"><span data-stu-id="b6451-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="b6451-132">Hello gli elementi seguenti sono facoltativi nel caso in cui non si dispone di un sensore.</span><span class="sxs-lookup"><span data-stu-id="b6451-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="b6451-133">È anche possibile hello utilizzando i dati del sensore simulato.</span><span class="sxs-lookup"><span data-stu-id="b6451-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="b6451-134">Sensore di temperatura e umidità Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="b6451-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="b6451-135">Basetta sperimentale</span><span class="sxs-lookup"><span data-stu-id="b6451-135">A breadboard</span></span>
* <span data-ttu-id="b6451-136">Cavi ponticello M/M</span><span class="sxs-lookup"><span data-stu-id="b6451-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="b6451-137">Connessione ESP8266 HUZZAH sfumatura con sensore hello e il computer</span><span class="sxs-lookup"><span data-stu-id="b6451-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="b6451-138">In questa sezione è connettersi Lavagna tooyour sensori di hello.</span><span class="sxs-lookup"><span data-stu-id="b6451-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="b6451-139">Quindi si collega il computer tooyour dispositivo per l'ulteriore utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b6451-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="b6451-140">Connettersi a un DHT22 temperatura e umidità sensore tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b6451-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="b6451-141">Utilizzare hello breadboard e ponticelli cavi toomake hello connessione come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b6451-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="b6451-142">Se non si dispone di un sensore, ignorare questa sezione in quanto è possibile usare i dati di sensori simulati.</span><span class="sxs-lookup"><span data-stu-id="b6451-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Riferimento per le connessioni](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="b6451-144">Per i codici PIN sensore, utilizzare hello seguente collegamento:</span><span class="sxs-lookup"><span data-stu-id="b6451-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="b6451-145">Inizio (sensore)</span><span class="sxs-lookup"><span data-stu-id="b6451-145">Start (Sensor)</span></span>           | <span data-ttu-id="b6451-146">Fine (scheda)</span><span class="sxs-lookup"><span data-stu-id="b6451-146">End (Board)</span></span>           | <span data-ttu-id="b6451-147">Colore del cavo</span><span class="sxs-lookup"><span data-stu-id="b6451-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="b6451-148">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="b6451-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="b6451-149">3V (Pin 58H)</span><span class="sxs-lookup"><span data-stu-id="b6451-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="b6451-150">Cavo rosso</span><span class="sxs-lookup"><span data-stu-id="b6451-150">Red cable</span></span>     |
| <span data-ttu-id="b6451-151">DATI (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="b6451-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="b6451-152">GPIO 2 (Pin 46A)</span><span class="sxs-lookup"><span data-stu-id="b6451-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="b6451-153">Cavo blu</span><span class="sxs-lookup"><span data-stu-id="b6451-153">Blue cable</span></span>    |
| <span data-ttu-id="b6451-154">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="b6451-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="b6451-155">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="b6451-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="b6451-156">Cavo nero</span><span class="sxs-lookup"><span data-stu-id="b6451-156">Black cable</span></span>   |

<span data-ttu-id="b6451-157">Per altre informazioni, vedere la [configurazione del sensore Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) e la [piedinatura di Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="b6451-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="b6451-158">Ora Feather Huzzah ESP8266 è connesso con un sensore funzionante.</span><span class="sxs-lookup"><span data-stu-id="b6451-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Connettere DHT22 a Feather HUZZAH](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="b6451-160">Connettere computer tooyour ESP8266 HUZZAH sfumatura</span><span class="sxs-lookup"><span data-stu-id="b6451-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="b6451-161">Come illustrato nella figura, utilizzare hello USB Micro tooType A USB cable tooconnect sfumatura HUZZAH ESP8266 tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="b6451-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Connettere computer tooyour Huzzah sfumatura](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="b6451-163">Aggiungere le autorizzazioni per la porta seriale (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b6451-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="b6451-164">Se si utilizza Ubuntu, verificare di che aver toooperate autorizzazioni hello in hello USB porta della sfumatura HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b6451-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b6451-165">le autorizzazioni della porta seriale tooadd, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="b6451-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="b6451-166">Eseguire hello seguenti comandi in un terminal:</span><span class="sxs-lookup"><span data-stu-id="b6451-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="b6451-167">Viene visualizzato uno dei hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="b6451-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="b6451-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b6451-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="b6451-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b6451-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="b6451-170">Nell'output di hello, si noti che `uucp` o `dialout` è nome del proprietario del gruppo hello di hello porta USB.</span><span class="sxs-lookup"><span data-stu-id="b6451-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="b6451-171">Aggiungi gruppo toohello hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b6451-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="b6451-172">`<group-owner-name>`è nome del proprietario del gruppo hello ottenuto nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b6451-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="b6451-173">`<username>` è il nome utente di Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b6451-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="b6451-174">Disconnettersi da Ubuntu e quindi accedere di nuovo per hello tooappear di modifica.</span><span class="sxs-lookup"><span data-stu-id="b6451-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="b6451-175">Raccogliere dati del sensore e inviarle tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="b6451-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="b6451-176">In questa sezione si distribuisce un'applicazione di esempio in Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b6451-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b6451-177">applicazione di esempio Hello lampeggia hello LED su ESP8266 HUZZAH sfumatura e invia la temperatura hello e umidità raccolti da hello DHT22 sensore tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b6451-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="b6451-178">Ottenere l'applicazione di esempio hello da GitHub</span><span class="sxs-lookup"><span data-stu-id="b6451-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="b6451-179">applicazione di esempio Hello è ospitata in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6451-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="b6451-180">Clonare il repository di esempio hello che contiene l'applicazione di esempio hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="b6451-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="b6451-181">repository di esempio hello tooclone, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="b6451-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="b6451-182">Aprire un prompt dei comandi o una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="b6451-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="b6451-183">Passare tooa cartella in cui si desidera toobe applicazione di esempio hello archiviati.</span><span class="sxs-lookup"><span data-stu-id="b6451-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="b6451-184">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b6451-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="b6451-185">Installare il pacchetto di hello per sfumatura HUZZAH ESP8266 in hello Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="b6451-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="b6451-186">Aprire hello cartella dove si trova l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="b6451-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="b6451-187">Aprire il file di app.ino hello nella cartella dell'applicazione hello in hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="b6451-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Aprire l'applicazione di esempio hello in Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="b6451-189">In hello Arduino IDE, fare clic su **File** > **preferenze**.</span><span class="sxs-lookup"><span data-stu-id="b6451-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="b6451-190">In hello **preferenze** finestra di dialogo fare clic su hello icona Avanti toohello **URL di gestione aggiuntivi lavagne** casella.</span><span class="sxs-lookup"><span data-stu-id="b6451-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="b6451-191">Nella finestra popup hello immettere hello URL seguente e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6451-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url del pacchetto nell'IDE Arduino tooa punto](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="b6451-193">In hello **preferenza** la finestra di dialogo, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6451-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="b6451-194">Fare clic su **Strumenti** > **Bacheca** > **Boards Manager** (Gestione bacheche) e quindi cercare esp8266.</span><span class="sxs-lookup"><span data-stu-id="b6451-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="b6451-195">Boards Manager indica che è installata ESP8266 con una versione 2.2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b6451-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![installazione del pacchetto esp8266 Hello](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="b6451-197">Fare clic su **Strumenti** > **Bacheca** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="b6451-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="b6451-198">Installare le librerie necessarie</span><span class="sxs-lookup"><span data-stu-id="b6451-198">Install necessary libraries</span></span>

1. <span data-ttu-id="b6451-199">In hello Arduino IDE, fare clic su **Sketch** > **libreria includono** > **Gestisci raccolte**.</span><span class="sxs-lookup"><span data-stu-id="b6451-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="b6451-200">Ricerca di hello seguente i nomi delle librerie uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="b6451-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="b6451-201">Per ogni libreria trovata fare clic su **Install** (Installa).</span><span class="sxs-lookup"><span data-stu-id="b6451-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="b6451-202">Non si dispone di un sensore DHT22 reale?</span><span class="sxs-lookup"><span data-stu-id="b6451-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="b6451-203">applicazione di esempio Hello possibile simulare la temperatura e umidità dati nel caso in cui non si dispone di un sensore DHT22 reale.</span><span class="sxs-lookup"><span data-stu-id="b6451-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="b6451-204">tooset dei dati di toouse simulate dell'applicazione di esempio hello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="b6451-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="b6451-205">Aprire hello `config.h` file hello `app` cartella.</span><span class="sxs-lookup"><span data-stu-id="b6451-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="b6451-206">Individuare hello successiva riga di codice e modificare il valore di hello da `false` troppo`true`:</span><span class="sxs-lookup"><span data-stu-id="b6451-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurare i dati simulati toouse dell'applicazione di esempio hello](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="b6451-208">Salvare file con estensione hello `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="b6451-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="b6451-209">Distribuire tooFeather applicazione di esempio hello HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b6451-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="b6451-210">In hello Arduino IDE, fare clic su **strumento** > **porta**, quindi fare clic su porta seriale hello per sfumatura HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b6451-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="b6451-211">Fare clic su **Sketch** > **caricare** toobuild e distribuire tooFeather applicazione di esempio hello HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b6451-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="b6451-212">Immettere le credenziali</span><span class="sxs-lookup"><span data-stu-id="b6451-212">Enter your credentials</span></span>

<span data-ttu-id="b6451-213">Dopo aver completato il caricamento di hello, seguire questi passaggi tooenter le credenziali:</span><span class="sxs-lookup"><span data-stu-id="b6451-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="b6451-214">In hello Arduino IDE, fare clic su **strumenti** > **monitoraggio seriale**.</span><span class="sxs-lookup"><span data-stu-id="b6451-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="b6451-215">Nella finestra di monitoraggio seriale hello, noti elenchi a discesa hello due nell'angolo inferiore destro hello.</span><span class="sxs-lookup"><span data-stu-id="b6451-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="b6451-216">Selezionare **alcuna terminazione di riga** per l'elenco a discesa sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="b6451-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="b6451-217">Selezionare **115200 baud** per l'elenco a discesa a destra hello.</span><span class="sxs-lookup"><span data-stu-id="b6451-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="b6451-218">Nella casella di input hello nella parte superiore di hello della finestra di monitoraggio seriale hello, immettere le seguenti informazioni se viene chiesto tooprovide hello, quindi fare clic su **inviare**.</span><span class="sxs-lookup"><span data-stu-id="b6451-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="b6451-219">Wi-Fi SSID</span><span class="sxs-lookup"><span data-stu-id="b6451-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="b6451-220">Password Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="b6451-220">Wi-Fi password</span></span>
   * <span data-ttu-id="b6451-221">Stringa di connessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="b6451-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="b6451-222">informazioni sulle credenziali Hello viene archiviati in hello EEPROM di sfumatura HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b6451-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b6451-223">Se si fa clic su pulsante Reimposta hello in hello Lavagna ESP8266 HUZZAH sfumatura, applicazione di esempio hello chiede se si desiderano informazioni hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="b6451-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="b6451-224">Immettere `Y` informazioni hello toohave cancellate.</span><span class="sxs-lookup"><span data-stu-id="b6451-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="b6451-225">Verrà chiesto informazioni hello tooprovide una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="b6451-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="b6451-226">Verificare l'applicazione di esempio hello venga eseguita correttamente</span><span class="sxs-lookup"><span data-stu-id="b6451-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="b6451-227">Se viene visualizzato seguito hello output della finestra di monitoraggio seriale hello e hello lampeggiante LED su ESP8266 HUZZAH sfumatura, applicazione di esempio hello venga eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="b6451-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Output finale nell'IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="b6451-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6451-229">Next steps</span></span>

<span data-ttu-id="b6451-230">Aver connesso un hub IoT di sfumatura HUZZAH ESP8266 tooyour e inviato hello acquisito sensore dati tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b6451-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

