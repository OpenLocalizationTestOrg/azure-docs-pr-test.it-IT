---
title: dispositivo serie StorSimple 8000 aaaUse riepilogo | Documenti Microsoft
description: "Descrive dispositivo del servizio di gestione di dispositivi StorSimple hello riepilogo e in che modo toouse è tooview metriche di archiviazione e gli iniziatori connessi e trova hello numero di serie e IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="bf3ca-103">Usare dispositivo hello riepilogo nel servizio di gestione di dispositivi StorSimple</span><span class="sxs-lookup"><span data-stu-id="bf3ca-103">Use hello device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="bf3ca-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bf3ca-104">Overview</span></span>
<span data-ttu-id="bf3ca-105">Pannello riepilogo dispositivo StorSimple di Hello viene fornita una panoramica delle informazioni per un dispositivo StorSimple specifico, al contrario toohello servizio Pannello di riepilogo, che fornisce informazioni su tutti i dispositivi di hello inclusi nella soluzione StorSimple di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-105">hello StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast toohello service summary blade, which gives you information about all hello devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="bf3ca-106">Pannello riepilogo di Hello dispositivo fornisce un riepilogo di un dispositivo StorSimple serie 8000 registrato con un determinato StorSimple Manager di dispositivi, evidenziando i problemi dei dispositivi che richiedono attenzione da parte dell'amministratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-106">hello device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="bf3ca-107">In questa esercitazione presenta Pannello di riepilogo dispositivo hello, spiega (funzione) e il contenuto di hello e vengono descritte le attività di hello che è possibile eseguire questo pannello.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-107">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="bf3ca-108">Pannello riepilogo di Hello dispositivo Visualizza hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="bf3ca-108">hello device summary blade displays hello following information:</span></span>

