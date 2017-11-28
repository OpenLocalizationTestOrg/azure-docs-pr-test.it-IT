---
title: aaaDeactivate ed eliminare un Array virtuale di Microsoft Azure StorSimple | Documenti Microsoft
description: Viene descritto come dispositivo di StorSimple tooremove dal servizio innanzitutto disattivarlo e quindi eliminarlo.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="f281e-103">Disattivare ed eliminare un array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="f281e-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="f281e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f281e-104">Overview</span></span>

<span data-ttu-id="f281e-105">Quando si disattiva un Array virtuale StorSimple, si interrompe la connessione hello tra hello dispositivo e il servizio StorSimple Manager periferica corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="f281e-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="f281e-106">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="f281e-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="f281e-107">Disattivare un dispositivo</span><span class="sxs-lookup"><span data-stu-id="f281e-107">Deactivate a device</span></span> 
* <span data-ttu-id="f281e-108">Eliminare un dispositivo disattivato</span><span class="sxs-lookup"><span data-stu-id="f281e-108">Delete a deactivated device</span></span>

<span data-ttu-id="f281e-109">informazioni di Hello in questo articolo si applicano tooStorSimple array virtuale.</span><span class="sxs-lookup"><span data-stu-id="f281e-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="f281e-110">Per informazioni sulla 8000 serie, passare toohow troppo[disattivare o eliminare un dispositivo](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="f281e-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="f281e-111">Quando toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="f281e-111">When toodeactivate?</span></span>

<span data-ttu-id="f281e-112">La disattivazione è un'operazione permanente e non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="f281e-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="f281e-113">È possibile registrare un dispositivo disattivato con il servizio di gestione di dispositivi StorSimple hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f281e-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="f281e-114">Si potrebbe necessario toodeactivate ed eliminare un Array virtuale StorSimple in hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="f281e-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="f281e-115">**Failover pianificato** : il dispositivo è online e si prevede di toofail failover del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f281e-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="f281e-116">Se si intende tooupgrade tooa maggiore dispositivo, potrebbe essere toofail failover del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f281e-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="f281e-117">Dopo che la proprietà dati hello viene trasferita e hello failover è stato completato, il dispositivo di origine hello viene eliminato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f281e-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="f281e-118">**Failover non pianificato** : il dispositivo è offline ed è necessario toofail su dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="f281e-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="f281e-119">Questo scenario può verificarsi durante un'emergenza quando si verifica un'interruzione nel Data Center hello e il dispositivo primario è inattivo.</span><span class="sxs-lookup"><span data-stu-id="f281e-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="f281e-120">Si prevede di toofail su hello tooa secondario dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f281e-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="f281e-121">Dopo che la proprietà dati hello viene trasferita e hello failover è stato completato, il dispositivo di origine hello viene eliminato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f281e-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="f281e-122">**Rimuovere le autorizzazioni** : si desidera toodecommission hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f281e-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="f281e-123">Questa operazione richiede il toofirst disattivare hello dispositivo e quindi eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="f281e-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="f281e-124">Quando si disattiva un dispositivo, tutti i dati archiviati localmente non saranno più accessibili.</span><span class="sxs-lookup"><span data-stu-id="f281e-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="f281e-125">È possibile solo i dati di hello accesso e di ripristino archiviati nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f281e-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="f281e-126">Se si prevede di dati del dispositivo hello tookeep dopo la disattivazione, è necessario creare uno snapshot di cloud di tutti i dati prima di disattivare un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f281e-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="f281e-127">Snapshot cloud consente toorecover tutti hello dati in una fase successiva.</span><span class="sxs-lookup"><span data-stu-id="f281e-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="f281e-128">Disattivare un dispositivo</span><span class="sxs-lookup"><span data-stu-id="f281e-128">Deactivate a device</span></span>

<span data-ttu-id="f281e-129">toodeactivate il dispositivo, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f281e-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="f281e-130">dispositivo hello toodeactivate</span><span class="sxs-lookup"><span data-stu-id="f281e-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="f281e-131">Nel servizio, andare troppo**gestione > dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="f281e-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="f281e-132">In hello **dispositivi** pannello, fare clic su e dispositivo di hello select che si desidera toodeactivate.</span><span class="sxs-lookup"><span data-stu-id="f281e-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Selezionare toodeactivate dispositivo](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="f281e-134">Nel **dashboard del dispositivo** pannello, fare clic su **... Ulteriori** e selezionare nell'elenco hello **disattiva**.</span><span class="sxs-lookup"><span data-stu-id="f281e-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Clic su Disattiva](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="f281e-136">In hello **disattiva** pannello, nome del tipo hello dispositivo e quindi fare clic su **disattiva**.</span><span class="sxs-lookup"><span data-stu-id="f281e-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Conferma della disattivazione](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="f281e-138">Hello disattivare processo inizia e accetta toocomplete di pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="f281e-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Disattivazione in corso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="f281e-140">Dopo la disattivazione, aggiorna l'elenco di hello dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="f281e-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Disattivazione completata](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="f281e-142">È ora possibile eliminare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f281e-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="f281e-143">Eliminare dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="f281e-143">Delete hello device</span></span>

<span data-ttu-id="f281e-144">Un dispositivo ha toodelete disattivate prima toobe è.</span><span class="sxs-lookup"><span data-stu-id="f281e-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="f281e-145">L'eliminazione di un dispositivo per rimuoverlo dall'elenco di hello del servizio di dispositivi connessi toohello.</span><span class="sxs-lookup"><span data-stu-id="f281e-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="f281e-146">servizio Hello quindi non può più gestire il dispositivo hello eliminato.</span><span class="sxs-lookup"><span data-stu-id="f281e-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="f281e-147">dati Hello associati hello dispositivo rimangono tuttavia nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="f281e-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="f281e-148">Su questi dati sono applicati degli addebiti.</span><span class="sxs-lookup"><span data-stu-id="f281e-148">This data then accrues charges.</span></span>

<span data-ttu-id="f281e-149">dispositivo hello toodelete, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="f281e-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="f281e-150">dispositivo hello toodelete</span><span class="sxs-lookup"><span data-stu-id="f281e-150">toodelete hello device</span></span>

1. <span data-ttu-id="f281e-151">Il servizio StorSimple Device Manager andare troppo**gestione > dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="f281e-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="f281e-152">In hello **dispositivi** pannello selezionare un dispositivo disattivato che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="f281e-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="f281e-153">In hello **dashboard del dispositivo** pannello, fare clic su **... Ulteriori** e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="f281e-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Selezionare toodelete dispositivo](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="f281e-155">In hello **eliminare** pannello, il nome del tipo hello di eliminazione di hello tooconfirm dispositivo e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="f281e-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="f281e-156">L'eliminazione dispositivo hello non elimina i dati di cloud hello associati hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f281e-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Conferma dell'eliminazione](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="f281e-158">l'eliminazione di Hello viene avviato e richiede pochi minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f281e-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Eliminazione in corso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="f281e-160">Dopo l'eliminazione hello dispositivo, è possibile visualizzare l'elenco di hello aggiornato di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="f281e-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f281e-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f281e-161">Next steps</span></span>

* <span data-ttu-id="f281e-162">Per informazioni su come toofail, andare troppo[Failover e ripristino di emergenza di matrice virtuale StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="f281e-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="f281e-163">altre informazioni sulle toolearn come toouse hello servizio di gestione di dispositivi StorSimple, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple l'Array virtuale StorSimple](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f281e-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

