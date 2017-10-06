---
title: aaaManage il catalogo di backup di StorSimple | Documenti Microsoft
description: Viene illustrato come toouse hello toolist pagina di gestione di dispositivi StorSimple servizio catalogo di backup, selezionare ed eliminare i set di backup.
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="6c2a7-103">Utilizzare toomanage servizio di gestione di dispositivi StorSimple hello il catalogo di backup</span><span class="sxs-lookup"><span data-stu-id="6c2a7-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="6c2a7-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6c2a7-104">Overview</span></span>
<span data-ttu-id="6c2a7-105">servizio di gestione di dispositivi StorSimple Hello **catalogo di Backup** pannello vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuale o pianificato.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="6c2a7-106">È possibile utilizzare tutti i backup hello di toolist questa pagina per un criterio di backup o un volume, seleziona o eliminare i backup, o utilizzare un backup toorestore o clonare un volume.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="6c2a7-107">In questa esercitazione viene illustrato come eliminare toolist e selezionare un set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="6c2a7-108">toolearn come toorestore il dispositivo di backup, andare troppo[ripristinare il dispositivo da un set di backup](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="6c2a7-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="6c2a7-109">toolearn come tooclone un volume, andare troppo[clonare un volume StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="6c2a7-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="6c2a7-111">Hello **catalogo di Backup** pannello fornisce un toonarrow query la selezione di set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="6c2a7-112">È possibile filtrare i set di backup hello che vengono recuperati, in base a hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="6c2a7-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="6c2a7-113">**Dispositivo** : dispositivo hello in cui hello è stato creato il set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="6c2a7-114">**Criteri di backup o il Volume** : hello criteri di backup o di volume associato a questo set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="6c2a7-115">**Da e a** : hello intervallo di data e ora, quando i set di backup hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="6c2a7-116">Hello set di backup filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c2a7-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="6c2a7-117">**Nome** : hello nome del criterio di backup hello o volume associato al set di backup hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="6c2a7-118">**Dimensioni** : hello dimensioni effettive hello del set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="6c2a7-119">**Data creazione** : hello data e l'ora di creazione dei backup hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="6c2a7-120">**Tipo** : i set di backup possono essere snapshot in locale o del cloud.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="6c2a7-121">Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente nel dispositivo hello, mentre uno snapshot nel cloud si riferisce toohello backup dei dati di volume che risiedono nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="6c2a7-122">Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="6c2a7-123">**Avviato da** : hello backup possono essere avviati automaticamente da una pianificazione o manualmente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="6c2a7-124">È possibile utilizzare i backup tooschedule un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="6c2a7-125">In alternativa, è possibile utilizzare hello **eseguire backup** opzione tootake un backup manuale.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="6c2a7-126">Elencare i set di backup di un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="6c2a7-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="6c2a7-127">Questa procedura completa di hello toolist tutti i backup di hello per un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="6c2a7-128">set di backup toolist</span><span class="sxs-lookup"><span data-stu-id="6c2a7-128">toolist backup sets</span></span>
1. <span data-ttu-id="6c2a7-129">Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **catalogo di Backup**.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="6c2a7-130">Hello selezioni dei filtri come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6c2a7-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="6c2a7-131">Specificare l'intervallo di tempo hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="6c2a7-132">Selezionare i dispositivi appropriati hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="6c2a7-133">Filtrare in base **criteri di Backup** tooview hello backup hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="6c2a7-134">Selezionare dall'elenco a discesa dei criteri di backup hello **tutti** tooview tutti hello i backup selezionati hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="6c2a7-135">Fare clic su **applica** tooexecute questa query.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="6c2a7-136">i backup Hello associati al criterio di backup hello selezionato verrà visualizzato nell'elenco di hello dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="6c2a7-138">Selezionare un set di backup</span><span class="sxs-lookup"><span data-stu-id="6c2a7-138">Select a backup set</span></span>
<span data-ttu-id="6c2a7-139">Completare hello seguendo i passaggi tooselect del set di un backup per un volume o criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="6c2a7-140">tooselect un set di backup</span><span class="sxs-lookup"><span data-stu-id="6c2a7-140">tooselect a backup set</span></span>
1. <span data-ttu-id="6c2a7-141">Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **catalogo di Backup**.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="6c2a7-142">Hello selezioni dei filtri come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6c2a7-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="6c2a7-143">Specificare l'intervallo di tempo hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="6c2a7-144">Selezionare i dispositivi appropriati hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="6c2a7-145">Filtrare in base volumi o criteri di backup per il backup di hello che si desidera tooselect.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="6c2a7-146">Fare clic su **applica** tooexecute questa query.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="6c2a7-147">Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="6c2a7-149">Selezionare ed espandere un set di backup</span><span class="sxs-lookup"><span data-stu-id="6c2a7-149">Select and expand a backup set.</span></span> <span data-ttu-id="6c2a7-150">È ora possibile visualizzare i set di backup hello suddivisi in base volumi hello in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="6c2a7-151">Hello **ripristinare** e **eliminare** opzioni sono disponibili tramite hello menu di scelta rapida (rapida) per i set di backup hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="6c2a7-152">È possibile eseguire una di queste azioni nel set di backup hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="6c2a7-154">Eliminare un set di backup</span><span class="sxs-lookup"><span data-stu-id="6c2a7-154">Delete a backup set</span></span>
<span data-ttu-id="6c2a7-155">Eliminare un backup quando non si desidera più tooretain hello dei dati.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="6c2a7-156">Eseguire hello seguendo i passaggi toodelete un set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="6c2a7-157">toodelete un set di backup</span><span class="sxs-lookup"><span data-stu-id="6c2a7-157">toodelete a backup set</span></span>
 <span data-ttu-id="6c2a7-158">Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **catalogo di Backup**.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="6c2a7-159">Hello selezioni dei filtri come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6c2a7-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="6c2a7-160">Specificare l'intervallo di tempo hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="6c2a7-161">Selezionare i dispositivi appropriati hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="6c2a7-162">Filtrare in base volumi o criteri di backup per il backup di hello che si desidera tooselect.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="6c2a7-163">Fare clic su **applica** tooexecute questa query.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="6c2a7-164">Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="6c2a7-166">Selezionare ed espandere un set di backup</span><span class="sxs-lookup"><span data-stu-id="6c2a7-166">Select and expand a backup set.</span></span> <span data-ttu-id="6c2a7-167">È ora possibile visualizzare i set di backup hello suddivisi in base volumi hello in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="6c2a7-168">Hello **ripristinare** e **eliminare** opzioni sono disponibili tramite hello menu di scelta rapida (rapida) per i set di backup hello.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="6c2a7-169">Fare doppio clic su set di backup selezionato hello e selezionare il menu di scelta rapida hello **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="6c2a7-171">Quando viene richiesta la conferma, esaminare le informazioni visualizzata hello e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="6c2a7-172">backup selezionato Hello viene eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-172">hello selected backup is deleted permanently.</span></span>

    ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="6c2a7-174">Si riceverà la notifica quando l'eliminazione di hello è in corso e quando ha terminato correttamente.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="6c2a7-175">Dopo l'eliminazione di hello, refresh query hello in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="6c2a7-176">set di backup Hello eliminato non verrà più visualizzato nell'elenco di hello dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="6c2a7-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Passare toobackup catalogo](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="6c2a7-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c2a7-178">Next steps</span></span>
* <span data-ttu-id="6c2a7-179">Informazioni su come troppo[utilizzare hello toorestore catalogo di backup del dispositivo da un set di backup](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="6c2a7-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="6c2a7-180">Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6c2a7-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

