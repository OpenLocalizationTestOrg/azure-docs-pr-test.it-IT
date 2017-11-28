---
title: batteria aaaReplace in Microsoft Azure dispositivo StorSimple serie 8000 | Documenti Microsoft
description: Descrive come sostituire tooremove e mantenere hello modulo batteria di backup nel dispositivo StorSimple.
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
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="63f3b-103">Sostituire il modulo batteria di backup hello nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="63f3b-103">Replace hello backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="63f3b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="63f3b-104">Overview</span></span>
<span data-ttu-id="63f3b-105">enclosure principale Hello alimentazione e raffreddamento modulo PCM () sul dispositivo Microsoft Azure StorSimple è un gruppo batterie aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="63f3b-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="63f3b-106">Questo Service pack assicura l'alimentazione in modo che hello dispositivo StorSimple può salvare i dati nel caso di perdita di enclosure principale toohello di alimentazione CA.</span><span class="sxs-lookup"><span data-stu-id="63f3b-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="63f3b-107">Questo gruppo batterie sono hello tooas cui *modulo batteria di backup*.</span><span class="sxs-lookup"><span data-stu-id="63f3b-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="63f3b-108">modulo batteria di backup Hello esiste solo per l'enclosure principale di hello del dispositivo StorSimple (hello enclosure EBOD non contiene un modulo batteria di backup).</span><span class="sxs-lookup"><span data-stu-id="63f3b-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="63f3b-109">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="63f3b-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="63f3b-110">Rimuovere hello modulo batteria di backup</span><span class="sxs-lookup"><span data-stu-id="63f3b-110">Remove hello backup battery module</span></span>
* <span data-ttu-id="63f3b-111">Installare un nuovo modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="63f3b-111">Install a new backup battery module</span></span>
* <span data-ttu-id="63f3b-112">Gestisci hello modulo batteria di backup</span><span class="sxs-lookup"><span data-stu-id="63f3b-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63f3b-113">Prima di rimozione e sostituzione di un modulo batteria di backup, rivedere le informazioni sulla sicurezza hello in hello [sostituzione dei componenti hardware tooStorSimple Introduzione](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="63f3b-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="63f3b-114">Rimuovere hello modulo batteria di backup</span><span class="sxs-lookup"><span data-stu-id="63f3b-114">Remove hello backup battery module</span></span>
<span data-ttu-id="63f3b-115">Hello modulo batteria di backup per il dispositivo StorSimple è un'unità sostituibile sul campo.</span><span class="sxs-lookup"><span data-stu-id="63f3b-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="63f3b-116">Prima di installarla in hello PCM, il modulo di batteria hello deve essere conservato nella confezione originale.</span><span class="sxs-lookup"><span data-stu-id="63f3b-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="63f3b-117">Eseguire hello batteria di backup hello tooremove i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="63f3b-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="63f3b-118">modulo batteria di backup di hello tooremove</span><span class="sxs-lookup"><span data-stu-id="63f3b-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="63f3b-119">Nel portale di Azure hello, andare pannello servizio di gestione di dispositivi StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="63f3b-119">In hello Azure portal, go tooyour StorSimple Device Manager service blade.</span></span> <span data-ttu-id="63f3b-120">Andare troppo**dispositivi** e quindi selezionare il dispositivo dall'elenco hello dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="63f3b-120">Go too**Devices** and then select your device from hello list of devices.</span></span> <span data-ttu-id="63f3b-121">Passare troppo**monitoraggio** > **lo stato di Hardware**.</span><span class="sxs-lookup"><span data-stu-id="63f3b-121">Navigate too**Monitor** > **Hardware health**.</span></span> <span data-ttu-id="63f3b-122">In **componenti condivisi**, esaminare lo stato di hello di batteria hello.</span><span class="sxs-lookup"><span data-stu-id="63f3b-122">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="63f3b-123">Identificare il PCM hello in cui hello batteria non funzionante.</span><span class="sxs-lookup"><span data-stu-id="63f3b-123">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="63f3b-124">Figura 1 mostra hello parte posteriore di dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="63f3b-124">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="63f3b-126">**Figura 1** Parte posteriore del dispositivo principale in cui vengono mostrati il PCM e i moduli del controller</span><span class="sxs-lookup"><span data-stu-id="63f3b-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="63f3b-127">Etichetta</span><span class="sxs-lookup"><span data-stu-id="63f3b-127">Label</span></span> | <span data-ttu-id="63f3b-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63f3b-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="63f3b-129">1</span><span class="sxs-lookup"><span data-stu-id="63f3b-129">1</span></span> |<span data-ttu-id="63f3b-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="63f3b-130">PCM 0</span></span> |
   | <span data-ttu-id="63f3b-131">2</span><span class="sxs-lookup"><span data-stu-id="63f3b-131">2</span></span> |<span data-ttu-id="63f3b-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="63f3b-132">PCM 1</span></span> |
   | <span data-ttu-id="63f3b-133">3</span><span class="sxs-lookup"><span data-stu-id="63f3b-133">3</span></span> |<span data-ttu-id="63f3b-134">Controller 0</span><span class="sxs-lookup"><span data-stu-id="63f3b-134">Controller 0</span></span> |
   | <span data-ttu-id="63f3b-135">4</span><span class="sxs-lookup"><span data-stu-id="63f3b-135">4</span></span> |<span data-ttu-id="63f3b-136">Controller 1</span><span class="sxs-lookup"><span data-stu-id="63f3b-136">Controller 1</span></span> |
   
    <span data-ttu-id="63f3b-137">Come illustrato nella figura 2 hello numero 3, hello monitoraggio indicatore LED sul PCM 0 corrispondente troppo**guasto alla batteria** deve essere acceso.</span><span class="sxs-lookup"><span data-stu-id="63f3b-137">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Backplane degli indicatori LED di monitoraggio del PCM del dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="63f3b-139">**Figura 2** hello di parte posteriore del PCM con indicatori LED di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="63f3b-139">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="63f3b-140">Etichetta</span><span class="sxs-lookup"><span data-stu-id="63f3b-140">Label</span></span> | <span data-ttu-id="63f3b-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63f3b-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="63f3b-142">1</span><span class="sxs-lookup"><span data-stu-id="63f3b-142">1</span></span> |<span data-ttu-id="63f3b-143">Guasto dell’alimentazione CA</span><span class="sxs-lookup"><span data-stu-id="63f3b-143">AC power failure</span></span> |
   | <span data-ttu-id="63f3b-144">2</span><span class="sxs-lookup"><span data-stu-id="63f3b-144">2</span></span> |<span data-ttu-id="63f3b-145">Guasto alla ventola</span><span class="sxs-lookup"><span data-stu-id="63f3b-145">Fan failure</span></span> |
   | <span data-ttu-id="63f3b-146">3</span><span class="sxs-lookup"><span data-stu-id="63f3b-146">3</span></span> |<span data-ttu-id="63f3b-147">Guasto alla batteria</span><span class="sxs-lookup"><span data-stu-id="63f3b-147">Battery fault</span></span> |
   | <span data-ttu-id="63f3b-148">4</span><span class="sxs-lookup"><span data-stu-id="63f3b-148">4</span></span> |<span data-ttu-id="63f3b-149">PCM OK</span><span class="sxs-lookup"><span data-stu-id="63f3b-149">PCM OK</span></span> |
   | <span data-ttu-id="63f3b-150">5</span><span class="sxs-lookup"><span data-stu-id="63f3b-150">5</span></span> |<span data-ttu-id="63f3b-151">Guasto dell'alimentazione CC</span><span class="sxs-lookup"><span data-stu-id="63f3b-151">DC power failure</span></span> |
   | <span data-ttu-id="63f3b-152">6</span><span class="sxs-lookup"><span data-stu-id="63f3b-152">6</span></span> |<span data-ttu-id="63f3b-153">Integrità della batteria</span><span class="sxs-lookup"><span data-stu-id="63f3b-153">Battery healthy</span></span> |
3. <span data-ttu-id="63f3b-154">tooremove hello PCM con batteria non funzionante, seguire i passaggi hello [rimuovere un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="63f3b-154">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="63f3b-155">Con hello PCM rimosso, accuratezza e batteria hello ruota modulo gestire verso l'alto, come indicato nella seguente illustrazione hello ed estrarla batteria hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="63f3b-155">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Rimozione della batteria dal PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="63f3b-157">**Figura 3** rimozione hello batteria dal PCM hello</span><span class="sxs-lookup"><span data-stu-id="63f3b-157">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="63f3b-158">Inserire il modulo di hello in unità sostituibile sul campo di hello creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="63f3b-158">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="63f3b-159">Restituire hello unità difettosa tooMicrosoft per la gestione e manutenzione corretto.</span><span class="sxs-lookup"><span data-stu-id="63f3b-159">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="63f3b-160">Installare un nuovo modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="63f3b-160">Install a new backup battery module</span></span>
<span data-ttu-id="63f3b-161">Eseguire hello seguente modulo batteria sostitutivo passaggi tooinstall hello in hello PCM nell'enclosure principale di hello del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="63f3b-161">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="63f3b-162">modulo batteria di hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="63f3b-162">tooinstall hello battery module</span></span>
1. <span data-ttu-id="63f3b-163">Inserire l'orientamento corretto hello in hello PCM hello modulo batteria di backup.</span><span class="sxs-lookup"><span data-stu-id="63f3b-163">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="63f3b-164">Premere la freccia giù modulo batteria hello gestire connettore di hello tooseat hello modo tutti.</span><span class="sxs-lookup"><span data-stu-id="63f3b-164">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="63f3b-165">Sostituire hello PCM nell'enclosure principale hello seguendo le linee guida hello in [sostituire un Power and Cooling Module nel dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="63f3b-165">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="63f3b-166">Una volta completata la sostituzione hello, tooyour dispositivo quindi indirizzata e troppo**monitoraggio** > **lo stato di Hardware** in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="63f3b-166">After hello replacement is complete, go tooyour device and then go too**Monitor** > **Hardware health** in hello Azure portal.</span></span> <span data-ttu-id="63f3b-167">Verificare lo stato di hello di hello batteria toomake assicurarsi della corretta installazione hello.</span><span class="sxs-lookup"><span data-stu-id="63f3b-167">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="63f3b-168">Stato verde indica che la batteria hello è integra.</span><span class="sxs-lookup"><span data-stu-id="63f3b-168">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="63f3b-169">Gestisci hello modulo batteria di backup</span><span class="sxs-lookup"><span data-stu-id="63f3b-169">Maintain hello backup battery module</span></span>
<span data-ttu-id="63f3b-170">Nel dispositivo StorSimple hello modulo batteria di backup fornisce controller toohello power durante un evento di perdita di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="63f3b-170">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="63f3b-171">Consente di hello StorSimple dispositivo toosave dati critici precedente tooshutting verso il basso in modo controllato.</span><span class="sxs-lookup"><span data-stu-id="63f3b-171">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="63f3b-172">Con due batterie completamente in hello PCM, il sistema di hello può gestire due interruzioni consecutive della fornitura.</span><span class="sxs-lookup"><span data-stu-id="63f3b-172">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="63f3b-173">Nel portale di Azure hello, hello **lo stato di Hardware** in hello **monitoraggio** pannello indica se batteria hello non funziona correttamente o se si sta avvicinando hello ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="63f3b-173">In hello Azure portal, hello **Hardware health** under hello **Monitor** blade indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="63f3b-174">stato della batteria Hello è indicato da **batteria in PCM 0** o **batteria in PCM 1** in **componenti condivisi**.</span><span class="sxs-lookup"><span data-stu-id="63f3b-174">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="63f3b-175">In questo pannello viene visualizzato lo stato **DANNEGGIATO** per indicare l'avvicinarsi della fine del ciclo di vita e **NON RIUSCITO** per indicare che è stata raggiunta la fine del ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="63f3b-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="63f3b-176">batteria Hello può segnalare **FAILED** quando è necessario semplicemente toobe addebitati.</span><span class="sxs-lookup"><span data-stu-id="63f3b-176">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>


<span data-ttu-id="63f3b-177">Se hello **danneggiato** viene visualizzato lo stato, è consigliabile hello seguente linea di condotta:</span><span class="sxs-lookup"><span data-stu-id="63f3b-177">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="63f3b-178">sistema Hello che si sia verificata un'interruzione dell'alimentazione recente o batterie hello potrebbero essere in fase di manutenzione periodica.</span><span class="sxs-lookup"><span data-stu-id="63f3b-178">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="63f3b-179">Osservare il sistema hello per 12 ore prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="63f3b-179">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="63f3b-180">Se lo stato di hello è ancora **danneggiato** dopo 12 ore di energia elettrica tooAC connessione continua con hello controller e i PCM in esecuzione, quindi hello batteria deve toobe sostituito.</span><span class="sxs-lookup"><span data-stu-id="63f3b-180">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="63f3b-181">[Contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md) per un modulo della batteria di backup sostitutivo.</span><span class="sxs-lookup"><span data-stu-id="63f3b-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="63f3b-182">Se lo stato di hello diventa OK dopo 12 ore, hello batteria è operativa ed era soltanto necessario un costo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="63f3b-182">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="63f3b-183">Se non si è verificata un'interruzione di alimentazione e hello PCM è acceso e connesso power tooAC, toobe sostituito batteria hello.</span><span class="sxs-lookup"><span data-stu-id="63f3b-183">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="63f3b-184">[Contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md) tooorder un modulo batteria di backup sostitutivo.</span><span class="sxs-lookup"><span data-stu-id="63f3b-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63f3b-185">Dispose di hello non riuscita della batteria in base toonational e alle normative locali.</span><span class="sxs-lookup"><span data-stu-id="63f3b-185">Dispose of hello failed battery according toonational and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63f3b-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63f3b-186">Next steps</span></span>
<span data-ttu-id="63f3b-187">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="63f3b-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

