---
title: un volume StorSimple da backup aaaRestore | Documenti Microsoft
description: Viene illustrato come toouse hello toorestore pagina di StorSimple Manager servizio catalogo di Backup un volume StorSimple da un set di backup.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="2f0d5-103">Ripristinare un volume StorSimple da un set di backup</span><span class="sxs-lookup"><span data-stu-id="2f0d5-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="2f0d5-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2f0d5-104">Overview</span></span>
<span data-ttu-id="2f0d5-105">Hello **catalogo di Backup** pagina vengono visualizzati tutti i set di backup di hello che vengono creati quando sono stati eseguiti backup manuali o automatizzati.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="2f0d5-106">È possibile utilizzare tutti i backup hello di toolist questa pagina per un criterio di backup o un volume, seleziona o eliminare i backup, o utilizzare un backup toorestore o clonare un volume.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![Pagina catalogo di backup](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="2f0d5-108">In questa esercitazione viene illustrato come hello toouse **catalogo di Backup** pagina toorestore un volume nel dispositivo da un set di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="2f0d5-109">Come toouse hello catalogo di backup</span><span class="sxs-lookup"><span data-stu-id="2f0d5-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="2f0d5-110">Hello **catalogo di Backup** pagina fornisce una query che consente di toonarrow la selezione di set di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="2f0d5-111">È possibile filtrare hello set di backup che vengono recuperati in base a hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="2f0d5-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="2f0d5-112">**Dispositivo** : dispositivo hello in cui hello è stato creato il set di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="2f0d5-113">**Criteri di backup** o **volume** : hello criteri di backup o di volume associato a questo set di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="2f0d5-114">**Da** e **a** : hello intervallo di data e ora, quando i set di backup hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="2f0d5-115">Hello set di backup filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f0d5-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="2f0d5-116">**Nome** : hello nome del criterio di backup hello o volume associato al set di backup hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="2f0d5-117">**Dimensioni** : hello dimensioni effettive hello del set di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="2f0d5-118">**Creare in** : hello data e l'ora di creazione dei backup hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="2f0d5-119">**Tipo** : i set di backup possono essere snapshot in locale o del cloud.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="2f0d5-120">Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente nel dispositivo hello, mentre uno snapshot nel cloud si riferisce toohello backup dei dati di volume che risiedono nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="2f0d5-121">Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="2f0d5-122">**Avviato da** : hello backup possono essere avviati automaticamente in base tooa pianificazione o manualmente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="2f0d5-123">(È possibile utilizzare i backup tooschedule un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="2f0d5-124">In alternativa, è possibile utilizzare hello **eseguire backup** opzione tootake un backup interattivo.)</span><span class="sxs-lookup"><span data-stu-id="2f0d5-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="2f0d5-125">Come toorestore il volume StorSimple da un backup</span><span class="sxs-lookup"><span data-stu-id="2f0d5-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="2f0d5-126">È possibile utilizzare hello **catalogo di Backup** pagina toorestore il volume StorSimple da un backup specifico.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="2f0d5-127">Ripristino da un backup sostituirà i volumi esistenti da un backup hello hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="2f0d5-128">Questo può causare la perdita di hello di tutti i dati dopo che è stato eseguito il backup di hello è stato scritto.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="2f0d5-129">Prima di avviare un ripristino in un volume, verificare che il volume di hello è offline.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="2f0d5-130">Sarà anche necessario innanzitutto tootake hello volume offline hello host e quindi hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="2f0d5-131">Seguire i passaggi di hello in [portare offline un volume](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="2f0d5-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="2f0d5-132">Eseguire hello seguendo i passaggi toorestore un volume da un set di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="2f0d5-133">toorestore da un set di backup</span><span class="sxs-lookup"><span data-stu-id="2f0d5-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="2f0d5-134">Nella pagina del servizio StorSimple Manager hello, fare clic su hello **catalogo di Backup** scheda.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![Catalogo di backup](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="2f0d5-136">Procedura di selezione di un set di backup:</span><span class="sxs-lookup"><span data-stu-id="2f0d5-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="2f0d5-137">Selezionare i dispositivi appropriati hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="2f0d5-138">Nell'elenco a discesa hello, scegliere hello volumi o criteri di backup per il backup di hello che si desidera tooselect.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="2f0d5-139">Specificare l'intervallo di tempo hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="2f0d5-140">Fare clic sull'icona di controllo hello</span><span class="sxs-lookup"><span data-stu-id="2f0d5-140">Click hello check icon</span></span> ![icona del segno di spunta](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="2f0d5-142">tooexecute questa query.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="2f0d5-143">Hello i backup associati hello selezionato volumi o criteri di backup dovrebbero essere visualizzato nell'elenco di hello dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="2f0d5-144">Espandere i volumi hello set di backup tooview hello associata.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="2f0d5-145">Questi volumi devono essere portati offline sull'host di hello e dispositivo prima di poter ripristinare.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="2f0d5-146">Seguire i passaggi di hello in [portare offline un volume](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="2f0d5-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2f0d5-147">Assicurarsi di avere eseguito hello volumi sull'host hello in primo luogo, prima di portare offline i volumi di hello sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="2f0d5-148">Se non si adotta volumi hello offline nell'host di hello, potenzialmente provocare il danneggiamento toodata.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="2f0d5-149">Selezionare un set di backup.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-149">Select a backup set.</span></span> <span data-ttu-id="2f0d5-150">Fare clic su **ripristinare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="2f0d5-151">Verrà richiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-151">You will be prompted for confirmation.</span></span> 
   
    ![Pagina di conferma](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="2f0d5-153">Esaminare le informazioni di ripristino hello e fare clic sull'icona di controllo hello ![il segno di spunta](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="2f0d5-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="2f0d5-154">Verrà avviato un processo di ripristino che è possibile visualizzare accedendo hello **processi** pagina.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="2f0d5-155">Dopo il ripristino di hello, è possibile verificare che il contenuto di hello dei volumi è sostituito dai volumi backup hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d5-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="2f0d5-156">![Video disponibile](./media/storsimple-restore-from-backup-set/Video_icon.png)**Video disponibile**</span><span class="sxs-lookup"><span data-stu-id="2f0d5-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="2f0d5-157">Fare clic su un video che illustra come usare clone hello e ripristinare le funzionalità nei file eliminato toorecover StorSimple, toowatch [qui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="2f0d5-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f0d5-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f0d5-158">Next steps</span></span>
* <span data-ttu-id="2f0d5-159">Informazioni su come troppo[volumi StorSimple gestire](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="2f0d5-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="2f0d5-160">Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="2f0d5-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

