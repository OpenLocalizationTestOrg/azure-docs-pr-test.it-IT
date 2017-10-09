---
title: chassis aaaReplace nel dispositivo StorSimple serie 8000 | Documenti Microsoft
description: Viene descritto come tooremove e sostituire hello chassis per l'enclosure principale StorSimple o enclosure EBOD.
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
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="9d4bb-103">Sostituzione dello chassis hello nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="9d4bb-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="9d4bb-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9d4bb-104">Overview</span></span>
<span data-ttu-id="9d4bb-105">In questa esercitazione viene illustrato come tooremove e sostituire uno chassis in un dispositivo StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="9d4bb-106">modello Hello StorSimple 8100 è un dispositivo a enclosure singola (uno chassis), mentre hello 8600 è un dispositivo a doppia enclosure (due chassis).</span><span class="sxs-lookup"><span data-stu-id="9d4bb-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="9d4bb-107">Per un modello 8600, esistono potenzialmente due chassis che potrebbe non riuscire in dispositivo hello: hello chassis per enclosure principale hello o chassis hello hello enclosure EBOD.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="9d4bb-108">In entrambi i casi chassis sostitutivo hello è fornito da Microsoft è vuoto.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="9d4bb-109">Non verranno inclusi PCM, moduli controller, unità disco a stato solido (SSD), unità disco rigido (HDD) o moduli EBOD.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d4bb-110">Prima di rimozione e sostituzione dello chassis hello, esaminare le informazioni di sicurezza hello in [sostituzione dei componenti hardware StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="9d4bb-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-chassis"></a><span data-ttu-id="9d4bb-111">Rimuovere hello chassis</span><span class="sxs-lookup"><span data-stu-id="9d4bb-111">Remove hello chassis</span></span>
<span data-ttu-id="9d4bb-112">Eseguire hello seguente chassis hello tooremove di passaggi nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="9d4bb-113">tooremove uno chassis</span><span class="sxs-lookup"><span data-stu-id="9d4bb-113">tooremove a chassis</span></span>
1. <span data-ttu-id="9d4bb-114">Verificare che il dispositivo StorSimple hello è spento e scollegato dalla fonte di alimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="9d4bb-115">Rimuovere tutti i cavi SAS e rete hello, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="9d4bb-116">Rimuovere l'unità di hello dal rack hello.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="9d4bb-117">Rimuovere ciascun nome dell'unità hello e prendere nota di slot hello da cui vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="9d4bb-118">Per ulteriori informazioni, vedere [rimuovere l'unità disco hello](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="9d4bb-118">For more information, see [Remove hello disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="9d4bb-119">In hello enclosure EBOD (se si tratta di chassis hello non riuscita), rimuovere i moduli controller EBOD di hello.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="9d4bb-120">Per ulteriori informazioni, vedere [Rimuovere un controller EBOD](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="9d4bb-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="9d4bb-121">In hello enclosure principale (se si tratta dello chassis hello non riuscita), rimuovere i controller hello e prendere nota di slot hello da cui vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="9d4bb-122">Per ulteriori informazioni, vedere [Rimuovere un controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="9d4bb-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="9d4bb-123">Installare hello chassis</span><span class="sxs-lookup"><span data-stu-id="9d4bb-123">Install hello chassis</span></span>
<span data-ttu-id="9d4bb-124">Eseguire hello seguente chassis hello tooinstall di passaggi nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="9d4bb-125">tooinstall uno chassis</span><span class="sxs-lookup"><span data-stu-id="9d4bb-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="9d4bb-126">Montare su rack hello chassis hello.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="9d4bb-127">Per altre informazioni, vedere [Montare su rack il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) o [Montare su rack il dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="9d4bb-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="9d4bb-128">Dopo aver hello montato nel rack hello, installare i moduli controller hello nelle hello che stesso posizioni che sono stati installati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="9d4bb-129">Installazione hello unità in hello stesso posiziona e slot che sono stati installati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d4bb-130">È consigliabile installare prima unità SSD hello negli slot hello e quindi installare hello HDD.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
  
4. <span data-ttu-id="9d4bb-131">Dispositivo hello montato nel rack hello e installati componenti di hello, connettersi fonti di alimentazione appropriate toohello il dispositivo e accendere il dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9d4bb-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="9d4bb-132">Per i dettagli, vedere [Cablare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) o [Cablare il dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="9d4bb-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d4bb-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d4bb-133">Next steps</span></span>
<span data-ttu-id="9d4bb-134">Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="9d4bb-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

