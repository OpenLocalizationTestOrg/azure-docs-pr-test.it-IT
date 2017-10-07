---
title: "un'unità disco in un dispositivo StorSimple serie 8000 aaaReplace | Documenti Microsoft"
description: "Viene illustrato come unità di tooreplace un disco in un'enclosure EBOD o di una enclosure principale StorSimple."
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
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="0ca33-103">Sostituire un'unità disco del dispositivo StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="0ca33-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="0ca33-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0ca33-104">Overview</span></span>
<span data-ttu-id="0ca33-105">In questa esercitazione viene illustrato come rimuovere e sostituire un'unità disco rigido che non funziona correttamente o guasta in un dispositivo Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0ca33-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="0ca33-106">tooreplace un'unità disco, è necessario:</span><span class="sxs-lookup"><span data-stu-id="0ca33-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="0ca33-107">Disattivare antimanomissione hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="0ca33-108">Rimuovere l'unità disco hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-108">Remove hello disk drive</span></span>
* <span data-ttu-id="0ca33-109">Installare il disco sostitutivo hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ca33-110">Prima di rimozione e sostituzione di un'unità disco, esaminare le informazioni di sicurezza hello in [sostituzione dei componenti hardware StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="0ca33-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="0ca33-111">Disattivare antimanomissione hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="0ca33-112">Questa procedura illustra come possono essere occupati o non innestate quando si sostituiscono le unità disco hello chiusure antimanomissione di hello nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0ca33-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="0ca33-113">chiusure antimanomissione Hello sono montati in hello unità vettore handle e vi si accede tramite una piccola apertura nel fermo hello dell'handle hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="0ca33-114">Le unità vengono fornite con blocchi hello imposta la posizione toohello bloccato.</span><span class="sxs-lookup"><span data-stu-id="0ca33-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="0ca33-115">chiusura antimanomissione hello toounlock</span><span class="sxs-lookup"><span data-stu-id="0ca33-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="0ca33-116">Inserire delicatamente chiave hello (un cacciavite T10 "chiusura" fornito da Microsoft) nell'apertura hello hello maniglia e nel relativo attacco.</span><span class="sxs-lookup"><span data-stu-id="0ca33-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   <span data-ttu-id="0ca33-117">Se è attivata antimanomissione hello, indicatore rosso hello è visibile nell'apertura hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
  
    ![Unità disco bloccata](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="0ca33-119">**Figura 1** Blocco antimanomissione attivato</span><span class="sxs-lookup"><span data-stu-id="0ca33-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="0ca33-120">Etichetta</span><span class="sxs-lookup"><span data-stu-id="0ca33-120">Label</span></span> | <span data-ttu-id="0ca33-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0ca33-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0ca33-122">1</span><span class="sxs-lookup"><span data-stu-id="0ca33-122">1</span></span> |<span data-ttu-id="0ca33-123">Apertura indicatore</span><span class="sxs-lookup"><span data-stu-id="0ca33-123">Indicator aperture</span></span> |
   | <span data-ttu-id="0ca33-124">2</span><span class="sxs-lookup"><span data-stu-id="0ca33-124">2</span></span> |<span data-ttu-id="0ca33-125">Blocco antimanomissione</span><span class="sxs-lookup"><span data-stu-id="0ca33-125">Antitamper lock</span></span> |
2. <span data-ttu-id="0ca33-126">Chiave di hello Ruota in senso antiorario finché l'indicatore rosso hello non è visibile nell'apertura di hello sopra hello chiave.</span><span class="sxs-lookup"><span data-stu-id="0ca33-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="0ca33-127">Rimuovere la chiave hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-127">Remove hello key.</span></span>
   
    ![Unità disco sbloccata](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="0ca33-129">**Figura 2** Unità disco sbloccata</span><span class="sxs-lookup"><span data-stu-id="0ca33-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="0ca33-130">è ora possibile rimuovere l'unità disco Hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="0ca33-131">Seguire i passaggi di hello in blocco hello tooengage inversa.</span><span class="sxs-lookup"><span data-stu-id="0ca33-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="0ca33-132">Rimuovere l'unità disco hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-132">Remove hello disk drive</span></span>
<span data-ttu-id="0ca33-133">Il dispositivo StorSimple supporta la configurazione degli spazi di archiviazione di tipo RAID 10.</span><span class="sxs-lookup"><span data-stu-id="0ca33-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="0ca33-134">Ciò implica che può funzionare normalmente con un'unità a stato solido (SSD), un'unità disco rigido (HDD) o un disco guasto.</span><span class="sxs-lookup"><span data-stu-id="0ca33-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="0ca33-135">Se il sistema dispone di più di un disco danneggiato, non rimuovere più di una unità SSD o HDD dal sistema hello in qualsiasi punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="0ca33-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="0ca33-136">Ciò potrebbe causare una perdita dei dati.</span><span class="sxs-lookup"><span data-stu-id="0ca33-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="0ca33-137">Assicurarsi di inserire un'unità SSD sostitutiva in uno slot che in precedenza conteneva un'unità SSD.</span><span class="sxs-lookup"><span data-stu-id="0ca33-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="0ca33-138">Analogamente, inserire un'unità HDD sostitutiva in uno slot che in precedenza conteneva un'unità HDD.</span><span class="sxs-lookup"><span data-stu-id="0ca33-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="0ca33-139">Nel portale di Azure hello, gli slot sono numerati da 0 a 11.</span><span class="sxs-lookup"><span data-stu-id="0ca33-139">In hello Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="0ca33-140">Pertanto, se il portale di hello mostra che un disco nello slot 2 non riuscita, sul dispositivo hello, cercare hello disco nel terzo slot hello hello in alto a sinistra.</span><span class="sxs-lookup"><span data-stu-id="0ca33-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="0ca33-141">Unità possono essere rimosse e sostituite mentre sistema hello è operativo.</span><span class="sxs-lookup"><span data-stu-id="0ca33-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="0ca33-142">tooremove un'unità</span><span class="sxs-lookup"><span data-stu-id="0ca33-142">tooremove a drive</span></span>
1. <span data-ttu-id="0ca33-143">disco, in hello portale di Azure andare tooyour dispositivo non riuscita di hello tooidentify **Impostazioni > lo stato di Hardware**.</span><span class="sxs-lookup"><span data-stu-id="0ca33-143">tooidentify hello failed disk, in hello Azure portal, go tooyour device **Settings > Hardware health**.</span></span> <span data-ttu-id="0ca33-144">Poiché può avere esito negativo di un disco nell'enclosure principale hello e/o in un'enclosure EBOD (se si utilizza un modello 8600), esaminare lo stato di hello di dischi hello in **dei componenti condivisi di** e in **componenti condivisi EBOD** .</span><span class="sxs-lookup"><span data-stu-id="0ca33-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="0ca33-145">Un disco guasto verrà visualizzato con uno stato rosso in entrambi gli chassis.</span><span class="sxs-lookup"><span data-stu-id="0ca33-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="0ca33-146">Individuare l'unità di hello nella parte anteriore hello di enclosure principale hello o enclosure EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="0ca33-147">Se il disco di hello è sbloccato, continuare toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="0ca33-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="0ca33-148">Se il disco di hello è bloccato, sbloccarlo seguendo la procedura hello in [disattivare antimanomissione hello](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="0ca33-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="0ca33-149">Premere hello nero latch nel modulo di gestione delle spedizioni di hello unità e tirare maniglia di hello verso l'esterno dalla parte anteriore hello dello chassis hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span>
   
    ![Rilascio del punto di manipolazione dell'unità disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="0ca33-151">**Figura 3** rilascio dell'handle dell'unità hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="0ca33-152">Quando maniglia di hello sia estesa completamente, far scorrere estraibile hello esterno dello chassis hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Scorrimento del disco fuori dall'unità disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="0ca33-154">**Figura 4** scorrimento all'unità disco hello fuori vettore hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="0ca33-155">Installare il disco sostitutivo hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="0ca33-156">Dopo aver rimosso un'unità non è riuscito nel dispositivo StorSimple, seguire questa tooreplace procedura con una nuova unità.</span><span class="sxs-lookup"><span data-stu-id="0ca33-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="0ca33-157">tooinsert un'unità</span><span class="sxs-lookup"><span data-stu-id="0ca33-157">tooinsert a drive</span></span>
1. <span data-ttu-id="0ca33-158">Assicurarsi maniglia di hello sia estesa completamente, come mostrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![Unità disco con punto di manipolazione esteso](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="0ca33-160">**Figura 5** Unità con punto di manipolazione esteso</span><span class="sxs-lookup"><span data-stu-id="0ca33-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="0ca33-161">Diapositiva estraibile hello modo hello tutti nello chassis hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-161">Slide hello drive carrier all hello way into hello chassis.</span></span>
   
    ![Scorrimento del disco nel supporto dell'unità disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="0ca33-163">**Figura 6** estendibile supporto estraibile hello nello chassis hello</span><span class="sxs-lookup"><span data-stu-id="0ca33-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="0ca33-164">Con hello vettore hello inserito, chiudere unità maniglia durante la continuazione toopush hello estraibile nello chassis di hello, fino a quando non hello maniglia scatta in posizione di blocco.</span><span class="sxs-lookup"><span data-stu-id="0ca33-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="0ca33-165">Tasto BLOC hello utilizzare fornita da maniglia a Microsoft (chiusura cacciavite Torx) toosecure hello in posizione ruotando vite hello un quarto di giro in senso orario.</span><span class="sxs-lookup"><span data-stu-id="0ca33-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="0ca33-166">Verificare che la sostituzione hello ha avuto esito positivo e hello unità sia operativa.</span><span class="sxs-lookup"><span data-stu-id="0ca33-166">Verify that hello replacement was successful and hello drive is operational.</span></span> <span data-ttu-id="0ca33-167">Accesso hello portale di Azure e la navigazione troppo**impostazioni** > **lo stato di Hardware**.</span><span class="sxs-lookup"><span data-stu-id="0ca33-167">Access hello Azure portal and navigate too**Settings** > **Hardware health**.</span></span> <span data-ttu-id="0ca33-168">In **dei componenti condivisi di** o **componenti condivisi EBOD**, lo stato di unità hello deve essere verde, che indica che è integro.</span><span class="sxs-lookup"><span data-stu-id="0ca33-168">Under **Shared components** or **EBOD shared components**, hello drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="0ca33-169">Può richiedere diverse ore hello disco stato tooturn verde dopo la sostituzione di hello.</span><span class="sxs-lookup"><span data-stu-id="0ca33-169">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="0ca33-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0ca33-170">Next steps</span></span>
<span data-ttu-id="0ca33-171">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="0ca33-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

