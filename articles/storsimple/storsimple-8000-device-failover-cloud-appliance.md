---
title: Failover di StorSimple, ripristino di emergenza in un'appliance cloud StorSimple | Microsoft Docs
description: Informazioni su come eseguire il failover del dispositivo StorSimple serie 8000 su un'appliance cloud.
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: ec8bebf2854e84a37e84b45564e80fc20b63d8d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-your-storsimple-cloud-appliance"></a><span data-ttu-id="8bde0-103">Failover nell'appliance cloud StorSimple</span><span class="sxs-lookup"><span data-stu-id="8bde0-103">Fail over to your StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="8bde0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8bde0-104">Overview</span></span>

<span data-ttu-id="8bde0-105">Questa esercitazione descrive i passaggi necessari per eseguire il failover di un dispositivo StorSimple serie 8000 fisico su un'appliance cloud StorSimple in caso di emergenza.</span><span class="sxs-lookup"><span data-stu-id="8bde0-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to a StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="8bde0-106">StorSimple usa la funzionalità di failover del dispositivo per eseguire la migrazione dei dati da un dispositivo fisico di origine nel data center a un'appliance cloud eseguita in Azure.</span><span class="sxs-lookup"><span data-stu-id="8bde0-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to a cloud appliance running in Azure.</span></span> <span data-ttu-id="8bde0-107">Le indicazioni fornite in questa esercitazione si applicano ai dispositivi fisici StorSimple serie 8000 e alle applicazioni cloud in cui sono installate le versioni software Update 3 e successive.</span><span class="sxs-lookup"><span data-stu-id="8bde0-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="8bde0-108">Per altre informazioni sul failover del dispositivo e su come usarlo per il ripristino di emergenza, passare a [Failover e ripristino di emergenza per dispositivi StorSimple serie 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="8bde0-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="8bde0-109">Per effettuare il failover di un dispositivo fisico StorSimple su un altro dispositivo fisico, vedere [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md) (Failover su un dispositivo fisico StorSimple).</span><span class="sxs-lookup"><span data-stu-id="8bde0-109">To fail over a StorSimple physical device to another physical device, go to [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="8bde0-110">Per eseguire il failover di un dispositivo su se stesso, passare a [Eseguire il failover sullo stesso dispositivo fisico StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="8bde0-110">To fail over a device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bde0-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8bde0-111">Prerequisites</span></span>

- <span data-ttu-id="8bde0-112">Assicurarsi di aver esaminato le considerazioni relative al failover dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8bde0-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="8bde0-113">Per altre informazioni, vedere [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md) (Considerazioni comuni per il failover dei dispositivi).</span><span class="sxs-lookup"><span data-stu-id="8bde0-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="8bde0-114">Prima di eseguire questa procedura, è necessario disporre di un'appliance cloud StorSimple creata e configurata.</span><span class="sxs-lookup"><span data-stu-id="8bde0-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="8bde0-115">Se è in l'aggiornamento 3 o una versione successiva del software, è consigliabile usare un'appliance cloud 8020 per il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="8bde0-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for the DR.</span></span> <span data-ttu-id="8bde0-116">Il modello 8020 dispone di 64 TB e usa l'Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="8bde0-116">The 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="8bde0-117">Per altre informazioni, vedere [Distribuire e gestire un'appliance cloud StorSimple](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="8bde0-117">For more information, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-to-fail-over-to-a-cloud-appliance"></a><span data-ttu-id="8bde0-118">Procedura di failover in un'appliance cloud</span><span class="sxs-lookup"><span data-stu-id="8bde0-118">Steps to fail over to a cloud appliance</span></span>

<span data-ttu-id="8bde0-119">Eseguire i passaggi seguenti per ripristinare il dispositivo su un'appliance cloud StorSimple di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8bde0-119">Perform the following steps to restore the device to a target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="8bde0-120">Verificare che il contenitore del volume di cui si desidera eseguire il failover sia associato alle snapshot cloud.</span><span class="sxs-lookup"><span data-stu-id="8bde0-120">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="8bde0-121">Per altre informazioni, vedere [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md) (Usare il servizio Gestione dispositivi StorSimple per creare backup).</span><span class="sxs-lookup"><span data-stu-id="8bde0-121">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="8bde0-122">Passare al servizio Gestione dispositivi StorSimple e fare clic su **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8bde0-122">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="8bde0-123">Nel pannello **Dispositivi**, visualizzare l'elenco di dispositivi connessi al servizio.</span><span class="sxs-lookup"><span data-stu-id="8bde0-123">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="8bde0-124">![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="8bde0-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="8bde0-125">Selezionare e fare clic sul dispositivo di origine.</span><span class="sxs-lookup"><span data-stu-id="8bde0-125">Select and click your source device.</span></span> <span data-ttu-id="8bde0-126">Il dispositivo di origine presenta i contenitori dei volumi di cui effettuare il failover.</span><span class="sxs-lookup"><span data-stu-id="8bde0-126">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="8bde0-127">Passare a **Impostazioni > Contenitori dei volumi**.</span><span class="sxs-lookup"><span data-stu-id="8bde0-127">Go to **Settings > Volume Containers**.</span></span>

    ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="8bde0-129">Selezionare un contenitore di volumi di cui si desidera eseguire il failover a un altro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8bde0-129">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="8bde0-130">Fare clic sul contenitore di volumi per visualizzare l'elenco dei volumi presenti nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="8bde0-130">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="8bde0-131">Selezionare un volume e fare clic con il pulsante destro del mouse su **Porta offline** per portare il volume offline.</span><span class="sxs-lookup"><span data-stu-id="8bde0-131">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span>

    ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="8bde0-133">Ripetere questo processo per tutti i volumi nel contenitore di volumi.</span><span class="sxs-lookup"><span data-stu-id="8bde0-133">Repeat this process for all the volumes in the volume container.</span></span>

     ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="8bde0-135">Ripetere il passaggio precedente per tutti i contenitori di volumi di cui si desidera eseguire il failover a un altro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8bde0-135">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>

7. <span data-ttu-id="8bde0-136">Tornare al pannello **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8bde0-136">Go back to the **Devices** blade.</span></span> <span data-ttu-id="8bde0-137">Nella barra dei comandi fare clic su **Failover**.</span><span class="sxs-lookup"><span data-stu-id="8bde0-137">From the command bar, click **Fail over**.</span></span>

    ![Fare clic su Failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="8bde0-139">Nel pannello **Failover** attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8bde0-139">In the **Fail over** blade, perform the following steps:</span></span>
   
    1. <span data-ttu-id="8bde0-140">Fare clic su **Origine**.</span><span class="sxs-lookup"><span data-stu-id="8bde0-140">Click **Source**.</span></span> <span data-ttu-id="8bde0-141">Selezionare i contenitori dei volumi per il failover.</span><span class="sxs-lookup"><span data-stu-id="8bde0-141">Select the volume containers to fail over.</span></span> <span data-ttu-id="8bde0-142">**Vengono visualizzati solo i contenitori di volumi con gli snapshot del cloud e i volumi offline associati.**</span><span class="sxs-lookup"><span data-stu-id="8bde0-142">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="8bde0-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png) (Seleziona origine)</span><span class="sxs-lookup"><span data-stu-id="8bde0-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="8bde0-144">Fare clic su **Destinazione**.</span><span class="sxs-lookup"><span data-stu-id="8bde0-144">Click **Target**.</span></span> <span data-ttu-id="8bde0-145">Nell'elenco a discesa dei dispositivi disponibili selezionare l'appliance cloud di destinazione.</span><span class="sxs-lookup"><span data-stu-id="8bde0-145">Select a target cloud appliance from the dropdown list of available devices.</span></span> <span data-ttu-id="8bde0-146">**Nell'elenco vengono visualizzati solo i dispositivi che hanno una capacità sufficiente a contenere i contenitori dei volumi di origine.**</span><span class="sxs-lookup"><span data-stu-id="8bde0-146">**Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.**</span></span>

        ![Selezionare la destinazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="8bde0-148">Esaminare le impostazioni di failover in **Riepilogo** e selezionare la casella di controllo che indica che i volumi nei contenitori dei volumi selezionati sono offline.</span><span class="sxs-lookup"><span data-stu-id="8bde0-148">Review the failover settings under **Summary** and select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> 

        ![Esaminare le impostazioni di failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="8bde0-150">Viene creato un processo di failover.</span><span class="sxs-lookup"><span data-stu-id="8bde0-150">A failover job is created.</span></span> <span data-ttu-id="8bde0-151">Per monitorare il processo di failover, fare clic sulla notifica del processo.</span><span class="sxs-lookup"><span data-stu-id="8bde0-151">To monitor the failover job, click the job notification.</span></span>

    ![Monitorare il processo di failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="8bde0-153">Dopo il completamento del failover, tornare al pannello **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8bde0-153">After the failover is completed, go back to the **Devices** blade.</span></span>

    1. <span data-ttu-id="8bde0-154">Selezionare il dispositivo usato come destinazione per il failover.</span><span class="sxs-lookup"><span data-stu-id="8bde0-154">Select the device that was used as the target for the failover.</span></span>

       ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="8bde0-156">Fare clic su **Contenitori di volume**.</span><span class="sxs-lookup"><span data-stu-id="8bde0-156">Click **Volume Containers**.</span></span> <span data-ttu-id="8bde0-157">Dovrebbero essere elencati tutti i contenitori di volumi,  insieme ai volumi del dispositivo precedente.</span><span class="sxs-lookup"><span data-stu-id="8bde0-157">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       <span data-ttu-id="8bde0-158">Se il contenitore del volume di cui è stato eseguito il failover ha volumi aggiunti in locale, verrà eseguito il failover di questi volumi come volumi a livelli.</span><span class="sxs-lookup"><span data-stu-id="8bde0-158">If the volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="8bde0-159">I volumi aggiunti in locale non sono attualmente supportati in un'appliance cloud StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8bde0-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Visualizzare i contenitori dei volumi di destinazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="8bde0-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8bde0-161">Next steps</span></span>

* <span data-ttu-id="8bde0-162">Dopo aver eseguito un failover, può essere necessario [disattivare o eliminare il dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="8bde0-162">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="8bde0-163">Per informazioni sull'uso del servizio Gestione dispositivi StorSimple, vedere [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md) (Usare il servizio Gestione dispositivi StorSimple per amministrare il dispositivo StorSimple).</span><span class="sxs-lookup"><span data-stu-id="8bde0-163">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