![Pannello di riepilogo del dispositivo](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="bf3ca-110">Barra dei comandi di gestione</span><span class="sxs-lookup"><span data-stu-id="bf3ca-110">Management command bar</span></span>

<span data-ttu-id="bf3ca-111">Nel pannello dispositivo di StorSimple hello, vedrai opzioni hello per la gestione del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-111">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="bf3ca-112">Verranno visualizzati i comandi di gestione hello in alto di hello del pannello hello e sul lato sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-112">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="bf3ca-113">Usare queste opzioni tooadd condivisioni o volumi, aggiornare o eseguire il failover del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-113">Use these options tooadd shares or volumes, or update or fail over your device.</span></span>

![Barra dei comandi di gestione](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="bf3ca-115">Informazioni di base</span><span class="sxs-lookup"><span data-stu-id="bf3ca-115">Essentials</span></span>

<span data-ttu-id="bf3ca-116">area essentials Hello acquisisce alcune delle proprietà importanti di hello, ad esempio, stato hello, modello, nome qualificato iSCSI di destinazione e versione del software hello.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-116">hello essentials area captures some of hello important properties such as, hello status, model, target IQN, and hello software version.</span></span> 

![Informazioni di base sui dispositivi](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="bf3ca-118">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="bf3ca-118">Monitoring</span></span>

* <span data-ttu-id="bf3ca-119">Hello **avvisi** riquadro fornisce uno snapshot di tutti gli avvisi attivi hello per il dispositivo, raggruppato in base alla gravità dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-119">hello **Alerts** tile provides a snapshot of all hello active alerts for your device, grouped by alert severity.</span></span>

    ![Riquadro avvisi](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="bf3ca-121">Fare clic su hello di hello riquadro tooopen **avvisi** blade e quindi fare clic su un singolo avviso tooview ulteriori dettagli sull'avviso, inclusi eventuali azioni consigliate.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-121">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="bf3ca-122">È inoltre possibile cancellare avviso hello se hello problema è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-122">You can also clear hello alert if hello issue has been resolved.</span></span>

    ![Fare clic sul riquadro degli avvisi](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="bf3ca-124">Hello **stato e l'integrità** riquadro offre informazioni approfondite integrità hello del componente hardware per un dispositivo, inclusi lo stato del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-124">hello **Status and health** tile provides insights into hello hardware component health for a device including hello device status.</span></span> <span data-ttu-id="bf3ca-125">stato del dispositivo Hello può essere disattivato, pronto, online o offline tooset up.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-125">hello device status may be offline, online, deactivated, or ready tooset up.</span></span>

    ![Riquadro Stato e integrità](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="bf3ca-127">Hello **volumi** riquadro fornisce un riepilogo del numero di hello di volumi nel dispositivo raggruppati per stato.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-127">hello **Volumes** tile provides a summary of hello number of volumes in your device grouped by status.</span></span>

    ![Riquadro Volumi](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="bf3ca-129">Fare clic su hello di hello riquadro tooopen **volumi** elenco pannello, quindi fare clic su un singolo volume di tooview o modificarne le proprietà.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-129">Click hello tile tooopen hello **Volumes** list blade, and then click on an individual volume tooview or modify its properties.</span></span>
    
    ![Fare clic sul riquadro Volumi](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="bf3ca-131">Per ulteriori informazioni, vedere come troppo[gestire volumi](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="bf3ca-131">For more information, see how too[manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="bf3ca-132">In hello **utilizzo** grafico, è possibile visualizzare l'archiviazione primaria di hello usata tra il dispositivo e archiviazione cloud hello consumata in hello ultimi 7 giorni, il periodo di tempo predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-132">In hello **Usage** chart, you can view hello primary storage used across your device, and hello cloud storage consumed over hello past 7 days, hello default time period.</span></span>

     ![Riquadro Utilizzo](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="bf3ca-134">toochoose una scala temporale diverso, utilizzare hello **modifica** opzione nell'angolo superiore destro di hello del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-134">toochoose a different time scale, use hello **Edit** option in hello top-right corner of hello chart.</span></span>

     ![Modificare il grafico sull'utilizzo](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="bf3ca-136">In questo grafico, è possibile visualizzare le metriche di archiviazione primaria totale hello (quantità hello dei dati scritti dal dispositivo tooyour host) e hello totale usata dal dispositivo in un periodo di tempo di archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-136">In this chart, you can view metrics for hello total primary storage (hello amount of data written by hosts tooyour device) and hello total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="bf3ca-137">In questo contesto, *archiviazione primaria* fa riferimento toohello quantità totale di dati scritti dall'host hello e possono essere suddivisi per tipo di volume: *primario a livelli di archiviazione* include sia archiviati localmente i dati e i dati cloud toohello a più livelli.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-137">In this context, *primary storage* refers toohello total amount of data written by hello host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered toohello cloud.</span></span> <span data-ttu-id="bf3ca-138">mentre *archiviazione primaria aggiunta in locale* include solo i dati archiviati in locale.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="bf3ca-139">*Archiviazione cloud*, in hello invece, è una misura della quantità totale di hello dei dati archiviati nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-139">*Cloud storage*, on hello other hand, is a measurement of hello total amount of data stored in hello cloud.</span></span> <span data-ttu-id="bf3ca-140">Questo tipo di archiviazione include i backup e i dati a più livelli.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="bf3ca-141">dati Hello archiviati nel cloud hello sono deduplicati e compresso, mentre l'archiviazione primaria indica la quantità hello spazio di archiviazione utilizzato prima che i dati di hello sono deduplicati e compressi.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-141">hello data stored in hello cloud is deduplicated and compressed, whereas primary storage indicates hello amount of storage used before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="bf3ca-142">(È possibile confrontare questi tooget due numeri un'idea del tasso di compressione hello). Per entrambi primario e l'archiviazione, hello importi basati su rilevamento frequenza configurata hello cloud.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-142">(You can compare these two numbers tooget an idea of hello compression rate.) For both primary and cloud storage, hello amounts shown are based on hello tracking frequency you configure.</span></span> <span data-ttu-id="bf3ca-143">Ad esempio, se si sceglie una frequenza di una settimana, il grafico hello Mostra i dati per ogni giorno hello settimana precedente.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-143">For example, if you choose a one week frequency, then hello chart shows data for each day in hello previous week.</span></span>

     <span data-ttu-id="bf3ca-144">quantità di hello toosee di archiviazione cloud usato nel corso del tempo, seleziona hello **archiviazione CLOUD usata** opzione.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-144">toosee hello amount of cloud storage consumed over time, select hello **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="bf3ca-145">toosee hello spazio di archiviazione totale scritta dall'host di hello, seleziona hello **primario utilizzato archiviazione a livelli** e **primario locale aggiunto spazio di archiviazione usato** opzioni.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-145">toosee hello total storage that has been written by hello host, select hello **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="bf3ca-146">Per ulteriori informazioni, vedere [utilizzare hello toomonitor servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="bf3ca-146">For more information, see [Use hello StorSimple Device Manager service toomonitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="bf3ca-147">Hello **capacità** riquadro Visualizza hello primario spazio di archiviazione viene eseguito il provisioning e rimanente in hello dispositivo toohello relativo spazio di archiviazione totale disponibile per hello stesso.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-147">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="bf3ca-148">**Il provisioning** fa riferimento toohello quantità di spazio di archiviazione preparata e allocata per l'utilizzo, **rimanente** fa riferimento toohello residua che è possibile effettuare il provisioning in questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-148">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> 

    ![Riquadro Utilizzo](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="bf3ca-150">Fare clic su questo tooview riquadro come viene eseguito il provisioning della capacità di hello tra i volumi aggiunti in locale e a più livelli.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-150">Click this tile tooview how hello capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="bf3ca-151">Hello **a livelli rimanenti** capacità sia hello disponibile una capacità che è possibile effettuare il provisioning inclusi cloud, mentre hello **rimanenti locale** capacità hello rimanente su dischi hello collegato toothis dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bf3ca-151">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis device.</span></span>

    ![Fare clic sul grafico Utilizzo](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="bf3ca-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf3ca-153">Next steps</span></span>
* <span data-ttu-id="bf3ca-154">Altre informazioni su hello [Pannello di riepilogo del servizio StorSimple](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="bf3ca-154">Learn more about hello [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="bf3ca-155">Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bf3ca-155">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

