---
title: Usare il riepilogo per dispositivi StorSimple serie 8000 | Microsoft Docs
description: Descrive il riepilogo del dispositivo del servizio Gestione dispositivi StorSimple e illustra come usarlo per visualizzare le metriche di archiviazione e gli iniziatori connessi e trovare il numero di serie e il nome qualificato iSCSI.
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
ms.openlocfilehash: 784d3ce9d8f926b00ac1c6fbf48a05c0b04f900a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="5dd9c-103">Usare il riepilogo del dispositivo nel servizio Gestione dispositivi StorSimple</span><span class="sxs-lookup"><span data-stu-id="5dd9c-103">Use the device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="5dd9c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5dd9c-104">Overview</span></span>
<span data-ttu-id="5dd9c-105">Il pannello di riepilogo del dispositivo StorSimple offre una panoramica delle informazioni per un determinato dispositivo StorSimple, a differenza del pannello di riepilogo del servizio, che fornisce informazioni su tutti i dispositivi inclusi nella soluzione Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-105">The StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast to the service summary blade, which gives you information about all the devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="5dd9c-106">Il pannello di riepilogo del dispositivo offre una vista di riepilogo di un dispositivo StorSimple serie 8000 registrato con un servizio Gestione dispositivi StorSimple, in modo da evidenziare eventuali problemi del dispositivo che richiedono attenzione da parte dell'amministratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-106">The device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="5dd9c-107">Questa esercitazione introduce il pannello di riepilogo del dispositivo, illustra il contenuto e la funzione e descrive le attività che è possibile eseguire da questo pannello.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-107">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="5dd9c-108">Il pannello di riepilogo dispositivo contiene le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5dd9c-108">The device summary blade displays the following information:</span></span>

