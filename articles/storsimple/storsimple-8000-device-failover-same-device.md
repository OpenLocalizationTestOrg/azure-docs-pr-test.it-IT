---
title: Failover e ripristino di emergenza di StorSimple per dispositivi serie 8000| Microsoft Docs
description: Informazioni su come effettuare il failover di un dispositivo StorSimple sullo stesso dispositivo.
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
ms.openlocfilehash: acc8929dc3476e9590e8e4d9526b38b7c0719570
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-your-storsimple-physical-device-to-same-device"></a><span data-ttu-id="653d2-103">Effettuare il failover di un dispositivo fisico StorSimple sullo stesso dispositivo</span><span class="sxs-lookup"><span data-stu-id="653d2-103">Fail over your StorSimple physical device to same device</span></span>

## <a name="overview"></a><span data-ttu-id="653d2-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="653d2-104">Overview</span></span>

<span data-ttu-id="653d2-105">Questa esercitazione descrive i passaggi necessari per effettuare il failover di un dispositivo fisico StorSimple serie 8000 sul dispositivo stesso in caso di emergenza.</span><span class="sxs-lookup"><span data-stu-id="653d2-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to itself if there is a disaster.</span></span> <span data-ttu-id="653d2-106">StorSimple usa la funzionalità di failover del dispositivo per eseguire la migrazione dei dati da un dispositivo fisico di origine nel data center a un altro dispositivo fisico.</span><span class="sxs-lookup"><span data-stu-id="653d2-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="653d2-107">Le indicazioni fornite in questa esercitazione si applicano ai dispositivi fisici StorSimple serie 8000 in cui sono installate le versioni software Update 3 e successive.</span><span class="sxs-lookup"><span data-stu-id="653d2-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="653d2-108">Per altre informazioni sul failover dei dispositivi e su come viene usato per il ripristino di emergenza, vedere [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md) (Failover e ripristino di emergenza per dispositivi StorSimple serie 8000).</span><span class="sxs-lookup"><span data-stu-id="653d2-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="653d2-109">Per effettuare il failover di un dispositivo fisico su un altro dispositivo fisico, vedere [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md) (Failover sullo stesso dispositivo fisico StorSimple).</span><span class="sxs-lookup"><span data-stu-id="653d2-109">To fail over a physical device to another physical device, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="653d2-110">Per effettuare il failover di un dispositivo fisico StorSimple su un'appliance cloud StorSimple, vedere [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md) (Failover su un'appliance cloud StorSimple).</span><span class="sxs-lookup"><span data-stu-id="653d2-110">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="653d2-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="653d2-111">Prerequisites</span></span>

- <span data-ttu-id="653d2-112">Assicurarsi di aver esaminato le considerazioni relative al failover dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="653d2-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="653d2-113">Per altre informazioni, vedere [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md) (Considerazioni comuni per il failover dei dispositivi).</span><span class="sxs-lookup"><span data-stu-id="653d2-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-to-fail-over-to-the-same-device"></a><span data-ttu-id="653d2-114">Procedura per il failover sullo stesso dispositivo</span><span class="sxs-lookup"><span data-stu-id="653d2-114">Steps to fail over to the same device</span></span>

<span data-ttu-id="653d2-115">Per effettuare il failover sullo stesso dispositivo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="653d2-115">Perform the following steps if you need to fail over to the same device.</span></span>

