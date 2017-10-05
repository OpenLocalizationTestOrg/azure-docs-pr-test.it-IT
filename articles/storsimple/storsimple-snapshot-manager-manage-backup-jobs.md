---
title: Operazioni di backup di StorSimple Snapshot Manager | Microsoft Docs
description: Viene descritto come usare lo snap-in MMC StorSimple Snapshot Manager per visualizzare e gestire i processi di backup pianificati, attualmente in esecuzione e completati.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="46f77-103">Usare StorSimple Snapshot Manager per visualizzare e gestire i processi di backup</span><span class="sxs-lookup"><span data-stu-id="46f77-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="46f77-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="46f77-104">Overview</span></span>
<span data-ttu-id="46f77-105">Nel nodo **Processi** del riquadro **Ambito** vengono mostrate le attività di backup **pianificate**, delle **ultime 24 ore** e **in esecuzione** avviate in modo interattivo o da un criterio configurato.</span><span class="sxs-lookup"><span data-stu-id="46f77-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="46f77-106">In questa esercitazione viene illustrato come usare il nodo **Processi** per visualizzare le informazioni sui processi di backup pianificati, recenti e attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="46f77-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="46f77-107">L'elenco dei processi e le informazioni corrispondenti vengono visualizzati nel riquadro **Risultati**. Inoltre, è possibile fare clic con il pulsante destro del mouse su un processo elencato e visualizzare un menu di scelta rapida in cui sono elencate le azioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="46f77-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="46f77-108">Visualizzazione dei processi pianificati</span><span class="sxs-lookup"><span data-stu-id="46f77-108">View scheduled jobs</span></span>
<span data-ttu-id="46f77-109">Utilizzare la procedura seguente per visualizzare i processi di backup pianificati.</span><span class="sxs-lookup"><span data-stu-id="46f77-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="46f77-110">Per visualizzare i processi pianificati</span><span class="sxs-lookup"><span data-stu-id="46f77-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="46f77-111">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="46f77-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="46f77-112">Nel riquadro **Ambito** espandere il nodo **Processi**, quindi fare clic su **Pianificati**.</span><span class="sxs-lookup"><span data-stu-id="46f77-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="46f77-113">Nel riquadro **Risultati** vengono visualizzate le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="46f77-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="46f77-114">**Nome** : il nome dello snapshot pianificato</span><span class="sxs-lookup"><span data-stu-id="46f77-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="46f77-115">**Prossima esecuzione** : la data e l’ora del successivo snapshot pianificato.</span><span class="sxs-lookup"><span data-stu-id="46f77-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="46f77-116">**Ultima esecuzione** : la data e l'ora dello snapshot pianificato più recente.</span><span class="sxs-lookup"><span data-stu-id="46f77-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="46f77-117">Solo per gli snapshot monouso, il valore di **Prossima esecuzione** e **Ultima esecuzione** sarà lo stesso.</span><span class="sxs-lookup"><span data-stu-id="46f77-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span>
     
     ![Processi di backup pianificati](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="46f77-119">Per eseguire azioni aggiuntive su un processo specifico, fare clic con il pulsante destro del mouse sul nome del processo nel riquadro **Risultati** e selezionare un’opzione del menu.</span><span class="sxs-lookup"><span data-stu-id="46f77-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="46f77-120">Visualizzazione dei processi recenti</span><span class="sxs-lookup"><span data-stu-id="46f77-120">View recent jobs</span></span>
<span data-ttu-id="46f77-121">Utilizzare la procedura seguente per visualizzare i processi di backup e ripristino completati nelle ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="46f77-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="46f77-122">Per visualizzare i processi recenti</span><span class="sxs-lookup"><span data-stu-id="46f77-122">To view recent jobs</span></span>
1. <span data-ttu-id="46f77-123">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="46f77-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="46f77-124">Nel riquadro **Ambito** espandere il nodo **Processi**, quindi fare clic su **Ultime 24 ore**.</span><span class="sxs-lookup"><span data-stu-id="46f77-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="46f77-125">Nel riquadro **Risultati** vengono mostrati i processi di backup per le ultime 24 ore (per un massimo di 64 processi).</span><span class="sxs-lookup"><span data-stu-id="46f77-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="46f77-126">Nel riquadro **Risultati** vengono visualizzate le informazioni seguenti, a seconda delle opzioni di **Visualizza** specificate:</span><span class="sxs-lookup"><span data-stu-id="46f77-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="46f77-127">**Nome** : il nome dello snapshot pianificato.</span><span class="sxs-lookup"><span data-stu-id="46f77-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="46f77-128">**Avviato** : la data e l’ora di avvio dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="46f77-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="46f77-129">**Arrestato** : la data e l'ora in cui lo snapshot è stato completato o terminato.</span><span class="sxs-lookup"><span data-stu-id="46f77-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="46f77-130">**Trascorso**: la quantità di tempo che intercorre tra l'ora di **Avviato** e **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="46f77-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="46f77-131">**Stato** : lo stato del processo completato di recente.</span><span class="sxs-lookup"><span data-stu-id="46f77-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="46f77-132">**Esito positivo** indica che il backup è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="46f77-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="46f77-133">**Operazione non riuscita** indica che il processo non è stato eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="46f77-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="46f77-134">**Informazioni** : il motivo dell'errore.</span><span class="sxs-lookup"><span data-stu-id="46f77-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="46f77-135">**Byte elaborati (MB)** : la quantità di dati del gruppo di volumi che è stata elaborata (in MB).</span><span class="sxs-lookup"><span data-stu-id="46f77-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![Processi eseguiti nelle ultime 24 ore](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="46f77-137">Per eseguire azioni aggiuntive su un processo specifico, fare clic con il pulsante destro del mouse sul nome del processo nel riquadro **Risultati** e selezionare un’opzione del menu.</span><span class="sxs-lookup"><span data-stu-id="46f77-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![Eliminare un processo](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="46f77-139">Visualizzazione dei processi attualmente in esecuzione</span><span class="sxs-lookup"><span data-stu-id="46f77-139">View currently running jobs</span></span>
<span data-ttu-id="46f77-140">Utilizzare la procedura seguente per visualizzare i processi attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="46f77-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="46f77-141">Per visualizzare i processi attualmente in esecuzione</span><span class="sxs-lookup"><span data-stu-id="46f77-141">To view currently running jobs</span></span>
1. <span data-ttu-id="46f77-142">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="46f77-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="46f77-143">Nel riquadro **Ambito** espandere il nodo **Processi**, quindi fare clic su **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="46f77-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="46f77-144">Nel riquadro **Risultati** vengono visualizzate le informazioni seguenti, a seconda delle opzioni di **Visualizza** specificate:</span><span class="sxs-lookup"><span data-stu-id="46f77-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="46f77-145">**Nome** : il nome dello snapshot pianificato.</span><span class="sxs-lookup"><span data-stu-id="46f77-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="46f77-146">**Avviato** : la data e l’ora di avvio dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="46f77-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="46f77-147">**Checkpoint** : l'azione corrente del backup.</span><span class="sxs-lookup"><span data-stu-id="46f77-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="46f77-148">**Stato** : la percentuale di completamento.</span><span class="sxs-lookup"><span data-stu-id="46f77-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="46f77-149">**Trascorso** : la quantità di tempo trascorso dall'avvio del backup.</span><span class="sxs-lookup"><span data-stu-id="46f77-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="46f77-150">**Velocità effettiva media (MB)** : rapporto tra i byte totali di dati elaborati e il tempo totale usato per l'elaborazione (MB).</span><span class="sxs-lookup"><span data-stu-id="46f77-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="46f77-151">**Byte elaborati (MB)** : totale dei byte di dati elaborati (in MB).</span><span class="sxs-lookup"><span data-stu-id="46f77-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="46f77-152">**Byte scritti (MB)** : totale dei byte scritti (in MB).</span><span class="sxs-lookup"><span data-stu-id="46f77-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="46f77-153">Questo valore include i dati e i metadati e quindi in genere è maggiore rispetto al valore dei byte elaborati.</span><span class="sxs-lookup"><span data-stu-id="46f77-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![Processi attualmente in esecuzione](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="46f77-155">Per eseguire azioni aggiuntive su un processo specifico, fare clic con il pulsante destro del mouse sul nome del processo nel riquadro **Risultati** e selezionare un’opzione del menu.</span><span class="sxs-lookup"><span data-stu-id="46f77-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46f77-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="46f77-156">Next steps</span></span>
* <span data-ttu-id="46f77-157">Informazioni su come [usare StorSimple Snapshot Manager per amministrare la soluzione di StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="46f77-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="46f77-158">Informazioni su come [usare StorSimple Snapshot Manager per gestire il catalogo di backup](storsimple-snapshot-manager-manage-backup-catalog.md)</span><span class="sxs-lookup"><span data-stu-id="46f77-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

