---
title: Sostituire lo chassis in un dispositivo StorSimple serie 8000| Microsoft Docs
description: Descrive come rimuovere e sostituire lo chassis per l'alloggiamento principale o EBOD di StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5295c5dd039b1d4746ebaaf90372932e4c3e7c26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a><span data-ttu-id="b8bf9-103">Sostituire lo chassis sul dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="b8bf9-103">Replace the chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="b8bf9-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b8bf9-104">Overview</span></span>
<span data-ttu-id="b8bf9-105">Questa esercitazione illustra come rimuovere e sostituire uno chassis in un dispositivo StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="b8bf9-106">Il modello 8100 di StorSimple è un dispositivo a chassis singolo (uno chassis), mentre il modello 8600 è un dispositivo a chassis doppio (due chassis).</span><span class="sxs-lookup"><span data-stu-id="b8bf9-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="b8bf9-107">Per un modello 8600, esistono potenzialmente due chassis che potrebbero avere esito negativo nel dispositivo: lo chassis per lo chassis principale o lo chassis per lo chassis EBOD.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span></span>

<span data-ttu-id="b8bf9-108">In entrambi i casi, lo chassis sostitutivo che viene fornito da Microsoft è vuoto.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="b8bf9-109">Non verranno inclusi PCM, moduli controller, unità disco a stato solido (SSD), unità disco rigido (HDD) o moduli EBOD.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8bf9-110">Prima di rimuovere e sostituire lo chassis, esaminare le informazioni di sicurezza descritte in [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b8bf9-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-chassis"></a><span data-ttu-id="b8bf9-111">Rimuovere lo chassis</span><span class="sxs-lookup"><span data-stu-id="b8bf9-111">Remove the chassis</span></span>
<span data-ttu-id="b8bf9-112">Eseguire i passaggi seguenti per rimuovere lo chassis sul dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-112">Perform the following steps to remove the chassis on your StorSimple device.</span></span>

#### <a name="to-remove-a-chassis"></a><span data-ttu-id="b8bf9-113">Per rimuovere uno chassis</span><span class="sxs-lookup"><span data-stu-id="b8bf9-113">To remove a chassis</span></span>
1. <span data-ttu-id="b8bf9-114">Assicurarsi che il dispositivo StorSimple sia arrestato e disconnesso da tutte le origini di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span></span>
2. <span data-ttu-id="b8bf9-115">Rimuovere tutti i cavi di rete e SAS, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-115">Remove all the network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="b8bf9-116">Rimuovere l'unità dal rack.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-116">Remove the unit from the rack.</span></span>
4. <span data-ttu-id="b8bf9-117">Rimuovere ciascuna unità e annotare gli slot da cui vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-117">Remove each of the drives and note the slots from which they are removed.</span></span> <span data-ttu-id="b8bf9-118">Per ulteriori informazioni, vedere [Rimuovere l'unità disco](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="b8bf9-118">For more information, see [Remove the disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="b8bf9-119">Nell'enclosure EBOD (se si tratta di chassis non riuscito), rimuovere i moduli controller EBOD.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span></span> <span data-ttu-id="b8bf9-120">Per ulteriori informazioni, vedere [Rimuovere un controller EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="b8bf9-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="b8bf9-121">Nell’enclosure principale (se si tratta di chassis non riuscito), rimuovere i controller e annotare gli slot da cui vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span></span> <span data-ttu-id="b8bf9-122">Per ulteriori informazioni, vedere [Rimuovere un controller](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="b8bf9-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-the-chassis"></a><span data-ttu-id="b8bf9-123">Installare lo chassis</span><span class="sxs-lookup"><span data-stu-id="b8bf9-123">Install the chassis</span></span>
<span data-ttu-id="b8bf9-124">Eseguire i passaggi seguenti per installare lo chassis sul dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-124">Perform the following steps to install the chassis on your StorSimple device.</span></span>

#### <a name="to-install-a-chassis"></a><span data-ttu-id="b8bf9-125">Per installare uno chassis</span><span class="sxs-lookup"><span data-stu-id="b8bf9-125">To install a chassis</span></span>
1. <span data-ttu-id="b8bf9-126">Montare lo chassis nel rack.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-126">Mount the chassis in the rack.</span></span> <span data-ttu-id="b8bf9-127">Per altre informazioni, vedere [Montare su rack il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) o [Montare su rack il dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="b8bf9-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="b8bf9-128">Dopo il montaggio dello chassis nel rack, installare i moduli controller nelle stesse posizioni in cui erano precedentemente installati.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="b8bf9-129">Installare le unità nelle stesse posizioni e slot in cui erano precedentemente installati.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-129">Install the drives in the same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b8bf9-130">È consigliabile installare prima le unità SSD negli slot e quindi installare i dischi rigidi.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="b8bf9-131">Con il dispositivo montato nel rack e i componenti installati, connettere il dispositivo alle appropriate prese di corrente e accendere il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b8bf9-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span></span> <span data-ttu-id="b8bf9-132">Per i dettagli, vedere [Cablare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) o [Cablare il dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="b8bf9-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8bf9-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8bf9-133">Next steps</span></span>
<span data-ttu-id="b8bf9-134">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b8bf9-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

