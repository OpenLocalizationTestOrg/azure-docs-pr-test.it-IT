---
title: failover aaaStorSimple, il ripristino di emergenza per i dispositivi 8000 serie | Documenti Microsoft
description: Informazioni su come toofail tramite il toohello dispositivo StorSimple stesso dispositivo.
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="12f71-103">Eseguire il failover del dispositivo di toosame dispositivo fisico StorSimple</span><span class="sxs-lookup"><span data-stu-id="12f71-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="12f71-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="12f71-104">Overview</span></span>

<span data-ttu-id="12f71-105">In questa esercitazione descrive hello passaggi necessari toofail su un tooitself di dispositivo fisico StorSimple 8000 series se si verifica un'emergenza.</span><span class="sxs-lookup"><span data-stu-id="12f71-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="12f71-106">StorSimple Usa dati toomigrate funzionalità hello dispositivo failover da un dispositivo fisico di origine nel dispositivo fisico di hello datacenter tooanother.</span><span class="sxs-lookup"><span data-stu-id="12f71-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="12f71-107">materiale sussidiario Hello in questa esercitazione si applica a dispositivi fisici serie 8000 tooStorSimple con le versioni di software Update 3 e successive.</span><span class="sxs-lookup"><span data-stu-id="12f71-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="12f71-108">toolearn ulteriori informazioni su failover del dispositivo e la modalità di toorecover utilizzato da un'emergenza, andare troppo[Failover e ripristino di emergenza per i dispositivi della serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="12f71-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="12f71-109">toofail su un dispositivo fisico tooanother dispositivo fisico, andare troppo[failover toohello stesso dispositivo fisico StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="12f71-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="12f71-110">toofail su un tooa dispositivo fisico StorSimple Appliance di Cloud di StorSimple, andare troppo[failover tooa StorSimple Appliance di Cloud](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="12f71-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="12f71-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="12f71-111">Prerequisites</span></span>

- <span data-ttu-id="12f71-112">Assicurarsi di aver esaminato considerazioni hello per failover del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12f71-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="12f71-113">Per ulteriori informazioni, visitare troppo[considerazioni comuni per il failover dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="12f71-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="12f71-114">Passaggi toofail su toohello stesso dispositivo</span><span class="sxs-lookup"><span data-stu-id="12f71-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="12f71-115">Eseguire operazioni se è necessario toofail su toohello hello stesso dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12f71-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="12f71-116">Creare snapshot cloud di tutti i volumi di hello nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12f71-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="12f71-117">Per ulteriori informazioni, visitare troppo[toocreate i backup del servizio di utilizzare Gestione periferiche di StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="12f71-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="12f71-118">Reimpostare le impostazioni predefinite del dispositivo toofactory.</span><span class="sxs-lookup"><span data-stu-id="12f71-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="12f71-119">Seguire hello dettagliate in [come impostazioni predefinite tooreset un toofactory dispositivo StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="12f71-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="12f71-120">Il servizio di gestione di dispositivi StorSimple toohello go e quindi selezionare **dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="12f71-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="12f71-121">In hello **dispositivi** pannello dispositivo precedente hello dovrebbe risultare **Offline**.</span><span class="sxs-lookup"><span data-stu-id="12f71-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Dispositivo di origine offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="12f71-123">Configurare il dispositivo e registrarlo di nuovo nel servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="12f71-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="12f71-124">Hello dispositivo appena registrato dovrebbe risultare **pronto tooset backup**.</span><span class="sxs-lookup"><span data-stu-id="12f71-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="12f71-125">nome del dispositivo per il nuovo dispositivo di hello Hello è hello stesso dispositivo precedente hello ma aggiunto con una numerazione tooindicate dispositivo hello stato reimpostazione toofactory predefinito e registrati nuovamente.</span><span class="sxs-lookup"><span data-stu-id="12f71-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![Dispositivo appena registrato tooset pronto backup](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="12f71-127">Per una nuova periferica hello, completare la configurazione di dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="12f71-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="12f71-128">Per ulteriori informazioni, visitare troppo[passaggio 4: completare l'installazione minima del dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="12f71-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="12f71-129">In hello **dispositivi** pannello stato hello del dispositivo hello diventa troppo**Online**.</span><span class="sxs-lookup"><span data-stu-id="12f71-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="12f71-130">**Completare la configurazione minima di hello prima o il ripristino di emergenza potrebbe non riuscire.**</span><span class="sxs-lookup"><span data-stu-id="12f71-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Dispositivo appena registrato online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="12f71-132">Selezionare il dispositivo precedente hello (stato non in linea) e dalla barra dei comandi di hello, fare clic su **failover**.</span><span class="sxs-lookup"><span data-stu-id="12f71-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="12f71-133">In hello **failover** pannello selezionare dispositivo precedente come origine di hello e specificare il dispositivo di destinazione hello hello appena registrato dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12f71-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Riepilogo del failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="12f71-135">Per istruzioni dettagliate, vedere troppo[failover dispositivo fisico tooanother](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="12f71-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="12f71-136">Viene creato un processo di ripristino di dispositivo che è possibile monitorare da hello **processi** blade.</span><span class="sxs-lookup"><span data-stu-id="12f71-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="12f71-137">Al termine il processo di hello, accedere di nuovo dispositivo hello e passare toohello **contenitori di volumi** blade.</span><span class="sxs-lookup"><span data-stu-id="12f71-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="12f71-138">Verificare che tutti i contenitori di volumi di hello dispositivo precedente hello siano stati migrati toohello nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12f71-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Migrazione dei contenitori dei volumi eseguita](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="12f71-140">Al termine del failover hello, è possibile disattivare ed eliminare dispositivo precedente hello dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="12f71-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="12f71-141">Selezionare hello precedente dispositivo (offline), pulsante destro del mouse, quindi **disattiva**.</span><span class="sxs-lookup"><span data-stu-id="12f71-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="12f71-142">Dopo la disattivazione di dispositivo hello, hello del dispositivo hello viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="12f71-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Dispositivo di origine disattivato](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="12f71-144">Seleziona hello disattivato dispositivo pulsante destro del mouse e quindi selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="12f71-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="12f71-145">Ciò elimina dispositivo hello dall'elenco di hello dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="12f71-145">This deletes hello device from hello list of devices.</span></span>

    ![Dispositivo di origine eliminato](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="12f71-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12f71-147">Next steps</span></span>

* <span data-ttu-id="12f71-148">Dopo aver eseguito un failover, potrebbe essere troppo[disattivare o eliminare il dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="12f71-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="12f71-149">Per informazioni su come toouse hello dispositivo StorSimple Manager service, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="12f71-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

