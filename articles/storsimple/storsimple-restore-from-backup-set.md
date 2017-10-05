---
title: Ripristinare un volume StorSimple dal backup | Microsoft Docs
description: Viene illustrato come utilizzare la pagina del catalogo di backup del servizio StorSimple Manager per ripristinare un volume StorSimple da un set di backup.
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
ms.openlocfilehash: 12484338f5b4d489604d70a657ef0992b6267297
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="1b51a-103">Ripristinare un volume StorSimple da un set di backup</span><span class="sxs-lookup"><span data-stu-id="1b51a-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="1b51a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1b51a-104">Overview</span></span>
<span data-ttu-id="1b51a-105">Nella pagina **Catalogo di backup** vengono visualizzati tutti i set di backup creati quando si eseguono backup manuali o automatizzati.</span><span class="sxs-lookup"><span data-stu-id="1b51a-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="1b51a-106">È possibile utilizzare questa pagina per elencare tutti i backup per un criterio di backup o un volume, selezionare o eliminare i backup o utilizzare un backup per ripristinare o clonare un volume.</span><span class="sxs-lookup"><span data-stu-id="1b51a-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

 ![Pagina catalogo di backup](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="1b51a-108">Questa esercitazione illustra come usare la pagina **Catalogo backup** per ripristinare un volume sul dispositivo da un set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="1b51a-109">Come utilizzare il catalogo di backup</span><span class="sxs-lookup"><span data-stu-id="1b51a-109">How to use the backup catalog</span></span>
<span data-ttu-id="1b51a-110">La pagina **Catalogo di backup** fornisce una query che consente di limitare la selezione del set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="1b51a-111">È possibile filtrare i set di backup che vengono recuperati in base ai parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b51a-111">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="1b51a-112">**Dispositivo** : il dispositivo in cui è stato creato il set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-112">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="1b51a-113">**Criterio di backup** o **Volume**: il criterio di backup o volume associato a questo set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="1b51a-114">**Da** e **A**: intervallo di data e ora di creazione del set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-114">**From** and **To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="1b51a-115">I set di backup filtrati vengono quindi catalogati in base ai seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="1b51a-115">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="1b51a-116">**Nome** : nome del criterio di backup o volume associato al set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-116">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="1b51a-117">**Dimensioni** : dimensione effettiva del set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-117">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="1b51a-118">**Creato il** : data e ora di creazione dei backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-118">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="1b51a-119">**Tipo** : i set di backup possono essere snapshot in locale o del cloud.</span><span class="sxs-lookup"><span data-stu-id="1b51a-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="1b51a-120">Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente sul dispositivo, mentre uno snapshot del cloud si riferisce al backup dei dati di volume che risiedono nel cloud.</span><span class="sxs-lookup"><span data-stu-id="1b51a-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="1b51a-121">Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.</span><span class="sxs-lookup"><span data-stu-id="1b51a-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="1b51a-122">**Avviato da** : i backup possono essere avviati automaticamente in base a una pianificazione o manualmente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="1b51a-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="1b51a-123">Per pianificare i backup, è possibile utilizzare un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-123">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="1b51a-124">In alternativa, è possibile utilizzare l’opzione **Esegui backup** per eseguire un backup interattivo.</span><span class="sxs-lookup"><span data-stu-id="1b51a-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="1b51a-125">Come ripristinare il volume di StorSimple da un backup</span><span class="sxs-lookup"><span data-stu-id="1b51a-125">How to restore your StorSimple volume from a backup</span></span>
<span data-ttu-id="1b51a-126">È possibile usare la pagina **Catalogo di backup** per ripristinare il volume StorSimple da un backup specifico.</span><span class="sxs-lookup"><span data-stu-id="1b51a-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="1b51a-127">Il ripristino da un backup sostituisce i volumi esistenti dal backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-127">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="1b51a-128">Ciò può comportare la perdita dei dati scritti dopo l'esecuzione del backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-128">This may cause the loss of any data that was written after the backup was taken.</span></span>
> 
> 

<span data-ttu-id="1b51a-129">Prima di avviare un ripristino su un volume, assicurarsi che il volume sia offline.</span><span class="sxs-lookup"><span data-stu-id="1b51a-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span></span> <span data-ttu-id="1b51a-130">È necessario portare offline il volume prima nell'host e poi sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b51a-130">You will need to take the volume offline on the host first and then the device.</span></span> <span data-ttu-id="1b51a-131">Seguire la procedura illustrata in [Portare un volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="1b51a-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="1b51a-132">Eseguire i passaggi seguenti per ripristinare un volume da un set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-132">Perform the following steps to restore a volume from a backup set.</span></span>

### <a name="to-restore-from-a-backup-set"></a><span data-ttu-id="1b51a-133">Per effettuare il ripristino da un set di backup</span><span class="sxs-lookup"><span data-stu-id="1b51a-133">To restore from a backup set</span></span>
1. <span data-ttu-id="1b51a-134">Nella pagina del servizio StorSimple Manager, fare clic sulla scheda **Catalogo di backup** .</span><span class="sxs-lookup"><span data-stu-id="1b51a-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
   
    ![Catalogo di backup](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="1b51a-136">Procedura di selezione di un set di backup:</span><span class="sxs-lookup"><span data-stu-id="1b51a-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="1b51a-137">Selezionare un dispositivo appropriato.</span><span class="sxs-lookup"><span data-stu-id="1b51a-137">Select the appropriate device.</span></span>
   2. <span data-ttu-id="1b51a-138">Nell'elenco a discesa, scegliere il volume o il criterio di backup per il backup che si desidera selezionare.</span><span class="sxs-lookup"><span data-stu-id="1b51a-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="1b51a-139">Specificare l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="1b51a-139">Specify the time range.</span></span>
   4. <span data-ttu-id="1b51a-140">Fare clic sull'icona del segno di spunta </span><span class="sxs-lookup"><span data-stu-id="1b51a-140">Click the check icon</span></span> ![icona del segno di spunta](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="1b51a-142">per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="1b51a-142">to execute this query.</span></span>
      
      <span data-ttu-id="1b51a-143">I backup associati al volume selezionato o al criterio di backup dovrebbero essere visualizzati nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="1b51a-144">Espandere il set di backup per visualizzare i volumi associati.</span><span class="sxs-lookup"><span data-stu-id="1b51a-144">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="1b51a-145">Questi volumi devono essere disconnessi nell'host e nel dispositivo prima di poterli ripristinare.</span><span class="sxs-lookup"><span data-stu-id="1b51a-145">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="1b51a-146">Seguire la procedura illustrata in [Portare un volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="1b51a-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="1b51a-147">Assicurarsi, in primo luogo, di aver disattivato tutti i volumi sull'host, prima di disattivarli sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b51a-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="1b51a-148">Se non si eseguono i volumi offline nell'host, si potrebbe verificare un danneggiamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="1b51a-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="1b51a-149">Selezionare un set di backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-149">Select a backup set.</span></span> <span data-ttu-id="1b51a-150">Fare clic su **Ripristina** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="1b51a-150">Click **Restore** at the bottom of the page.</span></span>
5. <span data-ttu-id="1b51a-151">Verrà richiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="1b51a-151">You will be prompted for confirmation.</span></span> 
   
    ![Pagina di conferma](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="1b51a-153">Esaminare le informazioni di ripristino e fare clic sull'icona di segno di spunta ![icona del segno di spunta](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="1b51a-153">Review the restore information and click the check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="1b51a-154">In questo modo viene avviato un processo di ripristino che è possibile visualizzare accedendo alla pagina **Processi** .</span><span class="sxs-lookup"><span data-stu-id="1b51a-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span></span> 
7. <span data-ttu-id="1b51a-155">Dopo aver completato il ripristino, è possibile verificare che i contenuti dei volumi siano sostituiti dai volumi dal backup.</span><span class="sxs-lookup"><span data-stu-id="1b51a-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span></span>

<span data-ttu-id="1b51a-156">![Video disponibile](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video disponibile**</span><span class="sxs-lookup"><span data-stu-id="1b51a-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="1b51a-157">Per guardare un video che illustra come è possibile utilizzare le funzionalità di copia e ripristino di StorSimple per ripristinare file eliminati, fare clic [qui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="1b51a-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b51a-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b51a-158">Next steps</span></span>
* <span data-ttu-id="1b51a-159">Informazioni su come [gestire i volumi StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="1b51a-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="1b51a-160">Informazioni su come [usare il servizio StorSimple Manager per gestire il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1b51a-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

