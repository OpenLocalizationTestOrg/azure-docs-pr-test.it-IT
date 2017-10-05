---
title: Gestire il catalogo di backup di StorSimple | Microsoft Docs
description: Illustra come usare la pagina del catalogo di backup del servizio Gestione dispositivi StorSimple per elencare, selezionare ed eliminare i set di backup.
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
ms.openlocfilehash: ac2577c6cd350d6d437d55e61ec73d954cb24893
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="44caa-103">Usare il servizio Gestione dispositivi StorSimple per gestire il catalogo di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-103">Use the StorSimple Device Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="44caa-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="44caa-104">Overview</span></span>
<span data-ttu-id="44caa-105">Il pannello **Catalogo di backup** del servizio Gestione dispositivi StorSimple visualizza tutti i set di backup creati quando si eseguono backup manuali o programmati.</span><span class="sxs-lookup"><span data-stu-id="44caa-105">The StorSimple Device Manager service **Backup Catalog** blade displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="44caa-106">È possibile utilizzare questa pagina per elencare tutti i backup per un criterio di backup o un volume, selezionare o eliminare i backup o utilizzare un backup per ripristinare o clonare un volume.</span><span class="sxs-lookup"><span data-stu-id="44caa-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="44caa-107">In questa esercitazione viene illustrato come elencare, selezionare ed eliminare un set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="44caa-108">Per scoprire come ripristinare il dispositivo dal backup, vedere [Ripristinare il dispositivo da un set di backup](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="44caa-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="44caa-109">Per scoprire come clonare un volume, vedere [Clonare un volume StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="44caa-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="44caa-111">Il pannello **Catalogo di backup** fornisce una query per limitare la selezione del set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-111">The **Backup Catalog** blade provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="44caa-112">È possibile filtrare i set di backup che vengono recuperati in base ai parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="44caa-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="44caa-113">**Dispositivo** : il dispositivo in cui è stato creato il set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="44caa-114">**Criterio di backup o Volume**: il criterio di backup o volume associato a questo set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-114">**Backup policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="44caa-115">**Da e A** - intervallo di data e ora di creazione del set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="44caa-116">I set di backup filtrati vengono quindi catalogati in base ai seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="44caa-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="44caa-117">**Nome** : nome del criterio di backup o volume associato al set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="44caa-118">**Dimensioni** : dimensione effettiva del set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="44caa-119">**Creato il** : data e ora di creazione dei backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="44caa-120">**Tipo** : i set di backup possono essere snapshot in locale o del cloud.</span><span class="sxs-lookup"><span data-stu-id="44caa-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="44caa-121">Uno snapshot locale è un backup di tutti i dati di volume archiviati localmente sul dispositivo, mentre uno snapshot del cloud si riferisce al backup dei dati di volume che risiedono nel cloud.</span><span class="sxs-lookup"><span data-stu-id="44caa-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="44caa-122">Gli snapshot in locale forniscono un accesso più rapido, mentre gli snapshot del cloud vengono scelti per la resilienza dei dati.</span><span class="sxs-lookup"><span data-stu-id="44caa-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="44caa-123">**Avviato da** : i backup possono essere avviati automaticamente da una pianificazione o manualmente dall'utente.</span><span class="sxs-lookup"><span data-stu-id="44caa-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="44caa-124">Per pianificare i backup, è possibile usare un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="44caa-125">In alternativa, è possibile usare l'opzione **Esegui backup** per eseguire un backup manuale.</span><span class="sxs-lookup"><span data-stu-id="44caa-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="44caa-126">Elencare i set di backup di un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="44caa-127">Completare la procedura seguente per elencare tutti i backup di un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-127">Complete the following steps to list all the backups for a backup policy.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="44caa-128">Per elencare i set di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-128">To list backup sets</span></span>
1. <span data-ttu-id="44caa-129">Passare al servizio Gestione dispositivi StorSimple e fare clic su **Catalogo di backup**.</span><span class="sxs-lookup"><span data-stu-id="44caa-129">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="44caa-130">Filtrare le selezioni come segue:</span><span class="sxs-lookup"><span data-stu-id="44caa-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="44caa-131">Specificare l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="44caa-131">Specify the time range.</span></span>
   2. <span data-ttu-id="44caa-132">Selezionare un dispositivo appropriato.</span><span class="sxs-lookup"><span data-stu-id="44caa-132">Select the appropriate device.</span></span>
   3. <span data-ttu-id="44caa-133">Filtrare in base ai **Criteri di backup** per visualizzare i backup corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="44caa-133">Filter by **Backup policy** to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="44caa-134">Nell'elenco a discesa dei criteri di backup, scegliere **Tutti** per visualizzare tutti i backup nel dispositivo selezionato.</span><span class="sxs-lookup"><span data-stu-id="44caa-134">From the backup policy dropdown list, choose **All** to view all the backups on the selected device.</span></span>
   4. <span data-ttu-id="44caa-135">Fare clic su **Applica** per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="44caa-135">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="44caa-136">I backup associati al criterio di backup selezionato dovrebbero vengono visualizzati nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-136">The backups associated with the selected backup policy should appear in the list of backup sets.</span></span>

      ![Passare a un catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="44caa-138">Selezionare un set di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-138">Select a backup set</span></span>
<span data-ttu-id="44caa-139">Completare i passaggi seguenti per selezionare un set di backup per un volume o i criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="44caa-140">Per selezionare un set di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-140">To select a backup set</span></span>
1. <span data-ttu-id="44caa-141">Passare al servizio Gestione dispositivi StorSimple e fare clic su **Catalogo di backup**.</span><span class="sxs-lookup"><span data-stu-id="44caa-141">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="44caa-142">Filtrare le selezioni come segue:</span><span class="sxs-lookup"><span data-stu-id="44caa-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="44caa-143">Specificare l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="44caa-143">Specify the time range.</span></span> 
   2. <span data-ttu-id="44caa-144">Selezionare un dispositivo appropriato.</span><span class="sxs-lookup"><span data-stu-id="44caa-144">Select the appropriate device.</span></span> 
   3. <span data-ttu-id="44caa-145">Filtrare in base al volume o al criterio di backup del backup che si vuole selezionare.</span><span class="sxs-lookup"><span data-stu-id="44caa-145">Filter by volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="44caa-146">Fare clic su **Applica** per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="44caa-146">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="44caa-147">I backup associati al volume selezionato o al criterio di backup dovrebbero essere visualizzati nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-147">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>

      ![Passare a un catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="44caa-149">Selezionare ed espandere un set di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-149">Select and expand a backup set.</span></span> <span data-ttu-id="44caa-150">È ora possibile visualizzare i set di backup suddivisi in base ai volumi che contengono.</span><span class="sxs-lookup"><span data-stu-id="44caa-150">You can now see the backup sets broken down by the volumes that it contains.</span></span> <span data-ttu-id="44caa-151">Le opzioni **Ripristina** ed **Elimina** sono disponibili nel menu di scelta rapida del set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-151">The **Restore** and **Delete** options are available via the context menu (right-click) for the backup set.</span></span> <span data-ttu-id="44caa-152">È possibile eseguire queste azioni sul set di backup selezionato.</span><span class="sxs-lookup"><span data-stu-id="44caa-152">You can perform either of these actions on the backup set that you selected.</span></span>

    ![Passare a un catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="44caa-154">Eliminare un set di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-154">Delete a backup set</span></span>
<span data-ttu-id="44caa-155">Eliminare un backup quando non si desidera più conservare i dati associati.</span><span class="sxs-lookup"><span data-stu-id="44caa-155">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="44caa-156">Eseguire la procedura seguente per eliminare un set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-156">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="44caa-157">Per eliminare un set di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-157">To delete a backup set</span></span>
 <span data-ttu-id="44caa-158">Passare al servizio Gestione dispositivi StorSimple e fare clic su **Catalogo di backup**.</span><span class="sxs-lookup"><span data-stu-id="44caa-158">Go to your StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="44caa-159">Filtrare le selezioni come segue:</span><span class="sxs-lookup"><span data-stu-id="44caa-159">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="44caa-160">Specificare l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="44caa-160">Specify the time range.</span></span> 
   2. <span data-ttu-id="44caa-161">Selezionare un dispositivo appropriato.</span><span class="sxs-lookup"><span data-stu-id="44caa-161">Select the appropriate device.</span></span> 
   3. <span data-ttu-id="44caa-162">Filtrare in base al volume o al criterio di backup del backup che si vuole selezionare.</span><span class="sxs-lookup"><span data-stu-id="44caa-162">Filter by volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="44caa-163">Fare clic su **Applica** per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="44caa-163">Click **Apply** to execute this query.</span></span>
      
      <span data-ttu-id="44caa-164">I backup associati al volume selezionato o al criterio di backup dovrebbero essere visualizzati nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-164">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>

      ![Passare a un catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="44caa-166">Selezionare ed espandere un set di backup</span><span class="sxs-lookup"><span data-stu-id="44caa-166">Select and expand a backup set.</span></span> <span data-ttu-id="44caa-167">È ora possibile visualizzare i set di backup suddivisi in base ai volumi che contengono.</span><span class="sxs-lookup"><span data-stu-id="44caa-167">You can now see the backup sets broken down by the volumes that it contains.</span></span> <span data-ttu-id="44caa-168">Le opzioni **Ripristina** ed **Elimina** sono disponibili nel menu di scelta rapida del set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-168">The **Restore** and **Delete** options are available via the context menu (right-click) for the backup set.</span></span> <span data-ttu-id="44caa-169">Fare clic con il pulsante destro del mouse sul set di backup selezionato e scegliere **Elimina** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="44caa-169">Right-click the selected backup set and from the context menu, select **Delete**.</span></span>

    ![Passare a un catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="44caa-171">Quando viene richiesta la conferma, esaminare le informazioni visualizzate e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="44caa-171">When prompted for confirmation, review the displayed information and click **Delete**.</span></span> <span data-ttu-id="44caa-172">Il backup selezionato verrà eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="44caa-172">The selected backup is deleted permanently.</span></span>

    ![Passare a un catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="44caa-174">Verrà visualizzata una notifica dell'operazione di eliminazione in corso e del corretto completamento.</span><span class="sxs-lookup"><span data-stu-id="44caa-174">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="44caa-175">Al termine dell'eliminazione, aggiornare la query nella pagina.</span><span class="sxs-lookup"><span data-stu-id="44caa-175">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="44caa-176">Il set di backup eliminato non verrà più visualizzato nell'elenco dei set di backup.</span><span class="sxs-lookup"><span data-stu-id="44caa-176">The deleted backup set will no longer appear in the list of backup sets.</span></span>

    ![Passare a un catalogo di backup](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="44caa-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="44caa-178">Next steps</span></span>
* <span data-ttu-id="44caa-179">Informazioni su come [usare la pagina Catalogo di backup per ripristinare il dispositivo da un set di backup](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="44caa-179">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="44caa-180">Informazioni su come [usare il servizio Gestione dispositivi StorSimple per gestire il dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="44caa-180">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

