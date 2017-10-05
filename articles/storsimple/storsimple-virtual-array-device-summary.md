---
title: Pannello di riepilogo dispositivo array virtuale StorSimple | Documentazione Microsoft
description: "Descrive il pannello di riepilogo dispositivo per Gestione dispositivi StorSimple e illustra come usarlo per monitorare l'integrità dell'array virtuale StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="41ac1-103">Usare il pannello di riepilogo dispositivo per il servizio Gestione dispositivi StorSimple connesso all'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="41ac1-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="41ac1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="41ac1-104">Overview</span></span>

<span data-ttu-id="41ac1-105">Il pannello del dispositivo di Gestione dispositivi StorSimple visualizza un riepilogo di un array virtuale StorSimple registrato con uno specifico servizio Gestione dispositivi StorSimple, evidenziando i problemi relativi al dispositivo che richiedono attenzione da parte dell'amministratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="41ac1-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="41ac1-106">Questa esercitazione introduce il pannello di riepilogo del dispositivo, illustra il contenuto e la funzione e descrive le attività che è possibile eseguire da questo pannello.</span><span class="sxs-lookup"><span data-stu-id="41ac1-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="41ac1-107">Il pannello di riepilogo dispositivo contiene le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="41ac1-107">The device summary blade displays the following information:</span></span>

![Pagina dashboard](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="41ac1-109">gestione</span><span class="sxs-lookup"><span data-stu-id="41ac1-109">Management</span></span>

<span data-ttu-id="41ac1-110">Il pannello del dispositivo StorSimple contiene le opzioni per la gestione del dispositivo StorSimple in uso.</span><span class="sxs-lookup"><span data-stu-id="41ac1-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="41ac1-111">I comandi per la gestione vengono visualizzati nella parte superiore del pannello e sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="41ac1-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="41ac1-112">Usare queste opzioni per aggiungere condivisioni o volumi, aggiornare o eseguire il failover dell'array virtuale.</span><span class="sxs-lookup"><span data-stu-id="41ac1-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="41ac1-113">L'area relativa alle informazioni di base riporta alcune proprietà importanti, ad esempio lo stato, il modello, la versione del software e un collegamento **all'interfaccia utente Web** dell'array.</span><span class="sxs-lookup"><span data-stu-id="41ac1-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="41ac1-114">Se si usa una rete interna, è possibile avviare direttamente l'[interfaccia utente Web locale](storsimple-ova-web-ui-admin.md) per amministrare l'array virtuale.</span><span class="sxs-lookup"><span data-stu-id="41ac1-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![Informazioni di base sui dispositivi](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="41ac1-116">Riepilogo dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="41ac1-116">StorSimple device summary</span></span>

* <span data-ttu-id="41ac1-117">Il riquadro **Avvisi** fornisce uno snapshot di tutti gli avvisi attivi per l'array virtuale, raggruppati in base alla gravità.</span><span class="sxs-lookup"><span data-stu-id="41ac1-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="41ac1-118">Fare clic sul riquadro per aprire il pannello **Avvisi**, quindi fare clic su un singolo avviso per visualizzare altri dettagli specifici, incluse tutte le operazioni consigliate.</span><span class="sxs-lookup"><span data-stu-id="41ac1-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="41ac1-119">È inoltre possibile cancellare l'avviso se il problema è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="41ac1-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="41ac1-120">Il riquadro **Capacità** mostra l'archiviazione primaria di cui è stato eseguito il provisioning e quella rimanente nel dispositivo virtuale rispetto all'archiviazione totale disponibile per lo stesso dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41ac1-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="41ac1-121">**Provisioning** fa riferimento alla quantità di spazio di archiviazione preparata e allocata per l'uso; **Rimanente** fa riferimento alla capacità rimanente di cui è possibile eseguire il provisioning in questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="41ac1-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="41ac1-122">**Rimanente a livelli** è la capacità disponibile di cui è possibile eseguire il provisioning, tra cui il cloud, mentre **Rimanente locale** è la capacità rimanente sui dischi collegati a questo array virtuale.</span><span class="sxs-lookup"><span data-stu-id="41ac1-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="41ac1-123">Nel grafico **Utilizzo** è possibile visualizzare l'archiviazione primaria usata in tutti gli array virtuali e l'archiviazione cloud usata negli ultimi sette giorni, il periodo di tempo predefinito.</span><span class="sxs-lookup"><span data-stu-id="41ac1-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="41ac1-124">Usare l'opzione **Modifica** nell'angolo superiore destro del grafico per scegliere una scala cronologica differente.</span><span class="sxs-lookup"><span data-stu-id="41ac1-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="41ac1-125">Il riquadro **Condivisioni** o **Volumi** fornisce un riepilogo del numero di condivisioni o volumi nel dispositivo raggruppati per stato.</span><span class="sxs-lookup"><span data-stu-id="41ac1-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="41ac1-126">Fare clic sul riquadro per aprire il pannello di elenco **Condivisioni** o **Volumi** e quindi fare clic su una singola condivisione o un singolo volume per visualizzare o modificare le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="41ac1-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="41ac1-127">Per altre informazioni, vedere l'articolo su come [gestire le condivisioni](storsimple-virtual-array-manage-shares.md) o [gestire i volumi](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="41ac1-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41ac1-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41ac1-128">Next steps</span></span>
<span data-ttu-id="41ac1-129">È possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="41ac1-129">Learn how to:</span></span>
- [<span data-ttu-id="41ac1-130">Gestire condivisioni su un array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="41ac1-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="41ac1-131">Gestire volumi su un array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="41ac1-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

