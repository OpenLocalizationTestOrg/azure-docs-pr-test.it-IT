---
title: 'Connettere Intel Edison (Node) ad Azure IoT: lezione 1: Configurare il dispositivo | Documentazione Microsoft'
description: Configurare Intel Edison per il primo uso.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: configurazione arduino, connessione di arduino al pc, configurazione di arduino, scheda arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 87bf3a917af096e43a43a2143afa4bf43a72d7fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="69cb9-104">Configurare Intel Edison</span><span class="sxs-lookup"><span data-stu-id="69cb9-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="69cb9-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="69cb9-105">What you will do</span></span>
<span data-ttu-id="69cb9-106">Configurare Intel Edison per il primo utilizzo assemblando la scheda, fornendo l'alimentazione e installando lo strumento di configurazione nel sistema operativo desktop per eseguire il flashing del firmware Edison, impostarne la password e connetterlo al Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="69cb9-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="69cb9-107">In caso di problemi, cercare le soluzioni nella [pagina sulla risoluzione dei problemi][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="69cb9-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="69cb9-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="69cb9-108">What you will learn</span></span>
<span data-ttu-id="69cb9-109">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="69cb9-109">In this article, you will learn:</span></span>

* <span data-ttu-id="69cb9-110">Come assemblare la scheda Edison e fornire l'alimentazione.</span><span class="sxs-lookup"><span data-stu-id="69cb9-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="69cb9-111">Come eseguire il flashing del firmware di Edison, impostare la password e connettere il Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="69cb9-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="69cb9-112">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="69cb9-112">What you need</span></span>
<span data-ttu-id="69cb9-113">Per completare questa operazione, è necessario disporre dei componenti seguenti dello starter kit di Intel Edison:</span><span class="sxs-lookup"><span data-stu-id="69cb9-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="69cb9-114">Modulo Intel® Edison</span><span class="sxs-lookup"><span data-stu-id="69cb9-114">Intel® Edison module</span></span>
* <span data-ttu-id="69cb9-115">Scheda di espansione Arduino</span><span class="sxs-lookup"><span data-stu-id="69cb9-115">Arduino expansion board</span></span>
* <span data-ttu-id="69cb9-116">Elementi distanziali o viti contenuti nel pacchetto, inclusi quattro set di viti ed elementi distanziali in plastica e due viti per fissare il modulo alla scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="69cb9-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="69cb9-117">Cavo USB Micro B/Tipo A</span><span class="sxs-lookup"><span data-stu-id="69cb9-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="69cb9-118">Alimentatore in corrente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="69cb9-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="69cb9-119">I valori nominali dell'alimentatore devono essere i seguenti:</span><span class="sxs-lookup"><span data-stu-id="69cb9-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="69cb9-120">7-15 V CC</span><span class="sxs-lookup"><span data-stu-id="69cb9-120">7-15V DC</span></span>
  - <span data-ttu-id="69cb9-121">Almeno 1500 mA</span><span class="sxs-lookup"><span data-stu-id="69cb9-121">At least 1500mA</span></span>
  - <span data-ttu-id="69cb9-122">Il pin centrale deve essere il polo positivo dell'alimentatore</span><span class="sxs-lookup"><span data-stu-id="69cb9-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Contenuto dello starter kit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="69cb9-124">Altri elementi necessari:</span><span class="sxs-lookup"><span data-stu-id="69cb9-124">You also need:</span></span>

* <span data-ttu-id="69cb9-125">Computer Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="69cb9-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="69cb9-126">Connessione wireless per Edison.</span><span class="sxs-lookup"><span data-stu-id="69cb9-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="69cb9-127">Connessione Internet per scaricare lo strumento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="69cb9-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="69cb9-128">Assemblare la scheda</span><span class="sxs-lookup"><span data-stu-id="69cb9-128">Assemble your board</span></span>