1. <span data-ttu-id="653d2-116">Acquisire snapshot nel cloud di tutti i volumi nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="653d2-116">Take cloud snapshots of all the volumes in your device.</span></span> <span data-ttu-id="653d2-117">Per altre informazioni, vedere [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md) (Usare il servizio Gestione dispositivi StorSimple per creare backup).</span><span class="sxs-lookup"><span data-stu-id="653d2-117">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="653d2-118">Ripristinare le impostazioni predefinite del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="653d2-118">Reset your device to factory defaults.</span></span> <span data-ttu-id="653d2-119">Seguire le istruzioni dettagliate in [come ripristinare le impostazioni predefinite di un dispositivo StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="653d2-119">Follow the detailed instructions in [how to reset a StorSimple device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="653d2-120">Passare al servizio Gestione dispositivi StorSimple e selezionare **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="653d2-120">Go to the StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="653d2-121">Nel pannello **Dispositivi** il dispositivo precedente dovrebbe essere visualizzato come **Offline**.</span><span class="sxs-lookup"><span data-stu-id="653d2-121">In the **Devices** blade, the old device should show as **Offline**.</span></span>

    ![Dispositivo di origine offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="653d2-123">Configurare il dispositivo e registrarlo di nuovo nel servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="653d2-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="653d2-124">Il dispositivo appena registrato verrà visualizzato come **Pronto per la configurazione**.</span><span class="sxs-lookup"><span data-stu-id="653d2-124">The newly registered device should show as **Ready to set up**.</span></span> <span data-ttu-id="653d2-125">Il nuovo dispositivo avrà lo stesso nome del dispositivo precedente, ma con l'aggiunta di un valore numerico per indicare il ripristino delle impostazioni predefinite e la nuova registrazione.</span><span class="sxs-lookup"><span data-stu-id="653d2-125">The device name for the new device is the same as the old device but appended with a numeral to indicate that the device was reset to factory default and registered again.</span></span>

    ![Dispositivo appena registrato pronto per la configurazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="653d2-127">Completare la configurazione del nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="653d2-127">For the new device, complete the device setup.</span></span> <span data-ttu-id="653d2-128">Per altre informazioni, vedere [Passaggio 4: Completare la configurazione minima del dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="653d2-128">For more information, go to [Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="653d2-129">Nel pannello **Dispositivi** lo stato del dispositivo passa a **Online**.</span><span class="sxs-lookup"><span data-stu-id="653d2-129">On the **Devices** blade, the status of the device changes to **Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="653d2-130">**Completare prima la configurazione minima, altrimenti il ripristino di emergenza potrebbe non riuscire.**</span><span class="sxs-lookup"><span data-stu-id="653d2-130">**Complete the minimum configuration first, or your DR may fail.**</span></span>

    ![Dispositivo appena registrato online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="653d2-132">Selezionare il dispositivo precedente (stato offline) e dalla barra dei comandi fare clic su **Failover**.</span><span class="sxs-lookup"><span data-stu-id="653d2-132">Select the old device (status offline) and from the command bar, click **Fail over**.</span></span> <span data-ttu-id="653d2-133">Nel pannello **Failover** selezionare il dispositivo precedente come origine e specificare come dispositivo di destinazione il dispositivo appena registrato.</span><span class="sxs-lookup"><span data-stu-id="653d2-133">In the **Fail over** blade, select old device as the source and specify the target device as the newly registered device.</span></span>

    ![Riepilogo del failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="653d2-135">Per istruzioni dettagliate, fare riferimento a [Failover su un altro dispositivo fisico](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="653d2-135">For detailed instructions, refer to [Fail over to another physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="653d2-136">Verrà creato un processo di ripristino del dispositivo che è possibile monitorare dal pannello **Processi**.</span><span class="sxs-lookup"><span data-stu-id="653d2-136">A device restore job is created that you can monitor from the **Jobs** blade.</span></span>

8. <span data-ttu-id="653d2-137">Al termine del processo, accedere al nuovo dispositivo e passare al pannello **Contenitori dei volumi**.</span><span class="sxs-lookup"><span data-stu-id="653d2-137">After the job has successfully completed, access the new device and navigate to the **Volume containers** blade.</span></span> <span data-ttu-id="653d2-138">Verificare che sia stata eseguita la migrazione di tutti i contenitori dei volumi dal dispositivo precedente al nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="653d2-138">Verify that all the volume containers from the old device have migrated to the new device.</span></span>

   ![Migrazione dei contenitori dei volumi eseguita](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="653d2-140">Al termine del failover, è possibile disattivare ed eliminare il dispositivo precedente dal portale.</span><span class="sxs-lookup"><span data-stu-id="653d2-140">After the failover is complete, you can deactivate and delete the old device from the portal.</span></span> <span data-ttu-id="653d2-141">Selezionare il dispositivo precedente (offline), fare clic con il pulsante destro del mouse e quindi selezionare **Disattiva**.</span><span class="sxs-lookup"><span data-stu-id="653d2-141">Select the old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="653d2-142">Dopo la disattivazione, lo stato del dispositivo verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="653d2-142">After the device is deactivated, the status of the device is updated.</span></span>

     ![Dispositivo di origine disattivato](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="653d2-144">Selezionare il dispositivo disattivato, fare clic con il pulsante destro del mouse e quindi selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="653d2-144">Select the deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="653d2-145">Il dispositivo verrà eliminato dall'elenco di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="653d2-145">This deletes the device from the list of devices.</span></span>

    ![Dispositivo di origine eliminato](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="653d2-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="653d2-147">Next steps</span></span>

* <span data-ttu-id="653d2-148">Dopo aver eseguito un failover, può essere necessario [disattivare o eliminare il dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="653d2-148">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="653d2-149">Per informazioni sull'uso del servizio Gestione dispositivi StorSimple, vedere [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md) (Usare il servizio Gestione dispositivi StorSimple per amministrare il dispositivo StorSimple).</span><span class="sxs-lookup"><span data-stu-id="653d2-149">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

