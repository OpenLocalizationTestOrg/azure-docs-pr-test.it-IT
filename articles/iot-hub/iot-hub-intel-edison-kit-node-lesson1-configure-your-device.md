---
title: 'Connettersi Edison Intel (nodo) tooAzure IoT - lezione 1: configurare i dispositivi | Documenti Microsoft'
description: Configurare Intel Edison per il primo utilizzo.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino impostato, connettersi arduino toopc, il programma di installazione arduino, arduino Lavagna
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
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="b5a11-104">Configurare Intel Edison</span><span class="sxs-lookup"><span data-stu-id="b5a11-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="b5a11-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b5a11-105">What you will do</span></span>
<span data-ttu-id="b5a11-106">Configurare Edison Intel per primo utilizzo assemblando Lavagna hello, l'accensione e l'installazione dello strumento Configurazione tooyour desktop tooflash OS firmware di Edison, impostare la relativa password e connetterla tooWi-Fi.</span><span class="sxs-lookup"><span data-stu-id="b5a11-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="b5a11-107">Se si verificano problemi, cercare soluzioni in hello [risoluzione dei problemi di pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="b5a11-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="b5a11-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="b5a11-108">What you will learn</span></span>
<span data-ttu-id="b5a11-109">Contenuto dell'articolo:</span><span class="sxs-lookup"><span data-stu-id="b5a11-109">In this article, you will learn:</span></span>

* <span data-ttu-id="b5a11-110">Come tooassemble Edison bordo e il sistema e backup.</span><span class="sxs-lookup"><span data-stu-id="b5a11-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="b5a11-111">Come firmware di Edison tooflash, impostare la password e la connessione Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="b5a11-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b5a11-112">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="b5a11-112">What you need</span></span>
<span data-ttu-id="b5a11-113">toocomplete questa operazione, è necessario hello dallo Starter Kit Edison Intel le seguenti parti:</span><span class="sxs-lookup"><span data-stu-id="b5a11-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="b5a11-114">Modulo Intel® Edison</span><span class="sxs-lookup"><span data-stu-id="b5a11-114">Intel® Edison module</span></span>
* <span data-ttu-id="b5a11-115">Scheda di espansione Arduino</span><span class="sxs-lookup"><span data-stu-id="b5a11-115">Arduino expansion board</span></span>
* <span data-ttu-id="b5a11-116">Le barre dello spaziatore né viti incluse nel pacchetto di hello, tra cui scheda di espansione toohello modulo hello toofasten due viti e quattro set di viti e spaziatore plastica.</span><span class="sxs-lookup"><span data-stu-id="b5a11-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="b5a11-117">Un cavo USB A di tooType Micro B</span><span class="sxs-lookup"><span data-stu-id="b5a11-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="b5a11-118">Alimentatore in corrente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="b5a11-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="b5a11-119">I valori nominali dell'alimentatore devono essere i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b5a11-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="b5a11-120">7-15 V CC</span><span class="sxs-lookup"><span data-stu-id="b5a11-120">7-15V DC</span></span>
  - <span data-ttu-id="b5a11-121">Almeno 1500 mA</span><span class="sxs-lookup"><span data-stu-id="b5a11-121">At least 1500mA</span></span>
  - <span data-ttu-id="b5a11-122">pin center/interna Hello devono essere polo positivo hello di alimentatore hello</span><span class="sxs-lookup"><span data-stu-id="b5a11-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![Contenuto dello starter kit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="b5a11-124">Altri elementi necessari:</span><span class="sxs-lookup"><span data-stu-id="b5a11-124">You also need:</span></span>

* <span data-ttu-id="b5a11-125">Computer Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="b5a11-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="b5a11-126">Una connessione wireless per tooconnect Edison per.</span><span class="sxs-lookup"><span data-stu-id="b5a11-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="b5a11-127">Strumento di configurazione toodownload connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="b5a11-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="b5a11-128">Assemblare la scheda</span><span class="sxs-lookup"><span data-stu-id="b5a11-128">Assemble your board</span></span>

