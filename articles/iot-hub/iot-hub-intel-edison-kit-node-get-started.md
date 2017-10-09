---
title: aaaIntel Edison toocloud (Node.js) - connessione Edison Intel tooAzure IoT Hub | Documenti Microsoft
description: Informazioni su come toosetup e connettersi Edison Intel tooAzure IoT Hub per la piattaforma cloud di Azure Edison Intel toosend dati toohello in questa esercitazione.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel hub iot edison, intel edison invia dati toocloud, intel toocloud edison
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a><span data-ttu-id="24ea4-104">Connettersi tooAzure Edison Intel IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="24ea4-104">Connect Intel Edison tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="24ea4-105">In questa esercitazione, è necessario innanzitutto hello nozioni fondamentali sulle operazioni con Intel Edison di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="24ea4-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="24ea4-106">Si apprenderà quindi la modalità di connessione cloud toohello dispositivi utilizzando tooseamlessly [IoT Hub Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="24ea4-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="24ea4-107">Se non si ha ancora un kit,</span><span class="sxs-lookup"><span data-stu-id="24ea4-107">Don't have a kit yet?</span></span> <span data-ttu-id="24ea4-108">iniziare da [qui](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="24ea4-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="24ea4-109">Operazioni da fare</span><span class="sxs-lookup"><span data-stu-id="24ea4-109">What you do</span></span>

* <span data-ttu-id="24ea4-110">Configurare i moduli Intel Edison e Grove.</span><span class="sxs-lookup"><span data-stu-id="24ea4-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="24ea4-111">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="24ea4-111">Create an IoT hub.</span></span>
* <span data-ttu-id="24ea4-112">Registrare un dispositivo per Edison nel proprio hub IoT.</span><span class="sxs-lookup"><span data-stu-id="24ea4-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="24ea4-113">Eseguire un'applicazione di esempio nell'hub IoT di Edison toosend sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="24ea4-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="24ea4-114">Connettersi Edison Intel tooan l'hub IoT creati.</span><span class="sxs-lookup"><span data-stu-id="24ea4-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="24ea4-115">Quindi eseguire un'applicazione di esempio in Edison toocollect temperatura e umidità dati da un sensore di temperatura Groove.</span><span class="sxs-lookup"><span data-stu-id="24ea4-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="24ea4-116">Infine, si invia l'hub IoT hello sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="24ea4-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="24ea4-117">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="24ea4-117">What you learn</span></span>

* <span data-ttu-id="24ea4-118">Come toocreate un hub IoT di Azure e ottenere la stringa di connessione nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24ea4-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="24ea4-119">Come tooconnect Edison con un sensore di temperatura Groove.</span><span class="sxs-lookup"><span data-stu-id="24ea4-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="24ea4-120">Come dati del sensore toocollect mediante l'esecuzione di un'applicazione di esempio su Edison.</span><span class="sxs-lookup"><span data-stu-id="24ea4-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="24ea4-121">Come l'hub IoT toosend sensore dati tooyour.</span><span class="sxs-lookup"><span data-stu-id="24ea4-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="24ea4-122">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="24ea4-122">What you need</span></span>

