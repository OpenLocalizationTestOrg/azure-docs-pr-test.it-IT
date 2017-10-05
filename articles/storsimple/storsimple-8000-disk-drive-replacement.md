---
title: "Sostituire un'unità disco nel dispositivo StorSimple serie 8000 | Microsoft Docs"
description: "Viene illustrato come sostituire un'unità disco in uno chassis principale StorSimple o in uno chassis EBOD."
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
ms.openlocfilehash: bb259b626ecd4dcbaa8f1c465f1ece4516aa8881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="41de0-103">Sostituire un'unità disco del dispositivo StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="41de0-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="41de0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="41de0-104">Overview</span></span>
<span data-ttu-id="41de0-105">In questa esercitazione viene illustrato come rimuovere e sostituire un'unità disco rigido che non funziona correttamente o guasta in un dispositivo Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41de0-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="41de0-106">Per sostituire un'unità disco, è necessario:</span><span class="sxs-lookup"><span data-stu-id="41de0-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="41de0-107">Disattivare il blocco antimanomissione</span><span class="sxs-lookup"><span data-stu-id="41de0-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="41de0-108">Rimuovere l'unità disco</span><span class="sxs-lookup"><span data-stu-id="41de0-108">Remove the disk drive</span></span>
* <span data-ttu-id="41de0-109">Installare l'unità disco sostitutiva</span><span class="sxs-lookup"><span data-stu-id="41de0-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41de0-110">Prima di rimuovere e sostituire un'unità disco, esaminare le informazioni di sicurezza descritte in [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="41de0-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="41de0-111">Disattivare il blocco antimanomissione</span><span class="sxs-lookup"><span data-stu-id="41de0-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="41de0-112">In questa procedura viene illustrato come i blocchi antimanomissione sul dispositivo StorSimple possono essere attivati o disattivati quando si sostituiscono le unità disco.</span><span class="sxs-lookup"><span data-stu-id="41de0-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="41de0-113">I blocchi antimanomissione vengono montati nei punti di manipolazione del supporto dell'unità e sono accessibili attraverso una piccola apertura nella sezione chiavistello del punto di manipolazione.</span><span class="sxs-lookup"><span data-stu-id="41de0-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="41de0-114">Le unità vengono fornite con i blocchi impostati sulla posizione bloccata.</span><span class="sxs-lookup"><span data-stu-id="41de0-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="41de0-115">Per sbloccare il blocco antimanomissione:</span><span class="sxs-lookup"><span data-stu-id="41de0-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="41de0-116">Inserire la chiave di blocco (un cacciavite "a prova di manomissione" T10 fornito da Microsoft) con attenzione nell'apertura del punto di manipolazione e nel relativo socket.</span><span class="sxs-lookup"><span data-stu-id="41de0-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   <span data-ttu-id="41de0-117">Se il blocco antimanomissione è attivato, l'indicatore rosso è visibile nell'apertura.</span><span class="sxs-lookup"><span data-stu-id="41de0-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
  
    ![Unità disco bloccata](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="41de0-119">**Figura 1** Blocco antimanomissione attivato</span><span class="sxs-lookup"><span data-stu-id="41de0-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="41de0-120">Etichetta</span><span class="sxs-lookup"><span data-stu-id="41de0-120">Label</span></span> | <span data-ttu-id="41de0-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="41de0-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="41de0-122">1</span><span class="sxs-lookup"><span data-stu-id="41de0-122">1</span></span> |<span data-ttu-id="41de0-123">Apertura indicatore</span><span class="sxs-lookup"><span data-stu-id="41de0-123">Indicator aperture</span></span> |
   | <span data-ttu-id="41de0-124">2</span><span class="sxs-lookup"><span data-stu-id="41de0-124">2</span></span> |<span data-ttu-id="41de0-125">Blocco antimanomissione</span><span class="sxs-lookup"><span data-stu-id="41de0-125">Antitamper lock</span></span> |
2. <span data-ttu-id="41de0-126">Ruotare la chiave in senso antiorario fino a quando l'indicatore rosso non è visibile nell'apertura sopra la chiave.</span><span class="sxs-lookup"><span data-stu-id="41de0-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="41de0-127">Rimuovere la chiave.</span><span class="sxs-lookup"><span data-stu-id="41de0-127">Remove the key.</span></span>
   
    ![Unità disco sbloccata](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="41de0-129">**Figura 2** Unità disco sbloccata</span><span class="sxs-lookup"><span data-stu-id="41de0-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="41de0-130">È ora possibile rimuovere l'unità disco.</span><span class="sxs-lookup"><span data-stu-id="41de0-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="41de0-131">Seguire i passaggi in ordine inverso per attivare il blocco.</span><span class="sxs-lookup"><span data-stu-id="41de0-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="41de0-132">Rimuovere l'unità disco</span><span class="sxs-lookup"><span data-stu-id="41de0-132">Remove the disk drive</span></span>
<span data-ttu-id="41de0-133">Il dispositivo StorSimple supporta la configurazione degli spazi di archiviazione di tipo RAID 10.</span><span class="sxs-lookup"><span data-stu-id="41de0-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="41de0-134">Ciò implica che può funzionare normalmente con un'unità a stato solido (SSD), un'unità disco rigido (HDD) o un disco guasto.</span><span class="sxs-lookup"><span data-stu-id="41de0-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="41de0-135">Se più di un disco nel sistema è guasto, non rimuovere più di un'unità SSD o HDD dal sistema in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="41de0-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="41de0-136">Ciò potrebbe causare una perdita dei dati.</span><span class="sxs-lookup"><span data-stu-id="41de0-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="41de0-137">Assicurarsi di inserire un'unità SSD sostitutiva in uno slot che in precedenza conteneva un'unità SSD.</span><span class="sxs-lookup"><span data-stu-id="41de0-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="41de0-138">Analogamente, inserire un'unità HDD sostitutiva in uno slot che in precedenza conteneva un'unità HDD.</span><span class="sxs-lookup"><span data-stu-id="41de0-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="41de0-139">Nel portale di Azure, gli slot sono numerati da 0 a 11.</span><span class="sxs-lookup"><span data-stu-id="41de0-139">In the Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="41de0-140">Pertanto, se nel portale viene mostrato che un disco nello slot 2 è guasto, sul dispositivo, cercare il disco guasto nel terzo slot dalla parte superiore sinistra.</span><span class="sxs-lookup"><span data-stu-id="41de0-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="41de0-141">Le unità possono essere rimosse e sostituite durante il funzionamento del sistema.</span><span class="sxs-lookup"><span data-stu-id="41de0-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="41de0-142">Per rimuovere un'unità:</span><span class="sxs-lookup"><span data-stu-id="41de0-142">To remove a drive</span></span>
1. <span data-ttu-id="41de0-143">Per identificare il disco guasto, nel portale di Azure, passare al panello **Impostazioni > Integrità hardware** del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41de0-143">To identify the failed disk, in the Azure portal, go to your device **Settings > Hardware health**.</span></span> <span data-ttu-id="41de0-144">Poiché un disco può presentare un guasto allo chassis principale e/o a uno chassis EBOD (se si usa un modello 8600), controllare lo stato dei dischi sotto **Componenti condivisi** e **EBOD enclosure Shared Components** (Componenti condivisi dello chassis EBOD).</span><span class="sxs-lookup"><span data-stu-id="41de0-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="41de0-145">Un disco guasto verrà visualizzato con uno stato rosso in entrambi gli chassis.</span><span class="sxs-lookup"><span data-stu-id="41de0-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="41de0-146">Individuare le unità nella parte anteriori dello chassis principale o dello chassis EBOD.</span><span class="sxs-lookup"><span data-stu-id="41de0-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="41de0-147">Se il disco è sbloccato, procedere al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="41de0-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="41de0-148">Se il disco è bloccato, sbloccarlo seguendo la procedura descritta in [Disattivazione del blocco antimanomissione](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="41de0-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="41de0-149">Premere il chiavistello nero sul modulo del supporto dell'unità e rimuovere il punto di manipolazione del supporto dell'unità dalla parte anteriore dello chassis.</span><span class="sxs-lookup"><span data-stu-id="41de0-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span>
   
    ![Rilascio del punto di manipolazione dell'unità disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="41de0-151">**Figura 3** Rilascio del punto di manipolazione dell'unità</span><span class="sxs-lookup"><span data-stu-id="41de0-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="41de0-152">Quando il punto di manipolazione del supporto dell'unità è completamente esteso, far scorrere il supporto dell'unità fuori dallo chassis.</span><span class="sxs-lookup"><span data-stu-id="41de0-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Scorrimento del disco fuori dall'unità disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="41de0-154">**Figura 4** Scorrimento dell'unità disco fuori dal supporto</span><span class="sxs-lookup"><span data-stu-id="41de0-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="41de0-155">Installare l'unità disco sostitutiva</span><span class="sxs-lookup"><span data-stu-id="41de0-155">Install the replacement disk drive</span></span>
<span data-ttu-id="41de0-156">Dopo aver rimosso un'unità guasta nel dispositivo StorSimple, seguire questa procedura per sostituirla con una nuova unità.</span><span class="sxs-lookup"><span data-stu-id="41de0-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="41de0-157">Per inserire un'unità:</span><span class="sxs-lookup"><span data-stu-id="41de0-157">To insert a drive</span></span>
1. <span data-ttu-id="41de0-158">Assicurarsi che il punto di manipolazione del supporto dell'unità sia completamente esteso, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="41de0-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![Unità disco con punto di manipolazione esteso](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="41de0-160">**Figura 5** Unità con punto di manipolazione esteso</span><span class="sxs-lookup"><span data-stu-id="41de0-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="41de0-161">Far scorrere il supporto dell'unità completamente nello chassis.</span><span class="sxs-lookup"><span data-stu-id="41de0-161">Slide the drive carrier all the way into the chassis.</span></span>
   
    ![Scorrimento del disco nel supporto dell'unità disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="41de0-163">**Figura 6** Scorrimento del supporto dell'unità nello chassis</span><span class="sxs-lookup"><span data-stu-id="41de0-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="41de0-164">Con il supporto dell'unità inserito, chiudere il punto di manipolazione del supporto dell'unità continuando a spingere il supporto dell'unità nello chassis, fino a quando il punto di manipolazione del supporto dell'unità non si chiude a scatto in una posizione bloccata.</span><span class="sxs-lookup"><span data-stu-id="41de0-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="41de0-165">Utilizzare la chiave di blocco fornita da Microsoft (cacciavite Torx a prova di manomissione) per fissare in posizione il punto di manipolazione del supporto girando la vite di blocco di un quarto in senso orario.</span><span class="sxs-lookup"><span data-stu-id="41de0-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="41de0-166">Verificare che la sostituzione sia riuscita e che l'unità sia operativa.</span><span class="sxs-lookup"><span data-stu-id="41de0-166">Verify that the replacement was successful and the drive is operational.</span></span> <span data-ttu-id="41de0-167">Accedere al portale di Azure e passare a **Impostazioni** > **Integrità hardware**.</span><span class="sxs-lookup"><span data-stu-id="41de0-167">Access the Azure portal and navigate to **Settings** > **Hardware health**.</span></span> <span data-ttu-id="41de0-168">In **Componenti condivisi** o **Componenti condivisi EBOD** , lo stato dell'unità deve essere verde, ovvero integro.</span><span class="sxs-lookup"><span data-stu-id="41de0-168">Under **Shared components** or **EBOD shared components**, the drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="41de0-169">Potrebbero essere necessarie diverse ore affinché lo stato del disco diventi verde dopo la sostituzione.</span><span class="sxs-lookup"><span data-stu-id="41de0-169">It may take several hours for the disk status to turn green after the replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="41de0-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41de0-170">Next steps</span></span>
<span data-ttu-id="41de0-171">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="41de0-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

