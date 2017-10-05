---
title: Disattivare ed eliminare un array virtuale Microsoft Azure StorSimple | Documentazione Microsoft
description: Viene descritto come rimuovere un dispositivo StorSimple dal servizio disattivandolo e poi eliminandolo.
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
ms.openlocfilehash: 8dea36f92b034f8c6cdb6875634848d37f4c6606
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="6737a-103">Disattivare ed eliminare un array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="6737a-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="6737a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="6737a-104">Overview</span></span>

<span data-ttu-id="6737a-105">Quando si disattiva un array virtuale StorSimple, si interrompe la connessione tra il dispositivo e il servizio Gestione dispositivi StorSimple corrispondente.</span><span class="sxs-lookup"><span data-stu-id="6737a-105">When you deactivate a StorSimple Virtual Array, you break the connection between the device and the corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="6737a-106">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="6737a-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="6737a-107">Disattivare un dispositivo</span><span class="sxs-lookup"><span data-stu-id="6737a-107">Deactivate a device</span></span> 
* <span data-ttu-id="6737a-108">Eliminare un dispositivo disattivato</span><span class="sxs-lookup"><span data-stu-id="6737a-108">Delete a deactivated device</span></span>

<span data-ttu-id="6737a-109">Le informazioni in questo articolo si applicano solo agli array virtuali StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6737a-109">The information in this article applies to StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="6737a-110">Per informazioni sulla serie 8000, passare alla procedura per [la disattivazione o per l'eliminazione di un dispositivo](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="6737a-110">For information on 8000 series, go to how to [deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-to-deactivate"></a><span data-ttu-id="6737a-111">Quando disattivare</span><span class="sxs-lookup"><span data-stu-id="6737a-111">When to deactivate?</span></span>

<span data-ttu-id="6737a-112">La disattivazione è un'operazione permanente e non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="6737a-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="6737a-113">Un dispositivo disattivato non può essere registrato di nuovo con il servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6737a-113">You cannot register a deactivated device with the StorSimple Device Manager service again.</span></span> <span data-ttu-id="6737a-114">Negli scenari seguenti potrebbe essere necessario disattivare ed eliminare un array virtuale StorSimple:</span><span class="sxs-lookup"><span data-stu-id="6737a-114">You may need to deactivate and delete a StorSimple Virtual Array in the following scenarios:</span></span>

* <span data-ttu-id="6737a-115">**Failover pianificato**: il dispositivo è in linea e si prevede di eseguirne il failover.</span><span class="sxs-lookup"><span data-stu-id="6737a-115">**Planned failover** : Your device is online and you plan to fail over your device.</span></span> <span data-ttu-id="6737a-116">Può essere necessario eseguire questa operazione se si prevede l'aggiornamento a un dispositivo di dimensioni superiori.</span><span class="sxs-lookup"><span data-stu-id="6737a-116">If you are planning to upgrade to a larger device, you may need to fail over your device.</span></span> <span data-ttu-id="6737a-117">Dopo il trasferimento della proprietà dei dati e il completamento del failover, il dispositivo di origine viene eliminato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6737a-117">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="6737a-118">**Failover non pianificato**: il dispositivo è offline ed è necessario eseguirne il failover.</span><span class="sxs-lookup"><span data-stu-id="6737a-118">**Unplanned failover** : Your device is offline and you need to fail over the device.</span></span> <span data-ttu-id="6737a-119">Questo scenario può verificarsi durante un'emergenza dovuta a un'interruzione nel datacenter e quando il dispositivo primario è inattivo.</span><span class="sxs-lookup"><span data-stu-id="6737a-119">This scenario may occur during a disaster when there is an outage in the datacenter and your primary device is down.</span></span> <span data-ttu-id="6737a-120">Si pianifica di eseguire il failover del dispositivo su un dispositivo secondario.</span><span class="sxs-lookup"><span data-stu-id="6737a-120">You plan to fail over the device to a secondary device.</span></span> <span data-ttu-id="6737a-121">Dopo il trasferimento della proprietà dei dati e il completamento del failover, il dispositivo di origine viene eliminato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6737a-121">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="6737a-122">**Rimozioni delle autorizzazioni**: si desidera rimuovere le autorizzazioni del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6737a-122">**Decommission** : You want to decommission the device.</span></span> <span data-ttu-id="6737a-123">Ciò richiede prima di tutto la disattivazione del dispositivo, quindi la sua eliminazione.</span><span class="sxs-lookup"><span data-stu-id="6737a-123">This requires you to first deactivate the device and then delete it.</span></span> <span data-ttu-id="6737a-124">Quando si disattiva un dispositivo, tutti i dati archiviati localmente non saranno più accessibili.</span><span class="sxs-lookup"><span data-stu-id="6737a-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="6737a-125">È possibile solo accedere e recuperare i dati archiviati nel cloud.</span><span class="sxs-lookup"><span data-stu-id="6737a-125">You can only access and recover the data stored in the cloud.</span></span> <span data-ttu-id="6737a-126">Se si pianifica cdi mantenere il dispositivo dopo la disattivazione, prima di effettuare tale operazione è necessario eseguire uno snapshot di tutti i dati nel cloud.</span><span class="sxs-lookup"><span data-stu-id="6737a-126">If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="6737a-127">In questo modo sarà possibile recuperare tutti i dati in una fase successiva.</span><span class="sxs-lookup"><span data-stu-id="6737a-127">This cloud snapshot allows you to recover all the data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="6737a-128">Disattivare un dispositivo</span><span class="sxs-lookup"><span data-stu-id="6737a-128">Deactivate a device</span></span>