<span data-ttu-id="b5a11-129">In questa sezione contiene passaggi tooattach la scheda di espansione Intel® Edison tooyour modulo.</span><span class="sxs-lookup"><span data-stu-id="b5a11-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="b5a11-130">Modulo di Intel® Edison hello sul posto all'interno di struttura hello bianca sulla Lavagna espansione, allineare fori hello sul modulo hello con viti hello nella scheda di espansione hello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="b5a11-131">Premere sul modulo hello subito dopo le parole hello `What will you make?` fino a quando non si ritiene un gioco da ragazzi.</span><span class="sxs-lookup"><span data-stu-id="b5a11-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![assemblare la scheda 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="b5a11-133">Utilizzare una scheda di espansione di hello due dadi esadecimale (inclusi nel pacchetto hello) toosecure hello modulo toohello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![assemblare la scheda 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="b5a11-135">Inserire una vite in uno dei quattro fori angolo hello nella scheda di espansione hello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="b5a11-136">Torsione e stringere uno spaziatore plastica di hello bianco su vite hello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![assemblare la scheda 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="b5a11-138">Ripetere l'operazione per hello spaziatore altri tre angolo.</span><span class="sxs-lookup"><span data-stu-id="b5a11-138">Repeat for hello other three corner spacers.</span></span>

   ![assemblare la scheda 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="b5a11-140">A questo punto la scheda è assemblata.</span><span class="sxs-lookup"><span data-stu-id="b5a11-140">Now your board is assembled.</span></span>

   ![scheda assemblata](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="b5a11-142">Alimentare Edison</span><span class="sxs-lookup"><span data-stu-id="b5a11-142">Power up Edison</span></span>

1. <span data-ttu-id="b5a11-143">Plug-in dell'alimentatore hello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-143">Plug in hello power supply.</span></span>

   ![Collegare l'alimentatore](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="b5a11-145">Un LED verde (nella scheda di espansione Arduino * hello con etichettato DS1) dovrebbe accendersi e rimanere acceso.</span><span class="sxs-lookup"><span data-stu-id="b5a11-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="b5a11-146">Attendere un minuto per hello Lavagna toofinish l'avvio.</span><span class="sxs-lookup"><span data-stu-id="b5a11-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b5a11-147">Se non si dispone di un alimentatore controller di dominio, è comunque possibile Lavagna hello power attraverso una porta USB.</span><span class="sxs-lookup"><span data-stu-id="b5a11-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="b5a11-148">Per informazioni dettagliate, vedere la sezione `Connect Edison tooyour computer`.</span><span class="sxs-lookup"><span data-stu-id="b5a11-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="b5a11-149">Questo modo di alimentare la scheda può causarne un comportamento non prevedibile, soprattutto quando si usa il Wi-Fi o si comandano motori.</span><span class="sxs-lookup"><span data-stu-id="b5a11-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="b5a11-150">Connettere computer tooyour Edison</span><span class="sxs-lookup"><span data-stu-id="b5a11-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="b5a11-151">Attiva o disattiva verso il basso microinterruttore hello verso hello due micro porte USB, in modo che Edison è in modalità di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b5a11-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="b5a11-152">Per informazioni sulle differenze tra la modalità dispositivo e la modalità host, vedere [qui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="b5a11-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Attivare o disattivare verso il basso microinterruttore hello](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="b5a11-154">Collegare il cavo USB micro di hello superiore porta USB micro hello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Porta micro-USB superiore](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="b5a11-156">Plug hello altra estremità del cavo USB nel computer.</span><span class="sxs-lookup"><span data-stu-id="b5a11-156">Plug hello other end of USB cable into your computer.</span></span>

   ![USB computer](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="b5a11-158">La scheda è completamente inizializzata quando il computer consente di montare una nuova unità (ad esempio inserendo una scheda SD).</span><span class="sxs-lookup"><span data-stu-id="b5a11-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="b5a11-159">Scaricare ed eseguire lo strumento di configurazione hello</span><span class="sxs-lookup"><span data-stu-id="b5a11-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="b5a11-160">Strumento di configurazione più recente di hello da ottenere [questo collegamento](https://software.intel.com/en-us/iot/hardware/edison/downloads) sotto hello `Installers` intestazione.</span><span class="sxs-lookup"><span data-stu-id="b5a11-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="b5a11-161">Esecuzione dello strumento hello e seguire il visualizzate le istruzioni, fare clic su Avanti dove necessario</span><span class="sxs-lookup"><span data-stu-id="b5a11-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="b5a11-162">Eseguire il flashing del firmware</span><span class="sxs-lookup"><span data-stu-id="b5a11-162">Flash firmware</span></span>
1. <span data-ttu-id="b5a11-163">In hello `Set up options` pagina, fare clic su `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="b5a11-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="b5a11-164">Selezionare tooflash immagine hello nella scheda effettuando una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="b5a11-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="b5a11-165">toodownload e flash la Lavagna con hello più recente del firmware immagine disponibile da Intel, selezionare `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="b5a11-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="b5a11-166">Selezionare la scheda con un'immagine è già stato salvato nel computer in uso, tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="b5a11-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="b5a11-167">Sfoglia tooand hello selezionare l'immagine tooflash tooyour Lavagna.</span><span class="sxs-lookup"><span data-stu-id="b5a11-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="b5a11-168">strumento di configurazione Hello tenterà tooflash la Lavagna.</span><span class="sxs-lookup"><span data-stu-id="b5a11-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="b5a11-169">processo lampeggiante Hello potrebbe richiedere too10 minuti.</span><span class="sxs-lookup"><span data-stu-id="b5a11-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="b5a11-170">Impostare la password</span><span class="sxs-lookup"><span data-stu-id="b5a11-170">Set password</span></span>
1. <span data-ttu-id="b5a11-171">In hello `Set up options` pagina, fare clic su `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="b5a11-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="b5a11-172">Per la scheda Intel® Edison è possibile impostare un nome personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b5a11-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="b5a11-173">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b5a11-173">This is optional.</span></span>
3. <span data-ttu-id="b5a11-174">Digitare una password per la scheda e quindi fare clic su `Set password`.</span><span class="sxs-lookup"><span data-stu-id="b5a11-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="b5a11-175">Contrassegnare come inattivo password hello, che viene utilizzata in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b5a11-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="b5a11-176">Connettere il Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="b5a11-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="b5a11-177">In hello `Set up options` pagina, fare clic su `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="b5a11-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="b5a11-178">Attesa di minuto tooone come l'analisi del computer per reti Wi-Fi disponibili.</span><span class="sxs-lookup"><span data-stu-id="b5a11-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="b5a11-179">Da hello `Detected Networks` elenco a discesa, selezionare la rete.</span><span class="sxs-lookup"><span data-stu-id="b5a11-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="b5a11-180">Da hello `Security` elenco a discesa, il tipo di sicurezza della rete selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="b5a11-181">Specificare le informazioni di accesso e la password, quindi fare clic su `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="b5a11-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="b5a11-182">Contrassegnare come inattivo hello indirizzo IP, che viene utilizzato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b5a11-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="b5a11-183">Assicurarsi che Edison sia connesso toohello stessa rete del computer.</span><span class="sxs-lookup"><span data-stu-id="b5a11-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="b5a11-184">Il computer si connette tooyour Edison utilizzando l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="b5a11-185">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="b5a11-185">Congratulations!</span></span> <span data-ttu-id="b5a11-186">Edison è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="b5a11-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="b5a11-187">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b5a11-187">Summary</span></span>
<span data-ttu-id="b5a11-188">In questo articolo, si è appreso come tooassemble hello Lavagna Edison, flash relativo firmware, la password di installazione e connetterla tooWi-Fi usando lo strumento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b5a11-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="b5a11-189">Si noti che hello che LED non ancora accendersi.</span><span class="sxs-lookup"><span data-stu-id="b5a11-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="b5a11-190">attività successiva Hello è software in preparazione per l'esecuzione di un'applicazione di esempio in Edison e gli strumenti necessari di tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="b5a11-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5a11-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5a11-191">Next steps</span></span>
<span data-ttu-id="b5a11-192">[Ottenere strumenti hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="b5a11-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md