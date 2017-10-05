---
title: Sostituzione di un PCM nel dispositivo StorSimple | Microsoft Docs
description: Viene illustrato come rimuovere e sostituire il modulo di alimentazione e raffreddamento (PCM, Power and Cooling Module) nel dispositivo StorSimple
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 2a956de58b279a013913631a077d7b03c6327f72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="6a1dc-103">Sostituzione di un modulo di alimentazione e raffreddamento nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="6a1dc-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="6a1dc-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6a1dc-104">Overview</span></span>
<span data-ttu-id="6a1dc-105">Il modulo di alimentazione e raffreddamento (PCM, Power and Cooling Module) nel dispositivo Microsoft Azure StorSimple è costituito da un alimentatore e ventole di raffreddamento controllati attraverso gli chassis principale e EBOD.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="6a1dc-106">Esiste un solo modello di PCM certificato per ciascuno chassis.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="6a1dc-107">Lo chassis principale è certificato per un PCM 764 W e lo chassis EBOD è certificato per un PCM 580 W.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="6a1dc-108">Sebbene i PCM per lo chassis principale e lo chassis EBOD siano diversi, la procedura di sostituzione è identica.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="6a1dc-109">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="6a1dc-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="6a1dc-110">Rimuovere un PCM</span><span class="sxs-lookup"><span data-stu-id="6a1dc-110">Remove a PCM</span></span>
* <span data-ttu-id="6a1dc-111">Installare un PCM sostitutivo</span><span class="sxs-lookup"><span data-stu-id="6a1dc-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a1dc-112">Prima di rimuovere e sostituire un PCM, esaminare le informazioni di sicurezza descritte in [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="6a1dc-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="6a1dc-113">Prima di sostituire un PCM:</span><span class="sxs-lookup"><span data-stu-id="6a1dc-113">Before you replace a PCM</span></span>
<span data-ttu-id="6a1dc-114">Prima di sostituire il PCM, tenere presente i seguenti aspetti importanti:</span><span class="sxs-lookup"><span data-stu-id="6a1dc-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="6a1dc-115">Se l'alimentatore del PCM è guasto, lasciare il modulo guasto installato, ma rimuovere il cavo di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="6a1dc-116">La ventola continuerà a ricevere alimentazione dallo chassis e a fornire il raffreddamento appropriato.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="6a1dc-117">Se la ventola è guasta, il PCM deve essere sostituito immediatamente.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="6a1dc-118">Prima di rimuovere il PCM, disconnettere l'alimentazione da PCM disattivando l'interruttore principale (se presente) oppure rimuovendo fisicamente il cavo di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="6a1dc-119">Ciò determina la visualizzazione di un avviso sul sistema indicante che è imminente un'interruzione dell'alimentazione.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="6a1dc-120">Assicurarsi che l'altro PCM sia funzionale per un funzionamento continuato del sistema prima di sostituire il PCM guasto.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="6a1dc-121">Un PCM guasto deve essere sostituito con un PCM completamente funzionante appena possibile.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="6a1dc-122">La sostituzione del modulo PCM richiede solo alcuni minuti, ma deve essere completata entro 10 minuti dalla rimozione del PCM guasto per impedire il surriscaldamento.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="6a1dc-123">Notare che i moduli 764 W PCM di sostituzione forniti dal produttore non contengono il modulo batteria di backup.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="6a1dc-124">È necessario rimuovere la batteria dal PCM non funzionante, quindi inserirla nel modulo di sostituzione prima di eseguire la sostituzione.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="6a1dc-125">Per altre informazioni, vedere come [rimuovere e inserire un modulo batteria di backup](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="6a1dc-125">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="6a1dc-126">Rimuovere un PCM</span><span class="sxs-lookup"><span data-stu-id="6a1dc-126">Remove a PCM</span></span>
<span data-ttu-id="6a1dc-127">Per rimuovere un modulo di alimentazione e raffreddamento (PCM, Power and Cooling Module) dal dispositivo Microsoft Azure StorSimple, seguire queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="6a1dc-128">Prima di rimuovere il PCM, verificare di disporre di una sostituzione appropriata (764 W per lo chassis principale o 580 W per lo chassis EBOD).</span><span class="sxs-lookup"><span data-stu-id="6a1dc-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>
> 
> 

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="6a1dc-129">Per rimuovere un PCM:</span><span class="sxs-lookup"><span data-stu-id="6a1dc-129">To remove a PCM</span></span>
1. <span data-ttu-id="6a1dc-130">Nel portale di Azure classico, fare clic su **Dispositivi** > **Manutenzione** > **Stato hardware**.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-130">In the Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="6a1dc-131">Controllare lo stato dei componenti del PCM sotto **Componenti condivisi** per identificare quale PCM è guasto:</span><span class="sxs-lookup"><span data-stu-id="6a1dc-131">Check the status of the PCM components under **Shared Components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="6a1dc-132">Se un alimentatore in PCM 0 è guasto, lo stato di **Alimentatore in PCM 0** sarà rosso.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="6a1dc-133">Se un alimentatore in PCM 1 è guasto, lo stato di **Alimentatore in PCM 1** sarà rosso.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="6a1dc-134">Se la ventola in PCM 1 è guasta, lo stato di **Raffreddamento 0 per PCM 0** o **Raffreddamento 1 per PCM 0** sarà rosso.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="6a1dc-135">Individuare il PCM guasto nella parte posteriore dello chassis principale.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="6a1dc-136">Se si esegue un modello 8600, identificare lo chassis principale controllando il numero di identificazione unità di sistema mostrato sul display LED del pannello anteriore.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="6a1dc-137">L'ID unità predefinito visualizzato sullo chassis principale è **00**, mentre l'ID unità predefinito visualizzato sullo chassis EBOD è **01**.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="6a1dc-138">Nel diagramma e nella tabella seguenti viene illustrato il pannello anteriore del display LED.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![ID del sistema sul pannello anteriore delle operazioni](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="6a1dc-140">**Figura 1** Pannello anteriore del dispositivo</span><span class="sxs-lookup"><span data-stu-id="6a1dc-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="6a1dc-141">Etichetta</span><span class="sxs-lookup"><span data-stu-id="6a1dc-141">Label</span></span> | <span data-ttu-id="6a1dc-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6a1dc-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="6a1dc-143">1</span><span class="sxs-lookup"><span data-stu-id="6a1dc-143">1</span></span> |<span data-ttu-id="6a1dc-144">Pulsante di disattivazione audio</span><span class="sxs-lookup"><span data-stu-id="6a1dc-144">Mute button</span></span> |
   | <span data-ttu-id="6a1dc-145">2</span><span class="sxs-lookup"><span data-stu-id="6a1dc-145">2</span></span> |<span data-ttu-id="6a1dc-146">Alimentazione del sistema</span><span class="sxs-lookup"><span data-stu-id="6a1dc-146">System power</span></span> |
   | <span data-ttu-id="6a1dc-147">3</span><span class="sxs-lookup"><span data-stu-id="6a1dc-147">3</span></span> |<span data-ttu-id="6a1dc-148">Errore del modulo</span><span class="sxs-lookup"><span data-stu-id="6a1dc-148">Module fault</span></span> |
   | <span data-ttu-id="6a1dc-149">4</span><span class="sxs-lookup"><span data-stu-id="6a1dc-149">4</span></span> |<span data-ttu-id="6a1dc-150">Errore logico</span><span class="sxs-lookup"><span data-stu-id="6a1dc-150">Logical fault</span></span> |
   | <span data-ttu-id="6a1dc-151">5</span><span class="sxs-lookup"><span data-stu-id="6a1dc-151">5</span></span> |<span data-ttu-id="6a1dc-152">Display ID unità</span><span class="sxs-lookup"><span data-stu-id="6a1dc-152">Unit ID display</span></span> |
3. <span data-ttu-id="6a1dc-153">I LED degli indicatori di monitoraggio nella parte posteriore dello chassis principale possono inoltre essere utilizzati per identificare il PCM guasto.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="6a1dc-154">Vedere il diagramma e la tabella seguenti per comprendere come utilizzare i LED per individuare il PCM guasto.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="6a1dc-155">Ad esempio, se il LED corrispondente a **Guasto ventola** è attivo, la ventola è guasta.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="6a1dc-156">Allo stesso modo, se il LED corrispondente a **Guasto CA** è attivo, l'alimentatore è guasto.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![Backplane degli indicatori LED di monitoraggio del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="6a1dc-158">**Figura 2** Parte posteriore del PCM con i LED degli indicatori</span><span class="sxs-lookup"><span data-stu-id="6a1dc-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="6a1dc-159">Etichetta</span><span class="sxs-lookup"><span data-stu-id="6a1dc-159">Label</span></span> | <span data-ttu-id="6a1dc-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6a1dc-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="6a1dc-161">1</span><span class="sxs-lookup"><span data-stu-id="6a1dc-161">1</span></span> |<span data-ttu-id="6a1dc-162">Guasto dell’alimentazione CA</span><span class="sxs-lookup"><span data-stu-id="6a1dc-162">AC power failure</span></span> |
   | <span data-ttu-id="6a1dc-163">2</span><span class="sxs-lookup"><span data-stu-id="6a1dc-163">2</span></span> |<span data-ttu-id="6a1dc-164">Guasto alla ventola</span><span class="sxs-lookup"><span data-stu-id="6a1dc-164">Fan failure</span></span> |
   | <span data-ttu-id="6a1dc-165">3</span><span class="sxs-lookup"><span data-stu-id="6a1dc-165">3</span></span> |<span data-ttu-id="6a1dc-166">Guasto alla batteria</span><span class="sxs-lookup"><span data-stu-id="6a1dc-166">Battery fault</span></span> |
   | <span data-ttu-id="6a1dc-167">4</span><span class="sxs-lookup"><span data-stu-id="6a1dc-167">4</span></span> |<span data-ttu-id="6a1dc-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="6a1dc-168">PCM OK</span></span> |
   | <span data-ttu-id="6a1dc-169">5</span><span class="sxs-lookup"><span data-stu-id="6a1dc-169">5</span></span> |<span data-ttu-id="6a1dc-170">Guasto dell'alimentazione CC</span><span class="sxs-lookup"><span data-stu-id="6a1dc-170">DC power failure</span></span> |
   | <span data-ttu-id="6a1dc-171">6</span><span class="sxs-lookup"><span data-stu-id="6a1dc-171">6</span></span> |<span data-ttu-id="6a1dc-172">Integrità della batteria</span><span class="sxs-lookup"><span data-stu-id="6a1dc-172">Battery healthy</span></span> |
4. <span data-ttu-id="6a1dc-173">Fare riferimento al diagramma seguente relativo alla parte posteriore del dispositivo StorSimple per individuare il modulo PCM guasto.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="6a1dc-174">PCM 0 è a sinistra e PCM 1 è a destra.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="6a1dc-175">Nella tabella seguente vengono illustrati i moduli.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-175">The table that follows explains the modules.</span></span>
   
     ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="6a1dc-177">**Figura 3** Parte posteriore del dispositivo con moduli plug-in</span><span class="sxs-lookup"><span data-stu-id="6a1dc-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="6a1dc-178">Etichetta</span><span class="sxs-lookup"><span data-stu-id="6a1dc-178">Label</span></span> | <span data-ttu-id="6a1dc-179">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6a1dc-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="6a1dc-180">1</span><span class="sxs-lookup"><span data-stu-id="6a1dc-180">1</span></span> |<span data-ttu-id="6a1dc-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="6a1dc-181">PCM 0</span></span> |
   | <span data-ttu-id="6a1dc-182">2</span><span class="sxs-lookup"><span data-stu-id="6a1dc-182">2</span></span> |<span data-ttu-id="6a1dc-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="6a1dc-183">PCM 1</span></span> |
   | <span data-ttu-id="6a1dc-184">3</span><span class="sxs-lookup"><span data-stu-id="6a1dc-184">3</span></span> |<span data-ttu-id="6a1dc-185">Controller 0</span><span class="sxs-lookup"><span data-stu-id="6a1dc-185">Controller 0</span></span> |
   | <span data-ttu-id="6a1dc-186">4</span><span class="sxs-lookup"><span data-stu-id="6a1dc-186">4</span></span> |<span data-ttu-id="6a1dc-187">Controller 1</span><span class="sxs-lookup"><span data-stu-id="6a1dc-187">Controller 1</span></span> |
5. <span data-ttu-id="6a1dc-188">Disattivare il PCM guasto e disconnettere il cavo di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="6a1dc-189">È ora possibile rimuovere il PCM.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="6a1dc-190">Afferrare il chiavistello e il lato del punto di manipolazione del PCM tra il pollice e l'indice, quindi stringerli insieme per aprire il punto di manipolazione.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![Apertura del punto di manipolazione del PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="6a1dc-192">**Figura 4** Apertura del punto di manipolazione del PCM</span><span class="sxs-lookup"><span data-stu-id="6a1dc-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="6a1dc-193">Afferrare il punto di manipolazione e rimuovere il PCM.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-193">Grip the handle and remove the PCM.</span></span>
   
    ![Rimozione del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="6a1dc-195">**Figura 5** Rimozione del PCM</span><span class="sxs-lookup"><span data-stu-id="6a1dc-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="6a1dc-196">Installare un PCM sostitutivo</span><span class="sxs-lookup"><span data-stu-id="6a1dc-196">Install a replacement PCM</span></span>
<span data-ttu-id="6a1dc-197">Seguire queste istruzioni per installare un PCM nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="6a1dc-198">Verificare di avere inserito il modulo batteria di backup prima di installare il PCM di sostituzione (si applica solo a 764 W PCM).</span><span class="sxs-lookup"><span data-stu-id="6a1dc-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="6a1dc-199">Per altre informazioni, vedere come [rimuovere e inserire un modulo batteria di backup](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="6a1dc-199">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="6a1dc-200">Per installare un PCM:</span><span class="sxs-lookup"><span data-stu-id="6a1dc-200">To install a PCM</span></span>
1. <span data-ttu-id="6a1dc-201">Verificare di disporre del PCM sostitutivo corretto per questo chassis.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="6a1dc-202">Per lo chassis principale è necessario un PCM 764 W e per lo chassis EBOD un PCM 580 W.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="6a1dc-203">Non tentare di utilizzare il PCM 580 W nello chassis principale o il PCM 764 W nello chassis EBOD.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="6a1dc-204">Nell'immagine seguente viene illustrato come identificare queste informazioni sull'etichetta apposta sul PCM.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![Etichetta del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="6a1dc-206">**Figura 6** Etichetta del PCM</span><span class="sxs-lookup"><span data-stu-id="6a1dc-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="6a1dc-207">Verifica la presenza di danni sullo chassis, prestando particolare attenzione ai connettori.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6a1dc-208">**Non installare il modulo se i perni dei connettori sono piegati.**</span><span class="sxs-lookup"><span data-stu-id="6a1dc-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="6a1dc-209">Con il punto di manipolazione del PCM in posizione aperta, far scorrere il modulo nello chassis.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![Installazione del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="6a1dc-211">**Figura 7** Installazione del PCM</span><span class="sxs-lookup"><span data-stu-id="6a1dc-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="6a1dc-212">Chiudere manualmente il punto di manipolazione del PCM.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-212">Manually close the PCM handle.</span></span> <span data-ttu-id="6a1dc-213">Quando il punto di manipolazione viene attivato si dovrebbe ascoltare un clic.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-213">You should hear a click as the handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6a1dc-214">Per assicurasi che i perni dei connettori siano attivati, è possibile tirare delicatamente il punto di manipolazione senza rilasciare il chiavistello.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="6a1dc-215">Se il PCM scorre fuori, il chiavistello è stato chiuso prima dell'attivazione dei connettori.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="6a1dc-216">Connettere i cavi di alimentazione alla fonte di alimentazione e al PCM.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="6a1dc-217">Fissare in posizione le fascette di serraggio.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-217">Secure the strain relief bales.</span></span> 
7. <span data-ttu-id="6a1dc-218">Accendere il PCM.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="6a1dc-219">Verificare che la sostituzione sia stata completata correttamente: nel portale di Azure classico del servizio StorSimple Manager, passare a **Dispositivi** > **Manutenzione** > **Stato hardware**.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-219">Verify that the replacement was successful: in the Azure classic portal of your StorSimple Manager service, navigate to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="6a1dc-220">Sotto **Componenti condivisi**, lo stato del PCM dovrebbe essere verde.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-220">Under **Shared Components**, the status of the PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6a1dc-221">L'inizializzazione completa del PCM sostitutivo potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="6a1dc-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="6a1dc-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a1dc-222">Next steps</span></span>
<span data-ttu-id="6a1dc-223">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="6a1dc-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

