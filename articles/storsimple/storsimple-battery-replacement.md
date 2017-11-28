---
title: batteria aaaReplace nel dispositivo StorSimple di Microsoft Azure | Documenti Microsoft
description: Descrive come sostituire tooremove e mantenere hello modulo batteria di backup nel dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="c26b9-103">Sostituire il modulo batteria di backup hello nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="c26b9-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="c26b9-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c26b9-104">Overview</span></span>
<span data-ttu-id="c26b9-105">enclosure principale Hello alimentazione e raffreddamento modulo PCM () sul dispositivo Microsoft Azure StorSimple è un gruppo batterie aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="c26b9-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="c26b9-106">Questo Service pack assicura l'alimentazione in modo che hello dispositivo StorSimple può salvare i dati nel caso di perdita di enclosure principale toohello di alimentazione CA.</span><span class="sxs-lookup"><span data-stu-id="c26b9-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="c26b9-107">Questo gruppo batterie sono hello tooas cui *modulo batteria di backup*.</span><span class="sxs-lookup"><span data-stu-id="c26b9-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="c26b9-108">modulo batteria di backup Hello esiste solo per l'enclosure principale di hello del dispositivo StorSimple (hello enclosure EBOD non contiene un modulo batteria di backup).</span><span class="sxs-lookup"><span data-stu-id="c26b9-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="c26b9-109">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="c26b9-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="c26b9-110">Rimuovere hello modulo batteria di backup</span><span class="sxs-lookup"><span data-stu-id="c26b9-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="c26b9-111">Installare un nuovo modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="c26b9-111">Install a new backup battery module</span></span>
* <span data-ttu-id="c26b9-112">Gestisci hello modulo batteria di backup</span><span class="sxs-lookup"><span data-stu-id="c26b9-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c26b9-113">Prima di rimozione e sostituzione di un modulo batteria di backup, rivedere le informazioni sulla sicurezza hello in hello [sostituzione dei componenti hardware tooStorSimple Introduzione](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="c26b9-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="c26b9-114">Rimuovere hello modulo batteria di backup</span><span class="sxs-lookup"><span data-stu-id="c26b9-114">Remove hello backup battery module</span></span>
<span data-ttu-id="c26b9-115">Hello modulo batteria di backup per il dispositivo StorSimple è un'unità sostituibile sul campo.</span><span class="sxs-lookup"><span data-stu-id="c26b9-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="c26b9-116">Prima di installarla in hello PCM, il modulo di batteria hello deve essere conservato nella confezione originale.</span><span class="sxs-lookup"><span data-stu-id="c26b9-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="c26b9-117">Eseguire hello batteria di backup hello tooremove i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="c26b9-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="c26b9-118">modulo batteria di backup di hello tooremove</span><span class="sxs-lookup"><span data-stu-id="c26b9-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="c26b9-119">Nel portale di Azure classico hello, andare troppo**dispositivi** > **manutenzione** > **stato Hardware**.</span><span class="sxs-lookup"><span data-stu-id="c26b9-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="c26b9-120">In **componenti condivisi**, esaminare lo stato di hello di batteria hello.</span><span class="sxs-lookup"><span data-stu-id="c26b9-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="c26b9-121">Identificare il PCM hello in cui hello batteria non funzionante.</span><span class="sxs-lookup"><span data-stu-id="c26b9-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="c26b9-122">Figura 1 mostra hello parte posteriore di dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="c26b9-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="c26b9-124">**Figura 1** Parte posteriore del dispositivo principale in cui vengono mostrati il PCM e i moduli del controller</span><span class="sxs-lookup"><span data-stu-id="c26b9-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="c26b9-125">Etichetta</span><span class="sxs-lookup"><span data-stu-id="c26b9-125">Label</span></span> | <span data-ttu-id="c26b9-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c26b9-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c26b9-127">1</span><span class="sxs-lookup"><span data-stu-id="c26b9-127">1</span></span> |<span data-ttu-id="c26b9-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="c26b9-128">PCM 0</span></span> |
   | <span data-ttu-id="c26b9-129">2</span><span class="sxs-lookup"><span data-stu-id="c26b9-129">2</span></span> |<span data-ttu-id="c26b9-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="c26b9-130">PCM 1</span></span> |
   | <span data-ttu-id="c26b9-131">3</span><span class="sxs-lookup"><span data-stu-id="c26b9-131">3</span></span> |<span data-ttu-id="c26b9-132">Controller 0</span><span class="sxs-lookup"><span data-stu-id="c26b9-132">Controller 0</span></span> |
   | <span data-ttu-id="c26b9-133">4</span><span class="sxs-lookup"><span data-stu-id="c26b9-133">4</span></span> |<span data-ttu-id="c26b9-134">Controller 1</span><span class="sxs-lookup"><span data-stu-id="c26b9-134">Controller 1</span></span> |
   
    <span data-ttu-id="c26b9-135">Come illustrato nella figura 2 hello numero 3, hello monitoraggio indicatore LED sul PCM 0 corrispondente troppo**guasto alla batteria** deve essere acceso.</span><span class="sxs-lookup"><span data-stu-id="c26b9-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Backplane degli indicatori LED di monitoraggio del PCM del dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="c26b9-137">**Figura 2** hello di parte posteriore del PCM con indicatori LED di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="c26b9-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="c26b9-138">Etichetta</span><span class="sxs-lookup"><span data-stu-id="c26b9-138">Label</span></span> | <span data-ttu-id="c26b9-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c26b9-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c26b9-140">1</span><span class="sxs-lookup"><span data-stu-id="c26b9-140">1</span></span> |<span data-ttu-id="c26b9-141">Guasto dell’alimentazione CA</span><span class="sxs-lookup"><span data-stu-id="c26b9-141">AC power failure</span></span> |
   | <span data-ttu-id="c26b9-142">2</span><span class="sxs-lookup"><span data-stu-id="c26b9-142">2</span></span> |<span data-ttu-id="c26b9-143">Guasto alla ventola</span><span class="sxs-lookup"><span data-stu-id="c26b9-143">Fan failure</span></span> |
   | <span data-ttu-id="c26b9-144">3</span><span class="sxs-lookup"><span data-stu-id="c26b9-144">3</span></span> |<span data-ttu-id="c26b9-145">Guasto alla batteria</span><span class="sxs-lookup"><span data-stu-id="c26b9-145">Battery fault</span></span> |
   | <span data-ttu-id="c26b9-146">4</span><span class="sxs-lookup"><span data-stu-id="c26b9-146">4</span></span> |<span data-ttu-id="c26b9-147">PCM OK</span><span class="sxs-lookup"><span data-stu-id="c26b9-147">PCM OK</span></span> |
   | <span data-ttu-id="c26b9-148">5</span><span class="sxs-lookup"><span data-stu-id="c26b9-148">5</span></span> |<span data-ttu-id="c26b9-149">Guasto dell'alimentazione CC</span><span class="sxs-lookup"><span data-stu-id="c26b9-149">DC power failure</span></span> |
   | <span data-ttu-id="c26b9-150">6</span><span class="sxs-lookup"><span data-stu-id="c26b9-150">6</span></span> |<span data-ttu-id="c26b9-151">Integrità della batteria</span><span class="sxs-lookup"><span data-stu-id="c26b9-151">Battery healthy</span></span> |
3. <span data-ttu-id="c26b9-152">tooremove hello PCM con batteria non funzionante, seguire i passaggi hello [rimuovere un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="c26b9-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="c26b9-153">Con hello PCM rimosso, accuratezza e batteria hello ruota modulo gestire verso l'alto, come indicato nella seguente illustrazione hello ed estrarla batteria hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="c26b9-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Rimozione della batteria dal PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="c26b9-155">**Figura 3** rimozione hello batteria dal PCM hello</span><span class="sxs-lookup"><span data-stu-id="c26b9-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="c26b9-156">Inserire il modulo di hello in unità sostituibile sul campo di hello creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c26b9-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="c26b9-157">Restituire hello unità difettosa tooMicrosoft per la gestione e manutenzione corretto.</span><span class="sxs-lookup"><span data-stu-id="c26b9-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="c26b9-158">Installare un nuovo modulo della batteria di backup</span><span class="sxs-lookup"><span data-stu-id="c26b9-158">Install a new backup battery module</span></span>
<span data-ttu-id="c26b9-159">Eseguire hello seguente modulo batteria sostitutivo passaggi tooinstall hello in hello PCM nell'enclosure principale di hello del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c26b9-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="c26b9-160">modulo batteria di hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="c26b9-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="c26b9-161">Inserire l'orientamento corretto hello in hello PCM hello modulo batteria di backup.</span><span class="sxs-lookup"><span data-stu-id="c26b9-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="c26b9-162">Premere la freccia giù modulo batteria hello gestire connettore di hello tooseat hello modo tutti.</span><span class="sxs-lookup"><span data-stu-id="c26b9-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="c26b9-163">Sostituire hello PCM nell'enclosure principale hello seguendo le linee guida hello in [sostituire un Power and Cooling Module nel dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="c26b9-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="c26b9-164">Una volta completata la sostituzione hello, andare troppo**dispositivi** > **manutenzione** > **stato Hardware** nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="c26b9-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="c26b9-165">Verificare lo stato di hello di hello batteria toomake assicurarsi della corretta installazione hello.</span><span class="sxs-lookup"><span data-stu-id="c26b9-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="c26b9-166">Stato verde indica che la batteria hello è integra.</span><span class="sxs-lookup"><span data-stu-id="c26b9-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="c26b9-167">Gestisci hello modulo batteria di backup</span><span class="sxs-lookup"><span data-stu-id="c26b9-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="c26b9-168">Nel dispositivo StorSimple hello modulo batteria di backup fornisce controller toohello power durante un evento di perdita di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="c26b9-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="c26b9-169">Consente di hello StorSimple dispositivo toosave dati critici precedente tooshutting verso il basso in modo controllato.</span><span class="sxs-lookup"><span data-stu-id="c26b9-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="c26b9-170">Con due batterie completamente in hello PCM, il sistema di hello può gestire due interruzioni consecutive della fornitura.</span><span class="sxs-lookup"><span data-stu-id="c26b9-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="c26b9-171">Nel portale di Azure classico hello, hello **stato Hardware** su hello **manutenzione** pagina indica se batteria hello non funziona correttamente o se si sta avvicinando hello ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="c26b9-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="c26b9-172">stato della batteria Hello è indicato da **batteria in PCM 0** o **batteria in PCM 1** in **componenti condivisi**.</span><span class="sxs-lookup"><span data-stu-id="c26b9-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="c26b9-173">In questa pagina verrà visualizzato lo stato **DANNEGGIATO** per indicare l'avvicinarsi della fine del ciclo di vita e **NON RIUSCITO** per indicare che è stata raggiunta la fine del ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="c26b9-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="c26b9-174">batteria Hello può segnalare **FAILED** quando è necessario semplicemente toobe addebitati.</span><span class="sxs-lookup"><span data-stu-id="c26b9-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="c26b9-175">Se hello **danneggiato** viene visualizzato lo stato, è consigliabile hello seguente linea di condotta:</span><span class="sxs-lookup"><span data-stu-id="c26b9-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="c26b9-176">sistema Hello che si sia verificata un'interruzione dell'alimentazione recente o batterie hello potrebbero essere in fase di manutenzione periodica.</span><span class="sxs-lookup"><span data-stu-id="c26b9-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="c26b9-177">Osservare il sistema hello per 12 ore prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="c26b9-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="c26b9-178">Se lo stato di hello è ancora **danneggiato** dopo 12 ore di energia elettrica tooAC connessione continua con hello controller e i PCM in esecuzione, quindi hello batteria deve toobe sostituito.</span><span class="sxs-lookup"><span data-stu-id="c26b9-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="c26b9-179">[Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) per un modulo della batteria di backup sostitutivo.</span><span class="sxs-lookup"><span data-stu-id="c26b9-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="c26b9-180">Se lo stato di hello diventa OK dopo 12 ore, hello batteria è operativa ed era soltanto necessario un costo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="c26b9-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="c26b9-181">Se non si è verificata un'interruzione di alimentazione e hello PCM è acceso e connesso power tooAC, toobe sostituito batteria hello.</span><span class="sxs-lookup"><span data-stu-id="c26b9-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="c26b9-182">[Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) tooorder un modulo batteria di backup sostitutivo.</span><span class="sxs-lookup"><span data-stu-id="c26b9-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c26b9-183">Dispose di hello non riuscita della batteria in base toonational e alle normative locali.</span><span class="sxs-lookup"><span data-stu-id="c26b9-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c26b9-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c26b9-184">Next steps</span></span>
<span data-ttu-id="c26b9-185">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="c26b9-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