<span data-ttu-id="6737a-129">Per disattivare un dispositivo seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="6737a-129">To deactivate your device, perform the following steps.</span></span>

#### <a name="to-deactivate-the-device"></a><span data-ttu-id="6737a-130">Per disattivare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="6737a-130">To deactivate the device</span></span>

1. <span data-ttu-id="6737a-131">Nel servizio passare a **Gestione > Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="6737a-131">In your service, go to **Management > Devices**.</span></span> <span data-ttu-id="6737a-132">Nel pannello **Dispositivi** fare clic e selezionare il dispositivo che si desidera disattivare.</span><span class="sxs-lookup"><span data-stu-id="6737a-132">In the **Devices** blade, click and select the device that you wish to deactivate.</span></span>
   
    ![Selezione del dispositivo disattivare](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="6737a-134">Nel pannello **Device dashboard** (Dashboard dispositivo) fare clic su **… More** (... Altro) e, nell'elenco, selezionare **Disattiva**.</span><span class="sxs-lookup"><span data-stu-id="6737a-134">In your **Device dashboard** blade, click **… More** and from the list, select **Deactivate**.</span></span>
   
    ![Clic su Disattiva](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="6737a-136">Nel pannello **Disattiva** digitare il nome del dispositivo e fare clic su **Disattiva**.</span><span class="sxs-lookup"><span data-stu-id="6737a-136">In the **Deactivate** blade, type the device name and then click **Deactivate**.</span></span> 
   
    ![Conferma della disattivazione](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="6737a-138">Si avvia il processo di disattivazione il cui completamento richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="6737a-138">The deactivate process starts and takes a few minutes to complete.</span></span>
   
    ![Disattivazione in corso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="6737a-140">Dopo la disattivazione, l'elenco dei dispositivi viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="6737a-140">After deactivation, the list of devices refreshes.</span></span>
   
    ![Disattivazione completata](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="6737a-142">È ora possibile eliminare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6737a-142">You can now delete this device.</span></span>

## <a name="delete-the-device"></a><span data-ttu-id="6737a-143">Eliminare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="6737a-143">Delete the device</span></span>

<span data-ttu-id="6737a-144">Per eliminare un dispositivo, è prima necessario disattivarlo.</span><span class="sxs-lookup"><span data-stu-id="6737a-144">A device has to be first deactivated to delete it.</span></span> <span data-ttu-id="6737a-145">L’eliminazione di un dispositivo lo rimuove dall'elenco dei dispositivi connessi al servizio.</span><span class="sxs-lookup"><span data-stu-id="6737a-145">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="6737a-146">Il servizio quindi non può più gestire il dispositivo eliminato.</span><span class="sxs-lookup"><span data-stu-id="6737a-146">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="6737a-147">I dati associati al dispositivo rimangono comunque nel cloud.</span><span class="sxs-lookup"><span data-stu-id="6737a-147">The data associated with the device however remains in the cloud.</span></span> <span data-ttu-id="6737a-148">Su questi dati sono applicati degli addebiti.</span><span class="sxs-lookup"><span data-stu-id="6737a-148">This data then accrues charges.</span></span>

<span data-ttu-id="6737a-149">Per eliminare il dispositivo, completare la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="6737a-149">To delete the device, perform the following steps.</span></span>

#### <a name="to-delete-the-device"></a><span data-ttu-id="6737a-150">Per eliminare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="6737a-150">To delete the device</span></span>

1. <span data-ttu-id="6737a-151">In Gestione dispositivi StorSimple passare a **Gestione > Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="6737a-151">In your StorSimple Device Manager, go to **Management > Devices**.</span></span> <span data-ttu-id="6737a-152">Nel pannello **Dispositivi** selezionare un dispositivo disattivato che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="6737a-152">In the **Devices** blade, select a deactivated device that you wish to delete.</span></span>
2. <span data-ttu-id="6737a-153">Nel pannello **Device dashboard** (Dashboard dispositivo) fare clic su **… More** (Altro), quindi su**Elimina**.</span><span class="sxs-lookup"><span data-stu-id="6737a-153">In the **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Selezione del dispositivo da eliminare](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="6737a-155">Nel pannello **Elimina** digitare il nome del dispositivo per confermare l'eliminazione, quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="6737a-155">In the **Delete** blade, type the name of your device to confirm the deletion and then click **Delete**.</span></span> <span data-ttu-id="6737a-156">L'eliminazione del dispositivo non determina l'eliminazione dei dati a esso associati presenti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="6737a-156">Deleting the device does not delete the cloud data associated with the device.</span></span> 
   
   ![Conferma dell'eliminazione](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="6737a-158">Si avvia il processo di eliminazione il cui completamento richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="6737a-158">The deletion starts and takes a few minutes to complete.</span></span>
   
   ![Eliminazione in corso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="6737a-160">Dopo il completamento dell'eliminazione, è possibile visualizzare l'elenco aggiornato dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="6737a-160">After the device is deleted, you can view the updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6737a-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6737a-161">Next steps</span></span>

* <span data-ttu-id="6737a-162">Per informazioni su come eseguire il failover, fare riferimento all'articolo relativo a [failover e ripristino di emergenza per l'array virtuale StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="6737a-162">For information on how to fail over, go to [Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="6737a-163">Per altre informazioni sull'uso del servizio Gestione dispositivi StorSimple, vedere l'articolo relativo all'[uso di Gestione dispositivi StorSimple per amministrare l'array virtuale StorSimple](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6737a-163">To learn more about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

