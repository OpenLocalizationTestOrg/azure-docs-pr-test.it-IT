---
title: Sostituire la batteria sul dispositivo Microsoft Azure StorSimple serie 8000 | Microsoft Docs
description: Viene descritto come rimuovere, sostituire e mantenere il modulo della batteria di backup nel dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 174a3163082594ea6a49b7f5a78857848f8f0566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="15007-103">Sostituzione del modulo della batteria di backup nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="15007-103">Replace the backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="15007-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="15007-104">Overview</span></span>
<span data-ttu-id="15007-105">Il modulo di alimentazione e raffreddamento (PCM, Power and Cooling Module) dello chassis principale nel dispositivo Microsoft Azure StorSimple dispone di un pacchetto di batteria aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="15007-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="15007-106">Tale pacchetto fornisce l'alimentazione in modo che il dispositivo StorSimple possa salvare i dati in caso di perdita dell'alimentazione CA allo chassis principale.</span><span class="sxs-lookup"><span data-stu-id="15007-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="15007-107">Questo pacchetto di batteria viene definito come *modulo della batteria di backup*.</span><span class="sxs-lookup"><span data-stu-id="15007-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="15007-108">Il modulo della batteria di backup è disponibile solo per lo chassis principale nel dispositivo StorSimple (lo chassis EBOD non contiene un modulo della batteria di backup).</span><span class="sxs-lookup"><span data-stu-id="15007-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="15007-109">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="15007-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="15007-110">Rimuovere il modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="15007-110">Remove the backup battery module</span></span>
* <span data-ttu-id="15007-111">Installare un nuovo modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="15007-111">Install a new backup battery module</span></span>
* <span data-ttu-id="15007-112">Mantenimento del modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="15007-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15007-113">Prima di rimuovere e sostituire un modulo della batteria di backup, esaminare le informazioni di sicurezza descritte in [Introduzione alla sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="15007-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="15007-114">Rimuovere il modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="15007-114">Remove the backup battery module</span></span>
<span data-ttu-id="15007-115">Il modulo della batteria di backup per il dispositivo StorSimple è un'unità sostituibile sul campo.</span><span class="sxs-lookup"><span data-stu-id="15007-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="15007-116">Prima di installarlo nel PCM, il modulo della batteria deve essere archiviato nel pacchetto originale.</span><span class="sxs-lookup"><span data-stu-id="15007-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="15007-117">Eseguire i seguenti passaggi per rimuovere la batteria di backup.</span><span class="sxs-lookup"><span data-stu-id="15007-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="15007-118">Per rimuovere il modulo della batteria di backup:</span><span class="sxs-lookup"><span data-stu-id="15007-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="15007-119">Nel portale di Azure passare al pannello del servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="15007-119">In the Azure portal, go to your StorSimple Device Manager service blade.</span></span> <span data-ttu-id="15007-120">Passare a **Dispositivi** e selezionare il dispositivo dall'elenco dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="15007-120">Go to **Devices** and then select your device from the list of devices.</span></span> <span data-ttu-id="15007-121">Passare a **Monitoraggio** > **Integrità hardware**.</span><span class="sxs-lookup"><span data-stu-id="15007-121">Navigate to **Monitor** > **Hardware health**.</span></span> <span data-ttu-id="15007-122">Sotto **Componenti condivisi**, controllare lo stato della batteria.</span><span class="sxs-lookup"><span data-stu-id="15007-122">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="15007-123">Identificare il PCM in cui la batteria è guasta.</span><span class="sxs-lookup"><span data-stu-id="15007-123">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="15007-124">Nella Figura 1 viene mostrata la parte posteriore del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="15007-124">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="15007-126">**Figura 1** Parte posteriore del dispositivo principale in cui vengono mostrati il PCM e i moduli del controller</span><span class="sxs-lookup"><span data-stu-id="15007-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="15007-127">Etichetta</span><span class="sxs-lookup"><span data-stu-id="15007-127">Label</span></span> | <span data-ttu-id="15007-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="15007-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="15007-129">1</span><span class="sxs-lookup"><span data-stu-id="15007-129">1</span></span> |<span data-ttu-id="15007-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="15007-130">PCM 0</span></span> |
   | <span data-ttu-id="15007-131">2</span><span class="sxs-lookup"><span data-stu-id="15007-131">2</span></span> |<span data-ttu-id="15007-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="15007-132">PCM 1</span></span> |
   | <span data-ttu-id="15007-133">3</span><span class="sxs-lookup"><span data-stu-id="15007-133">3</span></span> |<span data-ttu-id="15007-134">Controller 0</span><span class="sxs-lookup"><span data-stu-id="15007-134">Controller 0</span></span> |
   | <span data-ttu-id="15007-135">4</span><span class="sxs-lookup"><span data-stu-id="15007-135">4</span></span> |<span data-ttu-id="15007-136">Controller 1</span><span class="sxs-lookup"><span data-stu-id="15007-136">Controller 1</span></span> |
   
    <span data-ttu-id="15007-137">Come mostrato nella Figura 2 numero 3, l'indicatore LED di monitoraggio sul PCM 0 che corrisponde a **Guasto alla batteria** deve essere attivato.</span><span class="sxs-lookup"><span data-stu-id="15007-137">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Backplane degli indicatori LED di monitoraggio del PCM del dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="15007-139">**Figura 2** Parte posteriore del PCM in cui vengono mostrati gli indicatori LED di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="15007-139">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="15007-140">Etichetta</span><span class="sxs-lookup"><span data-stu-id="15007-140">Label</span></span> | <span data-ttu-id="15007-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="15007-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="15007-142">1</span><span class="sxs-lookup"><span data-stu-id="15007-142">1</span></span> |<span data-ttu-id="15007-143">Guasto dell’alimentazione CA</span><span class="sxs-lookup"><span data-stu-id="15007-143">AC power failure</span></span> |
   | <span data-ttu-id="15007-144">2</span><span class="sxs-lookup"><span data-stu-id="15007-144">2</span></span> |<span data-ttu-id="15007-145">Guasto alla ventola</span><span class="sxs-lookup"><span data-stu-id="15007-145">Fan failure</span></span> |
   | <span data-ttu-id="15007-146">3</span><span class="sxs-lookup"><span data-stu-id="15007-146">3</span></span> |<span data-ttu-id="15007-147">Guasto alla batteria</span><span class="sxs-lookup"><span data-stu-id="15007-147">Battery fault</span></span> |
   | <span data-ttu-id="15007-148">4</span><span class="sxs-lookup"><span data-stu-id="15007-148">4</span></span> |<span data-ttu-id="15007-149">PCM OK</span><span class="sxs-lookup"><span data-stu-id="15007-149">PCM OK</span></span> |
   | <span data-ttu-id="15007-150">5</span><span class="sxs-lookup"><span data-stu-id="15007-150">5</span></span> |<span data-ttu-id="15007-151">Guasto dell'alimentazione CC</span><span class="sxs-lookup"><span data-stu-id="15007-151">DC power failure</span></span> |
   | <span data-ttu-id="15007-152">6</span><span class="sxs-lookup"><span data-stu-id="15007-152">6</span></span> |<span data-ttu-id="15007-153">Integrità della batteria</span><span class="sxs-lookup"><span data-stu-id="15007-153">Battery healthy</span></span> |
3. <span data-ttu-id="15007-154">Per rimuovere il PCM con una batteria guasta, seguire i passaggi descritti in [Rimozione di un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="15007-154">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="15007-155">Dopo aver rimosso il PCM, sollevare e ruotare il punto di manipolazione del modulo della batteria verso l'alto, come indicato nella figura riportata di seguito ed estrarlo fino a rimuovere la batteria.</span><span class="sxs-lookup"><span data-stu-id="15007-155">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Rimozione della batteria dal PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="15007-157">**Figura 3** Rimozione della batteria dal PCM</span><span class="sxs-lookup"><span data-stu-id="15007-157">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="15007-158">Inserire il modulo nel pacchetto dell'unità sostituibile sul campo.</span><span class="sxs-lookup"><span data-stu-id="15007-158">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="15007-159">Restituire l'unità difettosa a Microsoft per un'assistenza e una gestione appropriate.</span><span class="sxs-lookup"><span data-stu-id="15007-159">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="15007-160">Installare un nuovo modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="15007-160">Install a new backup battery module</span></span>
<span data-ttu-id="15007-161">Eseguire i passaggi seguenti per installare il modulo della batteria sostitutiva nel PCM nello chassis principale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="15007-161">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="15007-162">Per installare il modulo della batteria:</span><span class="sxs-lookup"><span data-stu-id="15007-162">To install the battery module</span></span>
1. <span data-ttu-id="15007-163">Inserire il modulo della batteria di backup con l'orientamento appropriato nel PCM.</span><span class="sxs-lookup"><span data-stu-id="15007-163">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="15007-164">Premere completamente il punto di manipolazione del modulo della batteria per alloggiare il connettore.</span><span class="sxs-lookup"><span data-stu-id="15007-164">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="15007-165">Sostituire il PCM nello chassis principale seguendo le linee guida descritte in [Sostituzione del modulo di alimentazione e raffreddamento nel dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="15007-165">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="15007-166">Dopo aver completato la sostituzione, passare al dispositivo e quindi a **Monitoraggio** > **Integrità hardware** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="15007-166">After the replacement is complete, go to your device and then go to **Monitor** > **Hardware health** in the Azure portal.</span></span> <span data-ttu-id="15007-167">Verificare lo stato della batteria per assicurarsi che l'installazione abbia avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="15007-167">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="15007-168">Uno stato verde indica che la batteria è integra.</span><span class="sxs-lookup"><span data-stu-id="15007-168">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="15007-169">Mantenimento del modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="15007-169">Maintain the backup battery module</span></span>
<span data-ttu-id="15007-170">Nel dispositivo StorSimple, il modulo della batteria di backup fornisce alimentazione al controller durante un evento di perdita dell'alimentazione.</span><span class="sxs-lookup"><span data-stu-id="15007-170">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="15007-171">Consente al dispositivo StorSimple di salvare i dati critici prima dell'arresto in modo controllato.</span><span class="sxs-lookup"><span data-stu-id="15007-171">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="15007-172">Con due batterie completamente cariche nei PCM, il sistema può gestire due eventi di perdita consecutivi.</span><span class="sxs-lookup"><span data-stu-id="15007-172">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="15007-173">Nel portale di Azure classico la voce **Integrità hardware** nel pannello **Monitoraggio** indica se la batteria non funziona correttamente o se si sta avvicinando la fine del ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="15007-173">In the Azure portal, the **Hardware health** under the **Monitor** blade indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="15007-174">Lo stato della batteria è indicato da **Batteria in PCM 0** o **Batteria in PCM 1** sotto **Componenti condivisi**.</span><span class="sxs-lookup"><span data-stu-id="15007-174">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="15007-175">In questo pannello viene visualizzato lo stato **DANNEGGIATO** per indicare l'avvicinarsi della fine del ciclo di vita e **NON RIUSCITO** per indicare che è stata raggiunta la fine del ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="15007-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="15007-176">La batteria può segnalare **NON RIUSCITO** quando è semplicemente necessario ricaricarla.</span><span class="sxs-lookup"><span data-stu-id="15007-176">The battery can report **FAILED** when it simply needs to be charged.</span></span>


<span data-ttu-id="15007-177">Se viene visualizzato lo stato **DANNEGGIATO** , è consigliabile adottare la linea di azione seguente:</span><span class="sxs-lookup"><span data-stu-id="15007-177">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="15007-178">Nel sistema potrebbe essersi verificata una perdita di alimentazione recente o le batterie potrebbero essere sottoposte alla manutenzione periodica.</span><span class="sxs-lookup"><span data-stu-id="15007-178">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="15007-179">Osservare il sistema per 12 ore prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="15007-179">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="15007-180">Se lo stato è ancora **DANNEGGIATO** dopo 12 ore di connessione continua all'alimentazione CA con i controller e i PCM in esecuzione, la batteria deve essere sostituita.</span><span class="sxs-lookup"><span data-stu-id="15007-180">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="15007-181">[Contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md) per un modulo della batteria di backup sostitutivo.</span><span class="sxs-lookup"><span data-stu-id="15007-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="15007-182">Se lo stato diventa OK dopo 12 ore, la batteria è operativa e necessitava soltanto di una ricarica di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="15007-182">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="15007-183">Se non si è verificata una perdita dell'alimentazione CA associata e il PCM è acceso e connesso all'alimentazione CA, la batteria deve essere sostituita.</span><span class="sxs-lookup"><span data-stu-id="15007-183">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="15007-184">[Contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md) per ordinare un modulo della batteria di backup sostitutivo.</span><span class="sxs-lookup"><span data-stu-id="15007-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15007-185">Smaltire la batteria guasta in conformità con le normative nazionali e regionali.</span><span class="sxs-lookup"><span data-stu-id="15007-185">Dispose of the failed battery according to national and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15007-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15007-186">Next steps</span></span>
<span data-ttu-id="15007-187">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="15007-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

