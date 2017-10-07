---
title: Pannello riepilogo di aaaStorSimple Array virtuale dispositivo | Documenti Microsoft
description: "Descrive pannello riepilogo di hello dispositivo di gestione di dispositivi StorSimple e illustra come toouse, integrità hello toomonitor della matrice virtuale StorSimple."
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
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a><span data-ttu-id="ebb50-103">Pannello di riepilogo dispositivo hello utilizzo di gestione di dispositivi StorSimple connesso tooStorSimple Array virtuale</span><span class="sxs-lookup"><span data-stu-id="ebb50-103">Use hello device summary blade for StorSimple Device Manager connected tooStorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="ebb50-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ebb50-104">Overview</span></span>

<span data-ttu-id="ebb50-105">Pannello dispositivo di gestione di dispositivi StorSimple Hello fornisce un riepilogo di una matrice virtuale StorSimple registrato con un determinato StorSimple Manager di dispositivi, evidenziando i problemi dei dispositivi che richiedono attenzione da parte dell'amministratore di sistema.</span><span class="sxs-lookup"><span data-stu-id="ebb50-105">hello StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="ebb50-106">In questa esercitazione presenta Pannello di riepilogo dispositivo hello, spiega (funzione) e il contenuto di hello e vengono descritte le attività di hello che è possibile eseguire questo pannello.</span><span class="sxs-lookup"><span data-stu-id="ebb50-106">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="ebb50-107">Pannello riepilogo di Hello dispositivo Visualizza hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="ebb50-107">hello device summary blade displays hello following information:</span></span>

![Pagina dashboard](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="ebb50-109">gestione</span><span class="sxs-lookup"><span data-stu-id="ebb50-109">Management</span></span>

<span data-ttu-id="ebb50-110">Nel pannello dispositivo di StorSimple hello, vedrai opzioni hello per la gestione del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ebb50-110">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="ebb50-111">Verranno visualizzati i comandi di gestione hello in alto di hello del pannello hello e sul lato sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="ebb50-111">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="ebb50-112">Usare queste opzioni tooadd condivisioni o volumi, aggiornare o eseguire il failover l'array virtuale.</span><span class="sxs-lookup"><span data-stu-id="ebb50-112">Use these options tooadd shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="ebb50-113">Hello area essentials acquisisce alcune delle proprietà importanti di hello, ad esempio, lo stato di hello, modello, versione del software, nonché toohello un collegamento **dell'interfaccia utente Web** della matrice hello.</span><span class="sxs-lookup"><span data-stu-id="ebb50-113">hello essentials area captures some of hello important properties such as, hello status, model, software version as well as a link toohello **Web UI** of hello array.</span></span> <span data-ttu-id="ebb50-114">Se si utilizza una rete interna, è possibile avviare direttamente hello [interfaccia utente web locale](storsimple-ova-web-ui-admin.md) tooadminister l'array virtuale.</span><span class="sxs-lookup"><span data-stu-id="ebb50-114">If you are on an internal network, you can directly launch hello [local web UI](storsimple-ova-web-ui-admin.md) tooadminister your virtual array.</span></span>

![Informazioni di base sui dispositivi](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="ebb50-116">Riepilogo dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="ebb50-116">StorSimple device summary</span></span>

* <span data-ttu-id="ebb50-117">Hello **avvisi** riquadro fornisce uno snapshot di tutti gli avvisi attivi hello per l'array virtuale, raggruppato in base alla gravità dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="ebb50-117">hello **Alerts** tile provides a snapshot of all hello active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="ebb50-118">Fare clic su hello di hello riquadro tooopen **avvisi** blade e quindi fare clic su un singolo avviso tooview ulteriori dettagli sull'avviso, inclusi eventuali azioni consigliate.</span><span class="sxs-lookup"><span data-stu-id="ebb50-118">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="ebb50-119">È inoltre possibile cancellare avviso hello se hello problema è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="ebb50-119">You can also clear hello alert if hello issue has been resolved.</span></span>

* <span data-ttu-id="ebb50-120">Hello **capacità** riquadro Visualizza hello primario spazio di archiviazione viene eseguito il provisioning e rimanente in hello periferica virtuale toohello relativo spazio di archiviazione totale disponibile per hello stesso.</span><span class="sxs-lookup"><span data-stu-id="ebb50-120">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello virtual device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="ebb50-121">**Il provisioning** fa riferimento toohello quantità di spazio di archiviazione preparata e allocata per l'utilizzo, **rimanente** fa riferimento toohello residua che è possibile effettuare il provisioning in questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ebb50-121">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="ebb50-122">Hello **a livelli rimanenti** capacità sia hello disponibile una capacità che è possibile effettuare il provisioning inclusi cloud, mentre hello **rimanenti locale** capacità hello rimanente su dischi hello collegato toothis virtuale matrice.</span><span class="sxs-lookup"><span data-stu-id="ebb50-122">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis virtual array.</span></span>

* <span data-ttu-id="ebb50-123">In hello **utilizzo** grafico, è possibile visualizzare l'archiviazione primaria di hello usata tra l'array virtuale, nonché l'archiviazione cloud hello consumata in hello ultimi 7 giorni, il periodo di tempo predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="ebb50-123">In hello **Usage** chart, you can view hello primary storage used across your virtual array, as well as hello cloud storage consumed  over hello past 7 days, hello default time period.</span></span> <span data-ttu-id="ebb50-124">Hello utilizzare **modifica** opzione nell'angolo superiore destro di hello di hello grafico toochoose una scala temporale diverso.</span><span class="sxs-lookup"><span data-stu-id="ebb50-124">Use hello **Edit** option in hello top-right corner of hello chart toochoose a different time scale.</span></span>

* <span data-ttu-id="ebb50-125">Hello **condivisioni** o **volumi** riquadro fornisce un riepilogo del numero di hello delle condivisioni o volumi nel dispositivo raggruppati per stato.</span><span class="sxs-lookup"><span data-stu-id="ebb50-125">hello **Shares** or **Volumes** tile provides a summary of hello number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="ebb50-126">Fare clic su hello di hello riquadro tooopen **condivisioni** o **volumi** elenco pannello, quindi fare clic su un singolo tooview condivisione o volume o modificarne le proprietà.</span><span class="sxs-lookup"><span data-stu-id="ebb50-126">Click hello tile tooopen hello **Shares**  or **Volumes** list blade, and then click on an individual share or volume tooview or modify its properties.</span></span> <span data-ttu-id="ebb50-127">Per ulteriori informazioni, vedere come troppo[gestire condivisioni](storsimple-virtual-array-manage-shares.md) o [gestire volumi](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="ebb50-127">For more information, see how too[manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebb50-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ebb50-128">Next steps</span></span>
<span data-ttu-id="ebb50-129">È possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebb50-129">Learn how to:</span></span>
- [<span data-ttu-id="ebb50-130">Gestire condivisioni su un array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="ebb50-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="ebb50-131">Gestire volumi su un array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="ebb50-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

