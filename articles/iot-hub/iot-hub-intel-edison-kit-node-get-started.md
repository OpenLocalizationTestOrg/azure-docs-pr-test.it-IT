---
title: Da Intel Edison al cloud (Node.js) - Connettere Intel Edison all'Hub IoT di Azure | Microsoft Docs
description: "Informazioni su come configurare e connettere Intel Edison all'hub IoT di Azure perché Intel Edison invii i dati alla piattaforma cloud di Azure in questa esercitazione."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: azure iot intel edison, intel edison hub iot, intel edison invio dati al cloud, da intel edison al cloud
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5a31efba704045196b5563f7bc467c773bea7805
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-nodejs"></a><span data-ttu-id="ef217-104">Connettere Intel Edison all'Hub IoT di Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="ef217-104">Connect Intel Edison to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="ef217-105">Questa esercitazione illustra le nozioni base per l'uso di Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="ef217-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="ef217-106">Viene poi illustrato come connettere i dispositivi al cloud usando l'[hub IoT di Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="ef217-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="ef217-107">Se non si ha ancora un kit,</span><span class="sxs-lookup"><span data-stu-id="ef217-107">Don't have a kit yet?</span></span> <span data-ttu-id="ef217-108">iniziare da [qui](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="ef217-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="ef217-109">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="ef217-109">What you do</span></span>

* <span data-ttu-id="ef217-110">Configurare i moduli Intel Edison e Grove.</span><span class="sxs-lookup"><span data-stu-id="ef217-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="ef217-111">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef217-111">Create an IoT hub.</span></span>
* <span data-ttu-id="ef217-112">Registrare un dispositivo per Edison nel proprio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef217-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="ef217-113">Eseguire un'applicazione di esempio in Edison per inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef217-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="ef217-114">Connettere Intel Edison a un hub IoT creato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ef217-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="ef217-115">Eseguire un'applicazione di esempio in Edison per raccogliere dati di temperatura e umidità da un sensore temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="ef217-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="ef217-116">Infine inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef217-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="ef217-117">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ef217-117">What you learn</span></span>

* <span data-ttu-id="ef217-118">Come creare un hub IoT di Azure e ottenere la stringa di connessione del nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ef217-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="ef217-119">Come connettere Edison a un sensore temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="ef217-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="ef217-120">Come raccogliere i dati del sensore eseguendo un'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="ef217-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="ef217-121">Come inviare i dati del sensore all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef217-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ef217-122">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="ef217-122">What you need</span></span>

![Elementi necessari](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="ef217-124">Scheda Intel Edison</span><span class="sxs-lookup"><span data-stu-id="ef217-124">The Intel Edison board</span></span>
* <span data-ttu-id="ef217-125">Scheda di espansione Arduino</span><span class="sxs-lookup"><span data-stu-id="ef217-125">Arduino expansion board</span></span>
* <span data-ttu-id="ef217-126">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="ef217-126">An active Azure subscription.</span></span> <span data-ttu-id="ef217-127">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="ef217-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="ef217-128">Un Mac o PC che esegue Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="ef217-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="ef217-129">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="ef217-129">An Internet connection.</span></span>
* <span data-ttu-id="ef217-130">Cavo USB Micro B/Tipo A</span><span class="sxs-lookup"><span data-stu-id="ef217-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="ef217-131">Alimentatore in corrente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="ef217-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="ef217-132">I valori nominali dell'alimentatore devono essere i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef217-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="ef217-133">7-15 V CC</span><span class="sxs-lookup"><span data-stu-id="ef217-133">7-15V DC</span></span>
  - <span data-ttu-id="ef217-134">Almeno 1500 mA</span><span class="sxs-lookup"><span data-stu-id="ef217-134">At least 1500mA</span></span>
  - <span data-ttu-id="ef217-135">Il pin centrale deve essere il polo positivo dell'alimentatore</span><span class="sxs-lookup"><span data-stu-id="ef217-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="ef217-136">Gli elementi seguenti sono opzionali:</span><span class="sxs-lookup"><span data-stu-id="ef217-136">The following items are optional:</span></span>

* <span data-ttu-id="ef217-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="ef217-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="ef217-138">Sensore temperatura Grove</span><span class="sxs-lookup"><span data-stu-id="ef217-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="ef217-139">Cavo Grove</span><span class="sxs-lookup"><span data-stu-id="ef217-139">Grove Cable</span></span>
* <span data-ttu-id="ef217-140">Elementi distanziali o viti contenuti nel pacchetto, inclusi quattro set di viti ed elementi distanziali in plastica e due viti per fissare il modulo alla scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="ef217-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="ef217-141">Questi elementi sono opzionali, poiché l'esempio di codice supporta i dati del sensore simulato.</span><span class="sxs-lookup"><span data-stu-id="ef217-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="ef217-142">Configurare Intel Edison</span><span class="sxs-lookup"><span data-stu-id="ef217-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="ef217-143">Assemblare la scheda</span><span class="sxs-lookup"><span data-stu-id="ef217-143">Assemble your board</span></span>

<span data-ttu-id="ef217-144">Questa sezione contiene i passaggi per connettere il modulo Intel® Edison alla scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="ef217-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="ef217-145">Posizionare il modulo Intel® Edison all'interno del bordo bianco della scheda di espansione, allineando i fori del modulo con le viti della scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="ef217-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="ef217-146">Premere verso il basso il modulo sotto le parole `What will you make?` fino a quando non si sente uno scatto.</span><span class="sxs-lookup"><span data-stu-id="ef217-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![assemblare la scheda 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="ef217-148">Usare i due dadi esagonali (inclusi nel pacchetto) per fissare il modulo alla scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="ef217-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![assemblare la scheda 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="ef217-150">Inserire una vite in uno dei quattro fori negli angoli della scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="ef217-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="ef217-151">Avvitare e fissare uno dei due elementi distanziali in plastica alla vite.</span><span class="sxs-lookup"><span data-stu-id="ef217-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![assemblare la scheda 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="ef217-153">Ripetere l'operazione per gli altri tre elementi distanziali angolari.</span><span class="sxs-lookup"><span data-stu-id="ef217-153">Repeat for the other three corner spacers.</span></span>

   ![assemblare la scheda 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="ef217-155">A questo punto la scheda è assemblata.</span><span class="sxs-lookup"><span data-stu-id="ef217-155">Now your board is assembled.</span></span>

   ![scheda assemblata](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="ef217-157">Connettere Grove Base Shield e il sensore temperatura</span><span class="sxs-lookup"><span data-stu-id="ef217-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="ef217-158">Posizionare Grove Base Shield sulla scheda</span><span class="sxs-lookup"><span data-stu-id="ef217-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="ef217-159">e assicurarsi che sia inserito correttamente nella scheda.</span><span class="sxs-lookup"><span data-stu-id="ef217-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="ef217-161">Usare il cavo Grove Cable per connettere il sensore temperatura Grove alla porta **A0** di Grove Base Shield.</span><span class="sxs-lookup"><span data-stu-id="ef217-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Connettersi al sensore temperatura](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison e connessione al sensore](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="ef217-164">Il sensore è pronto.</span><span class="sxs-lookup"><span data-stu-id="ef217-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="ef217-165">Alimentare Edison</span><span class="sxs-lookup"><span data-stu-id="ef217-165">Power up Edison</span></span>

1. <span data-ttu-id="ef217-166">Collegare l'alimentatore.</span><span class="sxs-lookup"><span data-stu-id="ef217-166">Plug in the power supply.</span></span>

   ![Collegare l'alimentatore](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="ef217-168">Un LED verde (con etichetta DS1 sulla scheda di espansione Arduino*) dovrebbe accendersi e rimanere acceso.</span><span class="sxs-lookup"><span data-stu-id="ef217-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="ef217-169">Attendere un minuto per il completamento dell'avvio della scheda.</span><span class="sxs-lookup"><span data-stu-id="ef217-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef217-170">Se non si dispone di un alimentatore CC, è comunque possibile alimentare la scheda tramite una porta USB.</span><span class="sxs-lookup"><span data-stu-id="ef217-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="ef217-171">Per informazioni dettagliate, vedere la sezione `Connect Edison to your computer`.</span><span class="sxs-lookup"><span data-stu-id="ef217-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="ef217-172">Questo modo di alimentare la scheda può causarne un comportamento non prevedibile, soprattutto quando si usa il Wi-Fi o si comandano motori.</span><span class="sxs-lookup"><span data-stu-id="ef217-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="ef217-173">Connettere Edison al computer</span><span class="sxs-lookup"><span data-stu-id="ef217-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="ef217-174">Spostare i microinterruttori verso le due porte micro-USB in modo che Edison si trovi in modalità dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ef217-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="ef217-175">Per informazioni sulle differenze tra la modalità dispositivo e la modalità host, vedere [qui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="ef217-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Spostare verso il basso il microinterruttore](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="ef217-177">Collegare il cavo micro-USB alla porta micro-USB superiore.</span><span class="sxs-lookup"><span data-stu-id="ef217-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Porta micro-USB superiore](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="ef217-179">Collegare l'altra estremità del cavo USB al computer.</span><span class="sxs-lookup"><span data-stu-id="ef217-179">Plug the other end of USB cable into your computer.</span></span>

   ![USB computer](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="ef217-181">La scheda è completamente inizializzata quando il computer consente di montare una nuova unità (ad esempio inserendo una scheda SD).</span><span class="sxs-lookup"><span data-stu-id="ef217-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="ef217-182">Scaricare ed eseguire lo strumento di configurazione</span><span class="sxs-lookup"><span data-stu-id="ef217-182">Download and run the configuration tool</span></span>
<span data-ttu-id="ef217-183">Scaricare lo strumento di configurazione più recente presente in [questo collegamento](https://software.intel.com/en-us/iot/hardware/edison/downloads) sotto l'intestazione `Installers`.</span><span class="sxs-lookup"><span data-stu-id="ef217-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="ef217-184">Eseguire lo strumento e attenersi alle istruzioni visualizzate. Fare clic su Avanti quando necessario.</span><span class="sxs-lookup"><span data-stu-id="ef217-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="ef217-185">Eseguire il flashing del firmware</span><span class="sxs-lookup"><span data-stu-id="ef217-185">Flash firmware</span></span>
1. <span data-ttu-id="ef217-186">Nella pagina `Set up options` fare clic su `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="ef217-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="ef217-187">Selezionare l'immagine per eseguire il flashing sulla scheda tramite una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef217-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="ef217-188">Per scaricare ed eseguire il flashing della scheda con l'immagine del firmware più recente disponibile in Intel, selezionare `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="ef217-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="ef217-189">Per eseguire il flashing della scheda con un'immagine già salvata nel computer, selezionare `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="ef217-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="ef217-190">Individuare e selezionare l'immagine di cui si desidera eseguire il flashing nella scheda.</span><span class="sxs-lookup"><span data-stu-id="ef217-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="ef217-191">Lo strumento di installazione tenterà di eseguire il flashing della scheda.</span><span class="sxs-lookup"><span data-stu-id="ef217-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="ef217-192">L'intero processo di esecuzione del flashing può richiedere fino a 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="ef217-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="ef217-193">Impostare la password</span><span class="sxs-lookup"><span data-stu-id="ef217-193">Set password</span></span>
1. <span data-ttu-id="ef217-194">Nella pagina `Set up options` fare clic su `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="ef217-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="ef217-195">Per la scheda Intel® Edison è possibile impostare un nome personalizzato.</span><span class="sxs-lookup"><span data-stu-id="ef217-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="ef217-196">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ef217-196">This is optional.</span></span>
3. <span data-ttu-id="ef217-197">Digitare una password per la scheda e quindi fare clic su `Set password`.</span><span class="sxs-lookup"><span data-stu-id="ef217-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="ef217-198">Annotare la password per usarla in seguito.</span><span class="sxs-lookup"><span data-stu-id="ef217-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="ef217-199">Connettere il Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="ef217-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="ef217-200">Nella pagina `Set up options` fare clic su `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="ef217-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="ef217-201">Attendere fino a un minuto per la ricerca delle reti Wi-Fi disponibili.</span><span class="sxs-lookup"><span data-stu-id="ef217-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="ef217-202">Nell'elenco a discesa `Detected Networks` selezionare la rete.</span><span class="sxs-lookup"><span data-stu-id="ef217-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="ef217-203">Nell'elenco a discesa `Security` selezionare il tipo di sicurezza della rete.</span><span class="sxs-lookup"><span data-stu-id="ef217-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="ef217-204">Specificare le informazioni di accesso e la password, quindi fare clic su `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="ef217-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="ef217-205">Annotare l'indirizzo IP per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="ef217-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="ef217-206">Verificare che Edison sia connesso alla stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="ef217-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="ef217-207">Il computer si connette a Edison tramite l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="ef217-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Connettersi al sensore temperatura](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="ef217-209">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="ef217-209">Congratulations!</span></span> <span data-ttu-id="ef217-210">Edison è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="ef217-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="ef217-211">Eseguire un'applicazione di esempio in Intel Edison</span><span class="sxs-lookup"><span data-stu-id="ef217-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="ef217-212">Preparare Azure IoT SDK per dispositivi</span><span class="sxs-lookup"><span data-stu-id="ef217-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="ef217-213">Per connettersi a Intel Edison, usare uno dei client SSH seguenti dal computer host.</span><span class="sxs-lookup"><span data-stu-id="ef217-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="ef217-214">L'indirizzo IP è relativo allo strumento di configurazione e la password corrisponde a quella impostata nello strumento.</span><span class="sxs-lookup"><span data-stu-id="ef217-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="ef217-215">[PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="ef217-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="ef217-216">Il client SSH incorporato in Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="ef217-216">The built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="ef217-217">Clonare l'app client di esempio nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ef217-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="ef217-218">Passare quindi alla cartella del repository per eseguire il comando seguente, in modo da installare tutti i pacchetti. Il completamento dell'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="ef217-218">Then navigate to the repo folder to run the following command to install all packages, it may take serval minutes to complete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-the-sample-application"></a><span data-ttu-id="ef217-219">Configurare ed eseguire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="ef217-219">Configure and run the sample application</span></span>

1. <span data-ttu-id="ef217-220">Aprire il file di configurazione eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef217-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![File di configurazione](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="ef217-222">Questo file contiene due macro configurabili.</span><span class="sxs-lookup"><span data-stu-id="ef217-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="ef217-223">La prima è `INTERVAL`, che definisce l'intervallo di tempo tra due messaggi inviati al cloud.</span><span class="sxs-lookup"><span data-stu-id="ef217-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="ef217-224">La seconda è `simulatedData`, ossia un valore booleano che indica se usare o no i dati del sensore simulato.</span><span class="sxs-lookup"><span data-stu-id="ef217-224">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="ef217-225">Se **non si dispone del sensore**, impostare il valore `simulatedData` su `true` per permettere all'applicazione di esempio di creare e usare i dati del sensore simulati.</span><span class="sxs-lookup"><span data-stu-id="ef217-225">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="ef217-226">Salvare e uscire premendo CTRL-O > Invio > CTRL-X.</span><span class="sxs-lookup"><span data-stu-id="ef217-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="ef217-227">Eseguire l'applicazione di esempio tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ef217-227">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="ef217-228">Assicurarsi di copiare e incollare la stringa di connessione del dispositivo tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="ef217-228">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="ef217-229">Dovrebbe essere visibile l'output seguente che mostra i dati del sensore e i messaggi inviati all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef217-229">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - dati del sensore inviati da Intel Edison all'hub IoT](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="ef217-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef217-231">Next steps</span></span>

<span data-ttu-id="ef217-232">È stata eseguita un'applicazione di esempio per raccogliere i dati del sensore da inviare all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ef217-232">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