![Pannello di riepilogo del dispositivo](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="5dd9c-110">Barra dei comandi di gestione</span><span class="sxs-lookup"><span data-stu-id="5dd9c-110">Management command bar</span></span>

<span data-ttu-id="5dd9c-111">Il pannello del dispositivo StorSimple contiene le opzioni per la gestione del dispositivo StorSimple in uso.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-111">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="5dd9c-112">I comandi per la gestione vengono visualizzati nella parte superiore del pannello e sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-112">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="5dd9c-113">Usare queste opzioni per aggiungere condivisioni o volumi o per aggiornare o eseguire il failover del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-113">Use these options to add shares or volumes, or update or fail over your device.</span></span>

![Barra dei comandi di gestione](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="5dd9c-115">Informazioni di base</span><span class="sxs-lookup"><span data-stu-id="5dd9c-115">Essentials</span></span>

<span data-ttu-id="5dd9c-116">L'area relativa alle informazioni di base riporta alcune proprietà importanti, ad esempio lo stato, il modello, il nome qualificato iSCSI del dispositivo di destinazione e la versione del software.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-116">The essentials area captures some of the important properties such as, the status, model, target IQN, and the software version.</span></span> 

![Informazioni di base sui dispositivi](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="5dd9c-118">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="5dd9c-118">Monitoring</span></span>

* <span data-ttu-id="5dd9c-119">Il riquadro **Avvisi** offre uno snapshot di tutti gli avvisi attivi per il dispositivo, raggruppati in base alla gravità.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-119">The **Alerts** tile provides a snapshot of all the active alerts for your device, grouped by alert severity.</span></span>

    ![Riquadro avvisi](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="5dd9c-121">Fare clic sul riquadro per aprire il pannello **Avvisi**, quindi fare clic su un singolo avviso per visualizzare altri dettagli specifici, incluse tutte le operazioni consigliate.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-121">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="5dd9c-122">È inoltre possibile cancellare l'avviso se il problema è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-122">You can also clear the alert if the issue has been resolved.</span></span>

    ![Fare clic sul riquadro degli avvisi](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="5dd9c-124">Il riquadro **Stato e integrità** offre informazioni dettagliate sull'integrità dei componenti hardware di un dispositivo, oltre allo stato del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-124">The **Status and health** tile provides insights into the hardware component health for a device including the device status.</span></span> <span data-ttu-id="5dd9c-125">Lo stato del dispositivo può essere offline, online, disattivato o pronto per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-125">The device status may be offline, online, deactivated, or ready to set up.</span></span>

    ![Riquadro Stato e integrità](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="5dd9c-127">Il riquadro **Volumi** offre un riepilogo del numero di volumi nel dispositivo, raggruppati per stato.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-127">The **Volumes** tile provides a summary of the number of volumes in your device grouped by status.</span></span>

    ![Riquadro Volumi](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="5dd9c-129">Fare clic sul riquadro per aprire il pannello di elenco **Volumi** e quindi fare clic su un singolo volume per visualizzarne o modificarne le proprietà.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-129">Click the tile to open the **Volumes** list blade, and then click on an individual volume to view or modify its properties.</span></span>
    
    ![Fare clic sul riquadro Volumi](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="5dd9c-131">Per altre informazioni, vedere come [gestire i volumi](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5dd9c-131">For more information, see how to [manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="5dd9c-132">Nel grafico **Utilizzo** è possibile visualizzare l'archiviazione primaria usata nel dispositivo e l'archiviazione cloud usata negli ultimi sette giorni, che corrispondono al periodo di tempo predefinito.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-132">In the **Usage** chart, you can view the primary storage used across your device, and the cloud storage consumed over the past 7 days, the default time period.</span></span>

     ![Riquadro Utilizzo](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="5dd9c-134">Per scegliere una diversa scala cronologica, usare l'opzione **Modifica** nell'angolo superiore destro del grafico.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-134">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Modificare il grafico sull'utilizzo](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="5dd9c-136">In questo grafico, è possibile visualizzare le metriche per l'archiviazione primaria totale (la quantità di dati scritti dall'host per il dispositivo) e l'archiviazione cloud totale utilizzata dal dispositivo in un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-136">In this chart, you can view metrics for the total primary storage (the amount of data written by hosts to your device) and the total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="5dd9c-137">In questo contesto, *archiviazione primaria* fa riferimento alla quantità totale di dati scritti dall'host e può essere suddivisa in base al tipo di volume: *archiviazione primaria a livelli* include sia i dati archiviati in locale sia quelli archiviati a livelli nel cloud,</span><span class="sxs-lookup"><span data-stu-id="5dd9c-137">In this context, *primary storage* refers to the total amount of data written by the host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered to the cloud.</span></span> <span data-ttu-id="5dd9c-138">mentre *archiviazione primaria aggiunta in locale* include solo i dati archiviati in locale.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="5dd9c-139">L’*Archiviazione cloud*d'altra parte, è una misura della quantità totale di dati archiviati nel cloud.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-139">*Cloud storage*, on the other hand, is a measurement of the total amount of data stored in the cloud.</span></span> <span data-ttu-id="5dd9c-140">Questo tipo di archiviazione include i backup e i dati a più livelli.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="5dd9c-141">I dati archiviati nel cloud sono deduplicati e compressi, mentre l'archiviazione primaria indica la quantità di spazio di archiviazione usato prima che i dati vengano deduplicati e compressi.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-141">The data stored in the cloud is deduplicated and compressed, whereas primary storage indicates the amount of storage used before the data is deduplicated and compressed.</span></span> <span data-ttu-id="5dd9c-142">(È possibile confrontare i due numeri per avere un'idea del tasso di compressione). Per entrambe le archiviazioni, primaria e cloud, gli importi mostrati si basano sulla frequenza di rilevamento configurata.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-142">(You can compare these two numbers to get an idea of the compression rate.) For both primary and cloud storage, the amounts shown are based on the tracking frequency you configure.</span></span> <span data-ttu-id="5dd9c-143">Se, ad esempio, si sceglie una frequenza settimanale, il grafico mostrerà i dati per ogni giorno della settimana precedente.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-143">For example, if you choose a one week frequency, then the chart shows data for each day in the previous week.</span></span>

     <span data-ttu-id="5dd9c-144">Per visualizzare la quantità di archiviazione cloud usata nel corso del tempo, selezionare l'opzione **SPAZIO DI ARCHIVIAZIONE CLOUD UTILIZZATO**.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-144">To see the amount of cloud storage consumed over time, select the **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="5dd9c-145">Per visualizzare l'archiviazione totale scritta dall'host, selezionare le opzioni **PRIMARY TIERED STORAGE USED** (ARCHIVIAZIONE PRIMARIA A LIVELLI USATA) e **PRIMARY LOCALLY PINNED STORAGE USED** (ARCHIVIAZIONE PRIMARIA AGGIUNTA IN LOCALE USATA).</span><span class="sxs-lookup"><span data-stu-id="5dd9c-145">To see the total storage that has been written by the host, select the **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="5dd9c-146">Per ulteriori informazioni, vedere [Utilizzare il servizio StorSimple Manager per monitorare il dispositivo StorSimple](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="5dd9c-146">For more information, see [Use the StorSimple Device Manager service to monitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="5dd9c-147">Il riquadro **Capacità** mostra l'archiviazione primaria di cui è stato eseguito il provisioning e quella rimanente nel dispositivo rispetto all'archiviazione totale disponibile per lo stesso dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-147">The **Capacity** tile displays the primary storage that is provisioned and remaining across the device relative to the total storage available for the same.</span></span> <span data-ttu-id="5dd9c-148">**Provisioning** fa riferimento alla quantità di spazio di archiviazione preparata e allocata per l'uso; **Rimanente** fa riferimento alla capacità rimanente di cui è possibile eseguire il provisioning in questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-148">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> 

    ![Riquadro Utilizzo](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="5dd9c-150">Fare clic su questo riquadro per visualizzare come viene effettuato il provisioning della capacità tra i volumi a livelli e i volumi aggiunti in locale.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-150">Click this tile to view how the capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="5dd9c-151">**Rimanente a livelli** è la capacità disponibile di cui è possibile effettuare il provisioning, incluso cloud, mentre **Rimanente locale** è la capacità rimanente sui dischi collegati a questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5dd9c-151">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this device.</span></span>

    ![Fare clic sul grafico Utilizzo](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="5dd9c-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5dd9c-153">Next steps</span></span>
* <span data-ttu-id="5dd9c-154">Altre informazioni sul [pannello di riepilogo del servizio StorSimple](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="5dd9c-154">Learn more about the [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="5dd9c-155">Altre informazioni sull'[utilizzo del servizio Gestione dispositivi StorSimple per amministrare il dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5dd9c-155">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