![Elementi necessari](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="24ea4-124">Hello Lavagna Edison Intel</span><span class="sxs-lookup"><span data-stu-id="24ea4-124">hello Intel Edison board</span></span>
* <span data-ttu-id="24ea4-125">Scheda di espansione Arduino</span><span class="sxs-lookup"><span data-stu-id="24ea4-125">Arduino expansion board</span></span>
* <span data-ttu-id="24ea4-126">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="24ea4-126">An active Azure subscription.</span></span> <span data-ttu-id="24ea4-127">Se non si ha un account Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="24ea4-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="24ea4-128">Un Mac o PC che esegue Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="24ea4-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="24ea4-129">Una connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="24ea4-129">An Internet connection.</span></span>
* <span data-ttu-id="24ea4-130">Un cavo USB A di tooType Micro B</span><span class="sxs-lookup"><span data-stu-id="24ea4-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="24ea4-131">Alimentatore in corrente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="24ea4-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="24ea4-132">I valori nominali dell'alimentatore devono essere i seguenti:</span><span class="sxs-lookup"><span data-stu-id="24ea4-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="24ea4-133">7-15 V CC</span><span class="sxs-lookup"><span data-stu-id="24ea4-133">7-15V DC</span></span>
  - <span data-ttu-id="24ea4-134">Almeno 1500 mA</span><span class="sxs-lookup"><span data-stu-id="24ea4-134">At least 1500mA</span></span>
  - <span data-ttu-id="24ea4-135">pin center/interna Hello devono essere polo positivo hello di alimentatore hello</span><span class="sxs-lookup"><span data-stu-id="24ea4-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="24ea4-136">Hello seguenti elementi è facoltativo:</span><span class="sxs-lookup"><span data-stu-id="24ea4-136">hello following items are optional:</span></span>

* <span data-ttu-id="24ea4-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="24ea4-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="24ea4-138">Sensore temperatura Grove</span><span class="sxs-lookup"><span data-stu-id="24ea4-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="24ea4-139">Cavo Grove</span><span class="sxs-lookup"><span data-stu-id="24ea4-139">Grove Cable</span></span>
* <span data-ttu-id="24ea4-140">Le barre dello spaziatore né viti incluse nel pacchetto di hello, tra cui scheda di espansione toohello modulo hello toofasten due viti e quattro set di viti e spaziatore plastica.</span><span class="sxs-lookup"><span data-stu-id="24ea4-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="24ea4-141">Poiché il supporto di esempio di codice hello simulati i dati del sensore, questi elementi sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="24ea4-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="24ea4-142">Configurare Intel Edison</span><span class="sxs-lookup"><span data-stu-id="24ea4-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="24ea4-143">Assemblare la scheda</span><span class="sxs-lookup"><span data-stu-id="24ea4-143">Assemble your board</span></span>

<span data-ttu-id="24ea4-144">In questa sezione contiene passaggi tooattach la scheda di espansione Intel® Edison tooyour modulo.</span><span class="sxs-lookup"><span data-stu-id="24ea4-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="24ea4-145">Modulo di Intel® Edison hello sul posto all'interno di struttura hello bianca sulla Lavagna espansione, allineare fori hello sul modulo hello con viti hello nella scheda di espansione hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="24ea4-146">Premere sul modulo hello subito dopo le parole hello `What will you make?` fino a quando non si ritiene un gioco da ragazzi.</span><span class="sxs-lookup"><span data-stu-id="24ea4-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![assemblare la scheda 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="24ea4-148">Utilizzare una scheda di espansione di hello due dadi esadecimale (inclusi nel pacchetto hello) toosecure hello modulo toohello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![assemblare la scheda 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="24ea4-150">Inserire una vite in uno dei quattro fori angolo hello nella scheda di espansione hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="24ea4-151">Torsione e stringere uno spaziatore plastica di hello bianco su vite hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![assemblare la scheda 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="24ea4-153">Ripetere l'operazione per hello spaziatore altri tre angolo.</span><span class="sxs-lookup"><span data-stu-id="24ea4-153">Repeat for hello other three corner spacers.</span></span>

   ![assemblare la scheda 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="24ea4-155">A questo punto la scheda è assemblata.</span><span class="sxs-lookup"><span data-stu-id="24ea4-155">Now your board is assembled.</span></span>

   ![scheda assemblata](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="24ea4-157">Connettere hello dello scudo di Base di Groove e sensore di temperatura hello</span><span class="sxs-lookup"><span data-stu-id="24ea4-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="24ea4-158">Inserire hello dello scudo di Base di Groove nella Lavagna tooyour.</span><span class="sxs-lookup"><span data-stu-id="24ea4-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="24ea4-159">e assicurarsi che sia inserito correttamente nella scheda.</span><span class="sxs-lookup"><span data-stu-id="24ea4-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="24ea4-161">Sensore di temperatura utilizzare Groove cavo tooconnect Groove su hello dello scudo di Base di Groove **A0** porta.</span><span class="sxs-lookup"><span data-stu-id="24ea4-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Connettersi sensore tootemperature](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison e connessione al sensore](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="24ea4-164">Il sensore è pronto.</span><span class="sxs-lookup"><span data-stu-id="24ea4-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="24ea4-165">Alimentare Edison</span><span class="sxs-lookup"><span data-stu-id="24ea4-165">Power up Edison</span></span>

1. <span data-ttu-id="24ea4-166">Plug-in dell'alimentatore hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-166">Plug in hello power supply.</span></span>

   ![Collegare l'alimentatore](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="24ea4-168">Un LED verde (nella scheda di espansione Arduino * hello con etichettato DS1) dovrebbe accendersi e rimanere acceso.</span><span class="sxs-lookup"><span data-stu-id="24ea4-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="24ea4-169">Attendere un minuto per hello Lavagna toofinish l'avvio.</span><span class="sxs-lookup"><span data-stu-id="24ea4-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="24ea4-170">Se non si dispone di un alimentatore controller di dominio, è comunque possibile Lavagna hello power attraverso una porta USB.</span><span class="sxs-lookup"><span data-stu-id="24ea4-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="24ea4-171">Per informazioni dettagliate, vedere la sezione `Connect Edison tooyour computer`.</span><span class="sxs-lookup"><span data-stu-id="24ea4-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="24ea4-172">Questo modo di alimentare la scheda può causarne un comportamento non prevedibile, soprattutto quando si usa il Wi-Fi o si comandano motori.</span><span class="sxs-lookup"><span data-stu-id="24ea4-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="24ea4-173">Connettere computer tooyour Edison</span><span class="sxs-lookup"><span data-stu-id="24ea4-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="24ea4-174">Attiva o disattiva verso il basso microinterruttore hello verso hello due micro porte USB, in modo che Edison è in modalità di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24ea4-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="24ea4-175">Per informazioni sulle differenze tra la modalità dispositivo e la modalità host, vedere [qui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="24ea4-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Attivare o disattivare verso il basso microinterruttore hello](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="24ea4-177">Collegare il cavo USB micro di hello superiore porta USB micro hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Porta micro-USB superiore](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="24ea4-179">Plug hello altra estremità del cavo USB nel computer.</span><span class="sxs-lookup"><span data-stu-id="24ea4-179">Plug hello other end of USB cable into your computer.</span></span>

   ![USB computer](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="24ea4-181">La scheda è completamente inizializzata quando il computer consente di montare una nuova unità (ad esempio inserendo una scheda SD).</span><span class="sxs-lookup"><span data-stu-id="24ea4-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="24ea4-182">Scaricare ed eseguire lo strumento di configurazione hello</span><span class="sxs-lookup"><span data-stu-id="24ea4-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="24ea4-183">Strumento di configurazione più recente di hello da ottenere [questo collegamento](https://software.intel.com/en-us/iot/hardware/edison/downloads) sotto hello `Installers` intestazione.</span><span class="sxs-lookup"><span data-stu-id="24ea4-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="24ea4-184">Esecuzione dello strumento hello e seguire il visualizzate le istruzioni, fare clic su Avanti dove necessario</span><span class="sxs-lookup"><span data-stu-id="24ea4-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="24ea4-185">Eseguire il flashing del firmware</span><span class="sxs-lookup"><span data-stu-id="24ea4-185">Flash firmware</span></span>
1. <span data-ttu-id="24ea4-186">In hello `Set up options` pagina, fare clic su `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="24ea4-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="24ea4-187">Selezionare tooflash immagine hello nella scheda effettuando una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="24ea4-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="24ea4-188">toodownload e flash la Lavagna con hello più recente del firmware immagine disponibile da Intel, selezionare `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="24ea4-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="24ea4-189">Selezionare la scheda con un'immagine è già stato salvato nel computer in uso, tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="24ea4-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="24ea4-190">Sfoglia tooand hello selezionare l'immagine tooflash tooyour Lavagna.</span><span class="sxs-lookup"><span data-stu-id="24ea4-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="24ea4-191">strumento di configurazione Hello tenterà tooflash la Lavagna.</span><span class="sxs-lookup"><span data-stu-id="24ea4-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="24ea4-192">processo lampeggiante Hello potrebbe richiedere too10 minuti.</span><span class="sxs-lookup"><span data-stu-id="24ea4-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="24ea4-193">Impostare la password</span><span class="sxs-lookup"><span data-stu-id="24ea4-193">Set password</span></span>
1. <span data-ttu-id="24ea4-194">In hello `Set up options` pagina, fare clic su `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="24ea4-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="24ea4-195">Per la scheda Intel® Edison è possibile impostare un nome personalizzato.</span><span class="sxs-lookup"><span data-stu-id="24ea4-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="24ea4-196">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="24ea4-196">This is optional.</span></span>
3. <span data-ttu-id="24ea4-197">Digitare una password per la scheda e quindi fare clic su `Set password`.</span><span class="sxs-lookup"><span data-stu-id="24ea4-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="24ea4-198">Contrassegnare come inattivo password hello, che viene utilizzata in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="24ea4-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="24ea4-199">Connettere il Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="24ea4-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="24ea4-200">In hello `Set up options` pagina, fare clic su `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="24ea4-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="24ea4-201">Attesa di minuto tooone come l'analisi del computer per reti Wi-Fi disponibili.</span><span class="sxs-lookup"><span data-stu-id="24ea4-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="24ea4-202">Da hello `Detected Networks` elenco a discesa, selezionare la rete.</span><span class="sxs-lookup"><span data-stu-id="24ea4-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="24ea4-203">Da hello `Security` elenco a discesa, il tipo di sicurezza della rete selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="24ea4-204">Specificare le informazioni di accesso e la password, quindi fare clic su `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="24ea4-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="24ea4-205">Contrassegnare come inattivo hello indirizzo IP, che viene utilizzato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="24ea4-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="24ea4-206">Assicurarsi che Edison sia connesso toohello stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="24ea4-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="24ea4-207">Il computer si connette tooyour Edison utilizzando l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Connettersi sensore tootemperature](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="24ea4-209">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="24ea4-209">Congratulations!</span></span> <span data-ttu-id="24ea4-210">Edison è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="24ea4-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="24ea4-211">Eseguire un'applicazione di esempio in Intel Edison</span><span class="sxs-lookup"><span data-stu-id="24ea4-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="24ea4-212">Preparare hello dispositivo IoT di Azure SDK</span><span class="sxs-lookup"><span data-stu-id="24ea4-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="24ea4-213">Utilizzare uno dei seguenti client SSH dagli tooyour di tooconnect computer host Intel Edison hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="24ea4-214">indirizzo IP Hello è dallo strumento di configurazione hello e password di hello è hello uno impostate in questo strumento.</span><span class="sxs-lookup"><span data-stu-id="24ea4-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="24ea4-215">[PuTTY](http://www.putty.org/) per Windows.</span><span class="sxs-lookup"><span data-stu-id="24ea4-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="24ea4-216">client SSH incorporato Hello in Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="24ea4-216">hello built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="24ea4-217">Clone hello esempio app tooyour dispositivo client.</span><span class="sxs-lookup"><span data-stu-id="24ea4-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="24ea4-218">Quindi passare tutti i pacchetti hello toorun cartella repository di toohello tooinstall comando seguente, potrebbe richiedere serval minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="24ea4-218">Then navigate toohello repo folder toorun hello following command tooinstall all packages, it may take serval minutes toocomplete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a><span data-ttu-id="24ea4-219">Configurare ed eseguire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="24ea4-219">Configure and run hello sample application</span></span>

1. <span data-ttu-id="24ea4-220">Aprire il file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="24ea4-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![File di configurazione](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="24ea4-222">Questo file contiene due macro configurabili.</span><span class="sxs-lookup"><span data-stu-id="24ea4-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="24ea4-223">Hello prima uno è `INTERVAL`, che definisce l'intervallo di tempo hello tra due messaggi che inviano toocloud.</span><span class="sxs-lookup"><span data-stu-id="24ea4-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="24ea4-224">Hello secondo `simulatedData`, ovvero un valore booleano per se toouse sensore dati simulati o non.</span><span class="sxs-lookup"><span data-stu-id="24ea4-224">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="24ea4-225">Se si **non dispone di sensore hello**, hello impostare `simulatedData` valore troppo`true` applicazione di esempio hello toomake creare e utilizzare dati del sensore simulato.</span><span class="sxs-lookup"><span data-stu-id="24ea4-225">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="24ea4-226">Salvare e uscire premendo CTRL-O > Invio > CTRL-X.</span><span class="sxs-lookup"><span data-stu-id="24ea4-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="24ea4-227">Eseguire l'applicazione di esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="24ea4-227">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="24ea4-228">Assicurarsi copiare e incollare stringa di connessione del dispositivo hello in virgolette hello.</span><span class="sxs-lookup"><span data-stu-id="24ea4-228">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="24ea4-229">Verrà visualizzato l'output seguente hello che mostra hello sensore dati e hello i messaggi vengono inviati tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="24ea4-229">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Output - sensore dati vengono inviati da Intel Edison tooyour hub IoT](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="24ea4-231">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="24ea4-231">Next steps</span></span>

<span data-ttu-id="24ea4-232">È stato eseguito dati sensore toocollect di applicazione di esempio e inviarlo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="24ea4-232">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
