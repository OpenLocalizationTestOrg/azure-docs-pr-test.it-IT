---
title: Usare il riepilogo per dispositivi StorSimple serie 8000 | Microsoft Docs
description: "Descrive il pannello di riepilogo del servizio StorSimple e illustra come usarlo per monitorare l'integrità della soluzione StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: d987a4ae170f21532a886552cbe1eb5a0d25fc3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="40fe9-103">Usare il pannello di riepilogo del servizio per dispositivi StorSimple serie 8000</span><span class="sxs-lookup"><span data-stu-id="40fe9-103">Use the service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="40fe9-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="40fe9-104">Overview</span></span>

<span data-ttu-id="40fe9-105">Il pannello di riepilogo del servizio Gestione dispositivi StorSimple offre una visualizzazione di riepilogo di tutti i dispositivi connessi a tale servizio, evidenziando quelli che richiedono attenzione da parte dell'amministratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="40fe9-105">The StorSimple Device Manager service summary blade provides a summary view of all the devices that are connected to the StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="40fe9-106">Questa esercitazione illustra il pannello di riepilogo del servizio e descrive il contenuto e la funzione del dashboard nonché le attività che è possibile eseguire da questa pagina.</span><span class="sxs-lookup"><span data-stu-id="40fe9-106">This tutorial introduces the service summary blade, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![Riepilogo del servizio](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="40fe9-108">Comandi di gestione</span><span class="sxs-lookup"><span data-stu-id="40fe9-108">Management commands</span></span>

<span data-ttu-id="40fe9-109">Nel pannello di riepilogo del servizio StorSimple vengono visualizzate le opzioni per gestire il servizio Gestione dispositivi StorSimple e i dispositivi StorSimple serie 8000 in esso registrati.</span><span class="sxs-lookup"><span data-stu-id="40fe9-109">In the StorSimple service summary blade, you see the options for managing your StorSimple Device Manager service and the StorSimple 8000 series devices registered to this service.</span></span> <span data-ttu-id="40fe9-110">I comandi per la gestione vengono visualizzati nella parte superiore del pannello e sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="40fe9-110">You see the management commands across the top of the blade and on the left side.</span></span>

![Barra dei comandi](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="40fe9-112">Usare queste opzioni per eseguire diverse operazioni, ad esempio aggiungere volumi o condivisioni, oppure monitorare i vari processi in esecuzione nei dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="40fe9-112">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="40fe9-113">Informazioni di base</span><span class="sxs-lookup"><span data-stu-id="40fe9-113">Essentials</span></span>

<span data-ttu-id="40fe9-114">L'area relativa alle informazioni di base riporta alcune proprietà importanti, ad esempio il gruppo di risorse, il percorso e la sottoscrizione in cui è stato creato il servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="40fe9-114">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![Informazioni di base](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="40fe9-116">Riepilogo servizio di Gestione dispositivi StorSimple</span><span class="sxs-lookup"><span data-stu-id="40fe9-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="40fe9-117">Il riquadro **Avvisi** offre uno snapshot di tutti gli avvisi attivi per tutti i dispositivi, raggruppati in base alla gravità.</span><span class="sxs-lookup"><span data-stu-id="40fe9-117">The **Alerts** tile provides a snapshot of all the active alerts across all devices, grouped by alert severity.</span></span>

    ![Riquadro Avvisi](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="40fe9-119">Facendo clic sul riquadro viene aperto il pannello **Avvisi**, in cui è possibile fare clic su un singolo avviso per visualizzare altri dettagli specifici, incluse tutte le operazioni consigliate.</span><span class="sxs-lookup"><span data-stu-id="40fe9-119">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="40fe9-120">È inoltre possibile cancellare l'avviso se il problema è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="40fe9-120">You can also clear the alert if the issue has been resolved.</span></span>

    ![Fare clic sul riquadro Avvisi](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="40fe9-122">Il riquadro **Capacità** mostra lo spazio di archiviazione primario di cui è stato effettuato il provisioning e quello rimanente in tutti i dispositivi rispetto allo spazio di archiviazione totale in essi disponibile.</span><span class="sxs-lookup"><span data-stu-id="40fe9-122">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="40fe9-123">**Provisioning eseguito** fa riferimento allo spazio di archiviazione preparato e allocato per l'uso, mentre **Rimanente** fa riferimento alla capacità rimanente di cui è possibile effettuare il provisioning in tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="40fe9-123">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all devices.</span></span>

    ![Riquadro Capacità](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="40fe9-125">La capacità **Rimanente - A livelli** è quella disponibile per il provisioning includendo il cloud, mentre **Rimanente - Locale** è la capacità rimanente nei dischi collegati ai dispositivi StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="40fe9-125">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="40fe9-126">Nel grafico **Utilizzo** vengono visualizzate le metriche rilevanti per i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="40fe9-126">In the **Usage** chart, you can see the relevant metrics for your devices.</span></span> <span data-ttu-id="40fe9-127">È possibile visualizzare lo spazio di archiviazione primario usato in tutti i dispositivi e lo spazio di archiviazione cloud utilizzato dai dispositivi negli ultimi 7 giorni, il periodo di tempo predefinito.</span><span class="sxs-lookup"><span data-stu-id="40fe9-127">You can view the primary storage used across all devices, and the cloud storage consumed by devices over the past 7 days, the default time period.</span></span> 

    ![Riquadro Utilizzo](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="40fe9-129">Per scegliere una diversa scala cronologica, usare l'opzione **Modifica** nell'angolo superiore destro del grafico.</span><span class="sxs-lookup"><span data-stu-id="40fe9-129">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Fare clic sul riquadro Utilizzo](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![Esportare i dati del grafico](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="40fe9-132">Il riquadro **Dispositivi** contiene un riepilogo del numero dei dispositivi StorSimple serie 8000 in Gestione dispositivi StorSimple, raggruppati in base allo stato del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="40fe9-132">The **Devices** tile provides a summary of the number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![Riquadro Dispositivi](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="40fe9-134">Fare clic su questo riquadro per aprire l'elenco **Dispositivi** e fare clic su un singolo dispositivo per esaminarne in dettaglio il riepilogo.</span><span class="sxs-lookup"><span data-stu-id="40fe9-134">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="40fe9-135">È anche possibile eseguire azioni specifiche relative a un dispositivo dal pannello di riepilogo di un determinato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="40fe9-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="40fe9-136">Per altre informazioni sul pannello di riepilogo dispositivo, vedere [Pannello di riepilogo dispositivo](storsimple-8000-device-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="40fe9-136">For more information about the device summary blade, go to [Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![Fare clic sul riquadro Dispositivi](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-the-activity-logs"></a><span data-ttu-id="40fe9-138">Visualizzare i log attività</span><span class="sxs-lookup"><span data-stu-id="40fe9-138">View the activity logs</span></span>

<span data-ttu-id="40fe9-139">Per visualizzare le varie operazioni eseguite in Gestione dispositivi StorSimple, fare clic sul collegamento **Log attività** sul lato sinistro del pannello di riepilogo servizio StorSimple.</span><span class="sxs-lookup"><span data-stu-id="40fe9-139">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="40fe9-140">Viene visualizzato il pannello **Log attività** in cui è possibile visualizzare un riepilogo delle operazioni recenti eseguite.</span><span class="sxs-lookup"><span data-stu-id="40fe9-140">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![Log attività](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="40fe9-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40fe9-142">Next steps</span></span>

* <span data-ttu-id="40fe9-143">Altre informazioni su come [usare il servizio Gestione dispositivi StorSimple per amministrare un dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="40fe9-143">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

