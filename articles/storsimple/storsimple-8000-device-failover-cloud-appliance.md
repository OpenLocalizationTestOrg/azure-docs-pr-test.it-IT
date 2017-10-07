---
title: failover aaaStorSimple, ripristino di emergenza tooa StorSimple Appliance di Cloud | Documenti Microsoft
description: Informazioni su cloud toofail tramite il tooa di dispositivo fisico StorSimple 8000 series appliance.
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
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="f7c5d-103">Eseguire il failover tooyour StorSimple Appliance di Cloud</span><span class="sxs-lookup"><span data-stu-id="f7c5d-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="f7c5d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f7c5d-104">Overview</span></span>

<span data-ttu-id="f7c5d-105">Questa esercitazione descrive hello passaggi necessari toofail su un tooa di dispositivi fisici serie StorSimple 8000 StorSimple Appliance di Cloud se si verifica un'emergenza.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="f7c5d-106">StorSimple Usa dati toomigrate funzionalità hello dispositivo failover da un dispositivo fisico di origine nel dispositivo di hello datacenter tooa cloud in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="f7c5d-107">materiale sussidiario di Hello in questa esercitazione si applica a dispositivi fisici serie di tooStorSimple 8000 e Appliance di cloud con le versioni di software Update 3 e successive.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="f7c5d-108">toolearn ulteriori informazioni su failover del dispositivo e la modalità di toorecover utilizzato da un'emergenza, andare troppo[Failover e ripristino di emergenza per i dispositivi della serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="f7c5d-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="f7c5d-109">toofail su un dispositivo di fisica della tooanother dispositivo fisico del StorSimple, andare troppo[failover dispositivo fisico StorSimple tooa](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="f7c5d-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="f7c5d-110">toofail su tooitself un dispositivo, andare troppo[failover toohello stesso dispositivo fisico StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="f7c5d-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7c5d-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f7c5d-111">Prerequisites</span></span>

- <span data-ttu-id="f7c5d-112">Assicurarsi di aver esaminato considerazioni hello per failover del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="f7c5d-113">Per ulteriori informazioni, visitare troppo[considerazioni comuni per il failover dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="f7c5d-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="f7c5d-114">Prima di eseguire questa procedura, è necessario disporre di un'appliance cloud StorSimple creata e configurata.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="f7c5d-115">Se in esecuzione Aggiorna versione 3 o versioni successive, è consigliabile utilizzare un accessorio 8020 cloud per hello ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="f7c5d-116">modello 8020 Hello è 64 TB e utilizza l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="f7c5d-117">Per ulteriori informazioni, visitare troppo[distribuire e gestire un'applicazione Cloud StorSimple](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f7c5d-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="f7c5d-118">Passaggi toofail su dispositivo cloud tooa</span><span class="sxs-lookup"><span data-stu-id="f7c5d-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="f7c5d-119">Eseguire hello seguendo i passaggi toorestore hello tooa di destinazione del dispositivo StorSimple Appliance di Cloud.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="f7c5d-120">Verificare il contenitore del volume hello desiderato toofail siano associati snapshot nel cloud.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="f7c5d-121">Per ulteriori informazioni, visitare troppo[toocreate i backup del servizio di utilizzare Gestione periferiche di StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f7c5d-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="f7c5d-122">Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="f7c5d-123">In hello **dispositivi** blade, andare toohello elenco di dispositivi connessi con il servizio.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="f7c5d-124">![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="f7c5d-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="f7c5d-125">Selezionare e fare clic sul dispositivo di origine.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-125">Select and click your source device.</span></span> <span data-ttu-id="f7c5d-126">contenitori di volumi hello che si desidera toofail sulla periferica di origine di Hello.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="f7c5d-127">Andare troppo**Impostazioni > contenitori di volumi**.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-127">Go too**Settings > Volume Containers**.</span></span>

    ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="f7c5d-129">Selezionare un contenitore di volumi di cui si desidera toofail su tooanother dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="f7c5d-130">Fare clic su elenco hello toodisplay hello volumi contenitore di volumi all'interno del contenitore.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="f7c5d-131">Selezionare un volume, il pulsante destro del mouse e fare clic su **non in linea** tootake offline volume hello.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="f7c5d-133">Ripetere questo processo per tutti i volumi di hello hello contenitore del volume.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="f7c5d-135">Passaggio di ripetizione hello precedente per tutti i contenitori dei volumi di hello desideri toofail su tooanother dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="f7c5d-136">Tornare indietro toohello **dispositivi** blade.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="f7c5d-137">Dalla barra dei comandi di hello, fare clic su **failover**.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-137">From hello command bar, click **Fail over**.</span></span>

    ![Fare clic su Failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="f7c5d-139">In hello **failover** pannello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f7c5d-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="f7c5d-140">Fare clic su **Origine**.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-140">Click **Source**.</span></span> <span data-ttu-id="f7c5d-141">Selezionare hello volume contenitori toofail su.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="f7c5d-142">**Hello solo contenitori di volumi con snapshot cloud associati e i volumi offline sono visualizzati.**</span><span class="sxs-lookup"><span data-stu-id="f7c5d-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="f7c5d-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png) (Seleziona origine)</span><span class="sxs-lookup"><span data-stu-id="f7c5d-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="f7c5d-144">Fare clic su **Destinazione**.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-144">Click **Target**.</span></span> <span data-ttu-id="f7c5d-145">Selezionare un'applicazione cloud di destinazione dall'elenco a discesa hello dei dispositivi disponibili.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="f7c5d-146">**Solo i dispositivi di hello che dispongono di sufficiente capacità tooaccommodate origine i contenitori dei volumi vengono visualizzati nell'elenco di hello.**</span><span class="sxs-lookup"><span data-stu-id="f7c5d-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![Selezionare la destinazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="f7c5d-148">Esaminare le impostazioni di failover hello in **riepilogo** e selezionare la casella di controllo di hello, che indica che i volumi hello nei contenitori di volumi selezionati sono offline.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![Esaminare le impostazioni di failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="f7c5d-150">Viene creato un processo di failover.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-150">A failover job is created.</span></span> <span data-ttu-id="f7c5d-151">failover hello toomonitor di processo, fare clic su notifica del processo hello.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![Monitorare il processo di failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="f7c5d-153">Dopo aver completato il failover hello, tornare indietro toohello **dispositivi** blade.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="f7c5d-154">Selezionare il dispositivo hello che è stato utilizzato come destinazione di hello per il failover hello.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="f7c5d-156">Fare clic su **Contenitori di volume**.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-156">Click **Volume Containers**.</span></span> <span data-ttu-id="f7c5d-157">Tutti i contenitori di volumi di hello, insieme ai volumi hello dispositivo precedente hello, dovrebbero essere elencati.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="f7c5d-158">Se il contenitore del volume hello che è stato eseguito il failover ha aggiunto in locale i volumi, tali volumi vengono eseguiti il failover come volumi a livelli.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="f7c5d-159">I volumi aggiunti in locale non sono attualmente supportati in un'appliance cloud StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f7c5d-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Visualizzare i contenitori dei volumi di destinazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="f7c5d-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7c5d-161">Next steps</span></span>

* <span data-ttu-id="f7c5d-162">Dopo aver eseguito un failover, potrebbe essere troppo[disattivare o eliminare il dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="f7c5d-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="f7c5d-163">Per informazioni su come toouse hello dispositivo StorSimple Manager service, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f7c5d-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