<span data-ttu-id="69cb9-129">Questa sezione contiene i passaggi per connettere il modulo Intel® Edison alla scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="69cb9-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="69cb9-130">Posizionare il modulo Intel® Edison all'interno del bordo bianco della scheda di espansione, allineando i fori del modulo con le viti della scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="69cb9-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="69cb9-131">Premere verso il basso il modulo sotto le parole `What will you make?` fino a quando non si sente uno scatto.</span><span class="sxs-lookup"><span data-stu-id="69cb9-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![assemblare la scheda 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="69cb9-133">Usare i due dadi esagonali (inclusi nel pacchetto) per fissare il modulo alla scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="69cb9-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![assemblare la scheda 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="69cb9-135">Inserire una vite in uno dei quattro fori negli angoli della scheda di espansione.</span><span class="sxs-lookup"><span data-stu-id="69cb9-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="69cb9-136">Avvitare e fissare uno dei due elementi distanziali in plastica alla vite.</span><span class="sxs-lookup"><span data-stu-id="69cb9-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![assemblare la scheda 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="69cb9-138">Ripetere l'operazione per gli altri tre elementi distanziali angolari.</span><span class="sxs-lookup"><span data-stu-id="69cb9-138">Repeat for the other three corner spacers.</span></span>

   ![assemblare la scheda 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="69cb9-140">A questo punto la scheda è assemblata.</span><span class="sxs-lookup"><span data-stu-id="69cb9-140">Now your board is assembled.</span></span>

   ![scheda assemblata](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="69cb9-142">Alimentare Edison</span><span class="sxs-lookup"><span data-stu-id="69cb9-142">Power up Edison</span></span>

1. <span data-ttu-id="69cb9-143">Collegare l'alimentatore.</span><span class="sxs-lookup"><span data-stu-id="69cb9-143">Plug in the power supply.</span></span>

   ![Collegare l'alimentatore](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="69cb9-145">Un LED verde (con etichetta DS1 sulla scheda di espansione Arduino*) dovrebbe accendersi e rimanere acceso.</span><span class="sxs-lookup"><span data-stu-id="69cb9-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="69cb9-146">Attendere un minuto per il completamento dell'avvio della scheda.</span><span class="sxs-lookup"><span data-stu-id="69cb9-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="69cb9-147">Se non si dispone di un alimentatore CC, è comunque possibile alimentare la scheda tramite una porta USB.</span><span class="sxs-lookup"><span data-stu-id="69cb9-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="69cb9-148">Per informazioni dettagliate, vedere la sezione `Connect Edison to your computer`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="69cb9-149">Questo modo di alimentare la scheda può causarne un comportamento non prevedibile, soprattutto quando si usa il Wi-Fi o si comandano motori.</span><span class="sxs-lookup"><span data-stu-id="69cb9-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="69cb9-150">Connettere Edison al computer</span><span class="sxs-lookup"><span data-stu-id="69cb9-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="69cb9-151">Spostare i microinterruttori verso le due porte micro-USB in modo che Edison si trovi in modalità dispositivo.</span><span class="sxs-lookup"><span data-stu-id="69cb9-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="69cb9-152">Per informazioni sulle differenze tra la modalità dispositivo e la modalità host, vedere [qui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="69cb9-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Spostare verso il basso il microinterruttore](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="69cb9-154">Collegare il cavo micro-USB alla porta micro-USB superiore.</span><span class="sxs-lookup"><span data-stu-id="69cb9-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Porta micro-USB superiore](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="69cb9-156">Collegare l'altra estremità del cavo USB al computer.</span><span class="sxs-lookup"><span data-stu-id="69cb9-156">Plug the other end of USB cable into your computer.</span></span>

   ![USB computer](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="69cb9-158">La scheda è completamente inizializzata quando il computer consente di montare una nuova unità (ad esempio inserendo una scheda SD).</span><span class="sxs-lookup"><span data-stu-id="69cb9-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="69cb9-159">Scaricare ed eseguire lo strumento di configurazione</span><span class="sxs-lookup"><span data-stu-id="69cb9-159">Download and run the configuration tool</span></span>
<span data-ttu-id="69cb9-160">Scaricare lo strumento di configurazione più recente presente in [questo collegamento](https://software.intel.com/en-us/iot/hardware/edison/downloads) sotto l'intestazione `Installers`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="69cb9-161">Eseguire lo strumento e attenersi alle istruzioni visualizzate. Fare clic su Avanti quando necessario.</span><span class="sxs-lookup"><span data-stu-id="69cb9-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="69cb9-162">Eseguire il flashing del firmware</span><span class="sxs-lookup"><span data-stu-id="69cb9-162">Flash firmware</span></span>
1. <span data-ttu-id="69cb9-163">Nella pagina `Set up options` fare clic su `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="69cb9-164">Selezionare l'immagine per eseguire il flashing sulla scheda tramite una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="69cb9-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="69cb9-165">Per scaricare ed eseguire il flashing della scheda con l'immagine del firmware più recente disponibile in Intel, selezionare `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="69cb9-166">Per eseguire il flashing della scheda con un'immagine già salvata nel computer, selezionare `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="69cb9-167">Individuare e selezionare l'immagine di cui si desidera eseguire il flashing nella scheda.</span><span class="sxs-lookup"><span data-stu-id="69cb9-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="69cb9-168">Lo strumento di installazione tenterà di eseguire il flashing della scheda.</span><span class="sxs-lookup"><span data-stu-id="69cb9-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="69cb9-169">L'intero processo di esecuzione del flashing può richiedere fino a 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="69cb9-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="69cb9-170">Impostare la password</span><span class="sxs-lookup"><span data-stu-id="69cb9-170">Set password</span></span>
1. <span data-ttu-id="69cb9-171">Nella pagina `Set up options` fare clic su `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="69cb9-172">Per la scheda Intel® Edison è possibile impostare un nome personalizzato.</span><span class="sxs-lookup"><span data-stu-id="69cb9-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="69cb9-173">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="69cb9-173">This is optional.</span></span>
3. <span data-ttu-id="69cb9-174">Digitare una password per la scheda e quindi fare clic su `Set password`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="69cb9-175">Annotare la password per usarla in seguito.</span><span class="sxs-lookup"><span data-stu-id="69cb9-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="69cb9-176">Connettere il Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="69cb9-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="69cb9-177">Nella pagina `Set up options` fare clic su `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="69cb9-178">Attendere fino a un minuto per la ricerca delle reti Wi-Fi disponibili.</span><span class="sxs-lookup"><span data-stu-id="69cb9-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="69cb9-179">Nell'elenco a discesa `Detected Networks` selezionare la rete.</span><span class="sxs-lookup"><span data-stu-id="69cb9-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="69cb9-180">Nell'elenco a discesa `Security` selezionare il tipo di sicurezza della rete.</span><span class="sxs-lookup"><span data-stu-id="69cb9-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="69cb9-181">Specificare le informazioni di accesso e la password, quindi fare clic su `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="69cb9-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="69cb9-182">Annotare l'indirizzo IP per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="69cb9-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="69cb9-183">Verificare che Edison sia connesso alla stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="69cb9-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="69cb9-184">Il computer si connette a Edison tramite l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="69cb9-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="69cb9-185">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="69cb9-185">Congratulations!</span></span> <span data-ttu-id="69cb9-186">Edison è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="69cb9-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="69cb9-187">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="69cb9-187">Summary</span></span>
<span data-ttu-id="69cb9-188">Questo articolo ha illustrato come assemblare la scheda Edison, eseguire il flashing del firmware, impostare la password e connetterla al Wi-Fi usando lo strumento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="69cb9-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="69cb9-189">Si noti che il LED non si illumina ancora.</span><span class="sxs-lookup"><span data-stu-id="69cb9-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="69cb9-190">L'attività successiva consiste nell'installazione del software e degli strumenti necessari per preparare l'esecuzione di un'applicazione di esempio in Edison.</span><span class="sxs-lookup"><span data-stu-id="69cb9-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69cb9-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69cb9-191">Next steps</span></span>
<span data-ttu-id="69cb9-192">[Ottenere gli strumenti][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="69cb9-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md