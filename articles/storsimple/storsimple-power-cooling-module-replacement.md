---
title: un PCM nel dispositivo StorSimple aaaReplace | Documenti Microsoft
description: Viene illustrato come tooremove e sostituire hello Power e modulo di raffreddamento (PCM) nel dispositivo StorSimple
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
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="8da39-103">Sostituzione di un modulo di alimentazione e raffreddamento nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="8da39-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="8da39-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8da39-104">Overview</span></span>
<span data-ttu-id="8da39-105">Hello alimentazione e raffreddamento modulo PCM () nel dispositivo Microsoft Azure StorSimple costituito da un alimentatore e raffreddamento controllati tramite hello primario e l'enclosure EBOD.</span><span class="sxs-lookup"><span data-stu-id="8da39-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="8da39-106">Esiste un solo modello di PCM certificato per ciascuno chassis.</span><span class="sxs-lookup"><span data-stu-id="8da39-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="8da39-107">enclosure principale Hello è certificata per un PCM a 764 W ed enclosure EBOD hello è certificata per un PCM a 580 W.</span><span class="sxs-lookup"><span data-stu-id="8da39-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="8da39-108">Anche se hello PCM enclosure principale hello e hello dell'enclosure EBOD sono diversi, la procedura di sostituzione hello è identica.</span><span class="sxs-lookup"><span data-stu-id="8da39-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="8da39-109">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="8da39-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="8da39-110">Rimuovere un PCM</span><span class="sxs-lookup"><span data-stu-id="8da39-110">Remove a PCM</span></span>
* <span data-ttu-id="8da39-111">Installare un PCM sostitutivo</span><span class="sxs-lookup"><span data-stu-id="8da39-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8da39-112">Prima di rimozione e sostituzione di un PCM, esaminare le informazioni di sicurezza hello in [sostituzione dei componenti hardware StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8da39-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="8da39-113">Prima di sostituire un PCM:</span><span class="sxs-lookup"><span data-stu-id="8da39-113">Before you replace a PCM</span></span>
<span data-ttu-id="8da39-114">Tenere hello seguenti problemi importanti prima di sostituire il PCM:</span><span class="sxs-lookup"><span data-stu-id="8da39-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="8da39-115">Alimentatore hello di hello guasto PCM, lasciare hello modulo non funzionante installato, ma rimuovere il cavo di alimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="8da39-116">ventola Hello continuerà alimentazione tooreceive enclosure hello e continuare tooprovide corretto raffreddamento.</span><span class="sxs-lookup"><span data-stu-id="8da39-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="8da39-117">Se ha esito negativo della ventola hello, hello PCM deve toobe sostituito immediatamente.</span><span class="sxs-lookup"><span data-stu-id="8da39-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="8da39-118">Prima di rimuovere hello PCM, scollegare hello alimentazione hello PCM disattivando interruttore hello (se presente) o rimuovendo il cavo di alimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="8da39-119">Ciò fornisce un sistema di tooyour di avviso che è imminente interruzione dell'alimentazione.</span><span class="sxs-lookup"><span data-stu-id="8da39-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="8da39-120">Verificare che tale hello che è funzionale per l'altro PCM costantemente il funzionamento del sistema prima di sostituire hello PCM non funzionante.</span><span class="sxs-lookup"><span data-stu-id="8da39-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="8da39-121">Un PCM guasto deve essere sostituito con un PCM completamente funzionante appena possibile.</span><span class="sxs-lookup"><span data-stu-id="8da39-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="8da39-122">Sostituzione di un modulo PCM richiede solo pochi minuti toocomplete, ma deve essere completata entro 10 minuti dalla rimozione non riuscita hello PCM tooprevent surriscaldamento.</span><span class="sxs-lookup"><span data-stu-id="8da39-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="8da39-123">Si noti che hello sostituzione 764 W i moduli PCM forniti dalla factory hello non contengano hello modulo batteria di backup.</span><span class="sxs-lookup"><span data-stu-id="8da39-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="8da39-124">Sarà anche necessario batteria hello tooremove dal PCM non funzionante e quindi inserirla sostituzione hello di hello sostituzione modulo tooperforming precedente.</span><span class="sxs-lookup"><span data-stu-id="8da39-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="8da39-125">Per ulteriori informazioni, vedere come troppo[rimuovere e inserire un modulo batteria di backup](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8da39-125">For more information, see how too[remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="8da39-126">Rimuovere un PCM</span><span class="sxs-lookup"><span data-stu-id="8da39-126">Remove a PCM</span></span>
<span data-ttu-id="8da39-127">Quando si è pronti tooremove una potenza e modulo di raffreddamento (PCM) dal dispositivo di Microsoft Azure StorSimple, seguire queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="8da39-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="8da39-128">Prima di rimuovere il PCM, verificare di disporre di un componente sostitutivo corretto (764 W per l'enclosure principale hello) o 580 W per hello enclosure EBOD.</span><span class="sxs-lookup"><span data-stu-id="8da39-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>
> 
> 

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="8da39-129">tooremove un PCM</span><span class="sxs-lookup"><span data-stu-id="8da39-129">tooremove a PCM</span></span>
1. <span data-ttu-id="8da39-130">Nel portale di Azure classico hello, fare clic su **dispositivi** > **manutenzione** > **stato Hardware**.</span><span class="sxs-lookup"><span data-stu-id="8da39-130">In hello Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="8da39-131">Controllare lo stato di hello dei componenti PCM hello sotto **componenti condivisi** tooidentify quello non funzionante:</span><span class="sxs-lookup"><span data-stu-id="8da39-131">Check hello status of hello PCM components under **Shared Components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="8da39-132">Se un alimentatore in PCM 0 non è riuscita, hello stato **alimentatore in PCM 0** sarà di colore rosso.</span><span class="sxs-lookup"><span data-stu-id="8da39-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="8da39-133">Se un alimentatore in PCM 1 non è riuscita, hello stato **alimentatore in PCM 1** sarà di colore rosso.</span><span class="sxs-lookup"><span data-stu-id="8da39-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="8da39-134">Se la ventola hello in PCM 1 non è riuscita, hello indicatore di stato del **raffreddamento 0 PCM 0** o **raffreddamento 1 PCM 0** sarà di colore rosso.</span><span class="sxs-lookup"><span data-stu-id="8da39-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="8da39-135">Individuare hello PCM non funzionante in hello eseguire il backup dell'enclosure principale hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="8da39-136">Se si esegue un modello 8600, identificare l'enclosure principale hello esaminando hello mostrato sul display LED sul pannello anteriore hello numero identificativo dell'unità del sistema.</span><span class="sxs-lookup"><span data-stu-id="8da39-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="8da39-137">Hello predefinito visualizzato sull'enclosure principale hello è **00**, mentre il valore predefinito di hello ID di unità visualizzate nella hello enclosure EBOD è **01**.</span><span class="sxs-lookup"><span data-stu-id="8da39-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="8da39-138">Hello diagramma e la tabella seguenti illustrano pannello anteriore di hello del display LED hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![ID del sistema sul pannello anteriore delle operazioni](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="8da39-140">**Figura 1** pannello anteriore del dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="8da39-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="8da39-141">Etichetta</span><span class="sxs-lookup"><span data-stu-id="8da39-141">Label</span></span> | <span data-ttu-id="8da39-142">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8da39-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="8da39-143">1</span><span class="sxs-lookup"><span data-stu-id="8da39-143">1</span></span> |<span data-ttu-id="8da39-144">Pulsante di disattivazione audio</span><span class="sxs-lookup"><span data-stu-id="8da39-144">Mute button</span></span> |
   | <span data-ttu-id="8da39-145">2</span><span class="sxs-lookup"><span data-stu-id="8da39-145">2</span></span> |<span data-ttu-id="8da39-146">Alimentazione del sistema</span><span class="sxs-lookup"><span data-stu-id="8da39-146">System power</span></span> |
   | <span data-ttu-id="8da39-147">3</span><span class="sxs-lookup"><span data-stu-id="8da39-147">3</span></span> |<span data-ttu-id="8da39-148">Errore del modulo</span><span class="sxs-lookup"><span data-stu-id="8da39-148">Module fault</span></span> |
   | <span data-ttu-id="8da39-149">4</span><span class="sxs-lookup"><span data-stu-id="8da39-149">4</span></span> |<span data-ttu-id="8da39-150">Errore logico</span><span class="sxs-lookup"><span data-stu-id="8da39-150">Logical fault</span></span> |
   | <span data-ttu-id="8da39-151">5</span><span class="sxs-lookup"><span data-stu-id="8da39-151">5</span></span> |<span data-ttu-id="8da39-152">Display ID unità</span><span class="sxs-lookup"><span data-stu-id="8da39-152">Unit ID display</span></span> |
3. <span data-ttu-id="8da39-153">può essere utilizzato anche il monitoraggio di indicatori LED di hello parte posteriore dell'enclosure principale hello Hello tooidentify hello PCM non funzionante.</span><span class="sxs-lookup"><span data-stu-id="8da39-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="8da39-154">Vedere hello seguente diagramma e tabella come toounderstand toouse hello LED toolocate hello PCM non funzionante.</span><span class="sxs-lookup"><span data-stu-id="8da39-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="8da39-155">Ad esempio, se hello LED corrispondente toohello **guasto ventola** è acceso, significa che la ventola hello non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="8da39-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="8da39-156">Analogamente, se hello LED corrispondente troppo**guasto AC** è acceso, significa che alimentatore hello non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="8da39-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![Backplane degli indicatori LED di monitoraggio del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="8da39-158">**Figura 2** Parte posteriore del PCM con i LED degli indicatori</span><span class="sxs-lookup"><span data-stu-id="8da39-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="8da39-159">Etichetta</span><span class="sxs-lookup"><span data-stu-id="8da39-159">Label</span></span> | <span data-ttu-id="8da39-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8da39-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="8da39-161">1</span><span class="sxs-lookup"><span data-stu-id="8da39-161">1</span></span> |<span data-ttu-id="8da39-162">Guasto dell’alimentazione CA</span><span class="sxs-lookup"><span data-stu-id="8da39-162">AC power failure</span></span> |
   | <span data-ttu-id="8da39-163">2</span><span class="sxs-lookup"><span data-stu-id="8da39-163">2</span></span> |<span data-ttu-id="8da39-164">Guasto alla ventola</span><span class="sxs-lookup"><span data-stu-id="8da39-164">Fan failure</span></span> |
   | <span data-ttu-id="8da39-165">3</span><span class="sxs-lookup"><span data-stu-id="8da39-165">3</span></span> |<span data-ttu-id="8da39-166">Guasto alla batteria</span><span class="sxs-lookup"><span data-stu-id="8da39-166">Battery fault</span></span> |
   | <span data-ttu-id="8da39-167">4</span><span class="sxs-lookup"><span data-stu-id="8da39-167">4</span></span> |<span data-ttu-id="8da39-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="8da39-168">PCM OK</span></span> |
   | <span data-ttu-id="8da39-169">5</span><span class="sxs-lookup"><span data-stu-id="8da39-169">5</span></span> |<span data-ttu-id="8da39-170">Guasto dell'alimentazione CC</span><span class="sxs-lookup"><span data-stu-id="8da39-170">DC power failure</span></span> |
   | <span data-ttu-id="8da39-171">6</span><span class="sxs-lookup"><span data-stu-id="8da39-171">6</span></span> |<span data-ttu-id="8da39-172">Integrità della batteria</span><span class="sxs-lookup"><span data-stu-id="8da39-172">Battery healthy</span></span> |
4. <span data-ttu-id="8da39-173">Fare riferimento toohello seguente diagramma di hello parte posteriore modulo PCM di hello StorSimple dispositivo toolocate hello non riuscita.</span><span class="sxs-lookup"><span data-stu-id="8da39-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="8da39-174">PCM 0 si trova a sinistra di hello e PCM 1 è hello destra.</span><span class="sxs-lookup"><span data-stu-id="8da39-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="8da39-175">tabella Hello che segue vengono illustrati i moduli di hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-175">hello table that follows explains hello modules.</span></span>
   
     ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="8da39-177">**Figura 3** Parte posteriore del dispositivo con moduli plug-in</span><span class="sxs-lookup"><span data-stu-id="8da39-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="8da39-178">Etichetta</span><span class="sxs-lookup"><span data-stu-id="8da39-178">Label</span></span> | <span data-ttu-id="8da39-179">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8da39-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="8da39-180">1</span><span class="sxs-lookup"><span data-stu-id="8da39-180">1</span></span> |<span data-ttu-id="8da39-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="8da39-181">PCM 0</span></span> |
   | <span data-ttu-id="8da39-182">2</span><span class="sxs-lookup"><span data-stu-id="8da39-182">2</span></span> |<span data-ttu-id="8da39-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="8da39-183">PCM 1</span></span> |
   | <span data-ttu-id="8da39-184">3</span><span class="sxs-lookup"><span data-stu-id="8da39-184">3</span></span> |<span data-ttu-id="8da39-185">Controller 0</span><span class="sxs-lookup"><span data-stu-id="8da39-185">Controller 0</span></span> |
   | <span data-ttu-id="8da39-186">4</span><span class="sxs-lookup"><span data-stu-id="8da39-186">4</span></span> |<span data-ttu-id="8da39-187">Controller 1</span><span class="sxs-lookup"><span data-stu-id="8da39-187">Controller 1</span></span> |
5. <span data-ttu-id="8da39-188">Attivare off hello PCM non funzionante e scollegare cavo di alimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="8da39-189">È possibile rimuovere hello PCM.</span><span class="sxs-lookup"><span data-stu-id="8da39-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="8da39-190">Afferrare latch hello e lato hello di hello gestire PCM tra il pollice e l'indice, quindi premerli handle hello tooopen insieme.</span><span class="sxs-lookup"><span data-stu-id="8da39-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![Apertura del punto di manipolazione del PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="8da39-192">**Figura 4** gestire hello apertura PCM</span><span class="sxs-lookup"><span data-stu-id="8da39-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="8da39-193">Tirare la maniglia hello e rimuovere hello PCM.</span><span class="sxs-lookup"><span data-stu-id="8da39-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![Rimozione del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="8da39-195">**Figura 5** rimozione hello PCM</span><span class="sxs-lookup"><span data-stu-id="8da39-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="8da39-196">Installare un PCM sostitutivo</span><span class="sxs-lookup"><span data-stu-id="8da39-196">Install a replacement PCM</span></span>
<span data-ttu-id="8da39-197">Seguire questi tooinstall istruzioni un PCM del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8da39-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="8da39-198">Assicurarsi di avere inserito hello batteria di backup precedenti tooinstalling hello sostituzione di un modulo PCM (si applica solo PCM W too764).</span><span class="sxs-lookup"><span data-stu-id="8da39-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="8da39-199">Per ulteriori informazioni, vedere come troppo[rimuovere e inserire un modulo batteria di backup](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8da39-199">For more information, see how too[remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="8da39-200">tooinstall un PCM</span><span class="sxs-lookup"><span data-stu-id="8da39-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="8da39-201">Verificare di aver hello PCM sostitutivo appropriato per questa enclosure.</span><span class="sxs-lookup"><span data-stu-id="8da39-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="8da39-202">enclosure principale di Hello richiede un PCM a 764 W e hello enclosure EBOD deve un PCM a 580 W.</span><span class="sxs-lookup"><span data-stu-id="8da39-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="8da39-203">Non è consigliabile tentare toouse hello PCM a 580 W enclosure principale hello o hello PCM 764 W in hello enclosure EBOD.</span><span class="sxs-lookup"><span data-stu-id="8da39-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="8da39-204">Hello seguente immagine mostra se queste informazioni in hello etichetta ovvero tooidentify apposta toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="8da39-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![Etichetta del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="8da39-206">**Figura 6** Etichetta del PCM</span><span class="sxs-lookup"><span data-stu-id="8da39-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="8da39-207">Controllare per enclosure toohello danni, prestando particolare attenzione toohello connettori.</span><span class="sxs-lookup"><span data-stu-id="8da39-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8da39-208">**Se qualsiasi connettore presenta pin piegati, non installare il modulo di hello.**</span><span class="sxs-lookup"><span data-stu-id="8da39-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="8da39-209">Con hello PCM gestire nel hello aprire posizione, il modulo hello diapositiva in enclosure hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![Installazione del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="8da39-211">**Figura 7** installazione hello PCM</span><span class="sxs-lookup"><span data-stu-id="8da39-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="8da39-212">Chiudere manualmente maniglia del PCM hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="8da39-213">Quando hello handle fermo scatta, si sente un clic.</span><span class="sxs-lookup"><span data-stu-id="8da39-213">You should hear a click as hello handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8da39-214">si sono impegnati tooensure che hello pin dei connettori, è possibile tirare leggermente hello handle senza rilascio del latch hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="8da39-215">Se hello PCM scorre verso l'esterno, significa che il latch hello è stata chiusa prima hello connettori venissero inseriti.</span><span class="sxs-lookup"><span data-stu-id="8da39-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="8da39-216">Connettere hello cavi toohello power alimentazione e toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="8da39-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="8da39-217">Proteggere ceppo hello Balle rilievo.</span><span class="sxs-lookup"><span data-stu-id="8da39-217">Secure hello strain relief bales.</span></span> 
7. <span data-ttu-id="8da39-218">Attivare hello PCM.</span><span class="sxs-lookup"><span data-stu-id="8da39-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="8da39-219">Verifica della corretta sostituzione hello: nel portale di Azure classico del servizio StorSimple Manager hello, passare troppo**dispositivi** > **manutenzione**  >  **Stato hardware**.</span><span class="sxs-lookup"><span data-stu-id="8da39-219">Verify that hello replacement was successful: in hello Azure classic portal of your StorSimple Manager service, navigate too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="8da39-220">In **componenti condivisi**, stato hello di hello PCM deve essere di colore verde.</span><span class="sxs-lookup"><span data-stu-id="8da39-220">Under **Shared Components**, hello status of hello PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8da39-221">Potrebbe richiedere alcuni minuti per l'inizializzazione di toocompletely PCM sostitutivo hello.</span><span class="sxs-lookup"><span data-stu-id="8da39-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="8da39-222">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8da39-222">Next steps</span></span>
<span data-ttu-id="8da39-223">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8da39-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

