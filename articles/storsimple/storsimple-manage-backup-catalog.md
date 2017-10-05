---
title: Gestire il catalogo di backup di StorSimple | Microsoft Docs
description: Viene illustrato come utilizzare la pagina del catalogo di backup del servizio StorSimple Manager per elencare, selezionare ed eliminare dei set di backup per un volume.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 5ee9855e1428c7a2d871d9c215d302c5c3b7101a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="6d9eb-103">Per gestire il catalogo di backup, è possibile usare il servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-103">Use the StorSimple Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="6d9eb-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6d9eb-104">Overview</span></span>
<span data-ttu-id="6d9eb-105">La pagina **Catalogo di backup** del servizio StorSimple Manager visualizza tutti i set di backup creati quando si eseguono backup manuali o programmati.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="6d9eb-106">È possibile utilizzare questa pagina per elencare tutti i backup per un criterio di backup o un volume, selezionare o eliminare i backup o utilizzare un backup per ripristinare o clonare un volume.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="6d9eb-107">In questa esercitazione viene illustrato come elencare, selezionare ed eliminare un set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="6d9eb-108">Per scoprire come ripristinare il dispositivo dal backup, vedere [Ripristinare il dispositivo da un set di backup](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="6d9eb-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="6d9eb-109">Per scoprire come clonare un volume, vedere [Clonare un volume StorSimple](storsimple-clone-volume.md).</span><span class="sxs-lookup"><span data-stu-id="6d9eb-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![Catalogo di backup](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="6d9eb-111">La pagina **Catalogo di backup** fornisce una query per limitare la selezione del set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="6d9eb-112">È possibile filtrare i set di backup che vengono recuperati in base ai parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="6d9eb-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="6d9eb-113">**Dispositivo** : il dispositivo in cui è stato creato il set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="6d9eb-114">**Criterio di backup o Volume** - il criterio di backup o volume associato a questo set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="6d9eb-115">**Da e A** - intervallo di data e ora di creazione del set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="6d9eb-116">I set di backup filtrati vengono quindi catalogati in base ai seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="6d9eb-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="6d9eb-117">**Nome** : nome del criterio di backup o volume associato al set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="6d9eb-118">**Dimensioni** : dimensione effettiva del set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="6d9eb-119">**Creato il** : data e ora di creazione dei backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="6d9eb-120">**Tipo** : i set di backup possono essere snapshot in locale o del cloud.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="6d9eb-121">Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente sul dispositivo, mentre uno snapshot del cloud si riferisce al backup dei dati di volume che risiedono nel cloud.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="6d9eb-122">Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="6d9eb-123">**Avviato da** : i backup possono essere avviati automaticamente da una pianificazione o manualmente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="6d9eb-124">Per pianificare i backup, è possibile usare un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="6d9eb-125">In alternativa, è possibile usare l'opzione **Esegui backup** per eseguire un backup manuale.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="6d9eb-126">Elencare i set di backup per un volume</span><span class="sxs-lookup"><span data-stu-id="6d9eb-126">List backup sets for a volume</span></span>
<span data-ttu-id="6d9eb-127">Completare la procedura seguente per elencare tutti i backup per un volume.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-127">Complete the following steps to list all the backups for a volume.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="6d9eb-128">Per elencare i set di backup</span><span class="sxs-lookup"><span data-stu-id="6d9eb-128">To list backup sets</span></span>
1. <span data-ttu-id="6d9eb-129">Nella pagina del servizio StorSimple Manager, fare clic sulla scheda **Catalogo di backup** .</span><span class="sxs-lookup"><span data-stu-id="6d9eb-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="6d9eb-130">Filtrare le selezioni come segue:</span><span class="sxs-lookup"><span data-stu-id="6d9eb-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="6d9eb-131">Selezionare un dispositivo appropriato.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-131">Select the appropriate device.</span></span>
   2. <span data-ttu-id="6d9eb-132">Nell'elenco a discesa scegliere un volume per visualizzare i backup corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-132">In the drop-down list, choose a volume to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="6d9eb-133">Specificare l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-133">Specify the time range.</span></span>
   4. <span data-ttu-id="6d9eb-134">Fare clic sull'icona del segno di spunta </span><span class="sxs-lookup"><span data-stu-id="6d9eb-134">Click the check icon</span></span> ![Icona del segno di spunta](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="6d9eb-136">per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-136">to execute this query.</span></span>
      
      <span data-ttu-id="6d9eb-137">I backup associati al volume selezionato dovrebbero essere visualizzati nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-137">The backups associated with the selected volume should appear in the list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="6d9eb-138">Selezionare un set di backup</span><span class="sxs-lookup"><span data-stu-id="6d9eb-138">Select a backup set</span></span>
<span data-ttu-id="6d9eb-139">Completare i passaggi seguenti per selezionare un set di backup per un volume o i criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="6d9eb-140">Per selezionare un set di backup</span><span class="sxs-lookup"><span data-stu-id="6d9eb-140">To select a backup set</span></span>
1. <span data-ttu-id="6d9eb-141">Nella pagina del servizio StorSimple Manager, fare clic sulla scheda **Catalogo di backup** .</span><span class="sxs-lookup"><span data-stu-id="6d9eb-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="6d9eb-142">Filtrare le selezioni come segue:</span><span class="sxs-lookup"><span data-stu-id="6d9eb-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="6d9eb-143">Selezionare un dispositivo appropriato.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-143">Select the appropriate device.</span></span>
   2. <span data-ttu-id="6d9eb-144">Nell'elenco a discesa, scegliere il volume o il criterio di backup per il backup che si desidera selezionare.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="6d9eb-145">Specificare l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-145">Specify the time range.</span></span>
   4. <span data-ttu-id="6d9eb-146">Fare clic sull'icona del segno di spunta </span><span class="sxs-lookup"><span data-stu-id="6d9eb-146">Click the check icon</span></span> ![Icona del segno di spunta](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="6d9eb-148">per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-148">to execute this query.</span></span>
      
      <span data-ttu-id="6d9eb-149">I backup associati al volume selezionato o al criterio di backup dovrebbero essere visualizzati nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="6d9eb-150">Selezionare ed espandere un set di backup</span><span class="sxs-lookup"><span data-stu-id="6d9eb-150">Select and expand a backup set.</span></span> <span data-ttu-id="6d9eb-151">Le opzioni **Ripristina** ed **Elimina** sono visualizzate nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="6d9eb-152">È possibile eseguire queste azioni sul set di backup selezionato.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-152">You can perform either of these actions on the backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="6d9eb-153">Eliminare un set di backup</span><span class="sxs-lookup"><span data-stu-id="6d9eb-153">Delete a backup set</span></span>
<span data-ttu-id="6d9eb-154">Eliminare un backup quando non si desidera più conservare i dati associati.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-154">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="6d9eb-155">Eseguire la procedura seguente per eliminare un set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-155">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="6d9eb-156">Per eliminare un set di backup</span><span class="sxs-lookup"><span data-stu-id="6d9eb-156">To delete a backup set</span></span>
1. <span data-ttu-id="6d9eb-157">Nella pagina del servizio StorSimple Manager fare clic sulla scheda **Catalogo di backup**.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="6d9eb-158">Filtrare le selezioni come segue:</span><span class="sxs-lookup"><span data-stu-id="6d9eb-158">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="6d9eb-159">Selezionare un dispositivo appropriato.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-159">Select the appropriate device.</span></span>
   2. <span data-ttu-id="6d9eb-160">Nell'elenco a discesa, scegliere il volume o il criterio di backup per il backup che si desidera selezionare.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="6d9eb-161">Specificare l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-161">Specify the time range.</span></span>
   4. <span data-ttu-id="6d9eb-162">Fare clic sull'icona del segno di spunta </span><span class="sxs-lookup"><span data-stu-id="6d9eb-162">Click the check icon</span></span> ![Icona del segno di spunta](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="6d9eb-164">per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-164">to execute this query.</span></span>
      
      <span data-ttu-id="6d9eb-165">I backup associati al volume selezionato o al criterio di backup dovrebbero essere visualizzati nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="6d9eb-166">Selezionare ed espandere un set di backup</span><span class="sxs-lookup"><span data-stu-id="6d9eb-166">Select and expand a backup set.</span></span> <span data-ttu-id="6d9eb-167">Le opzioni **Ripristina** ed **Elimina** sono visualizzate nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="6d9eb-168">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-168">Click **Delete**.</span></span>
4. <span data-ttu-id="6d9eb-169">Verrà visualizzata una notifica dell'operazione di eliminazione in corso e del corretto completamento.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-169">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="6d9eb-170">Al termine dell'eliminazione, aggiornare la query nella pagina.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-170">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="6d9eb-171">Il set di backup eliminato non verrà più visualizzato nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="6d9eb-171">The deleted backup set will no longer appear in the list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d9eb-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6d9eb-172">Next steps</span></span>
* <span data-ttu-id="6d9eb-173">Informazioni su come [usare la pagina Catalogo di backup per ripristinare il dispositivo da un set di backup](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="6d9eb-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="6d9eb-174">Informazioni su come [utilizzare il servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6d9eb-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

