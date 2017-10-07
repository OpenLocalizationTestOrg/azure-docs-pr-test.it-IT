---
title: processi di backup di Snapshot Manager aaaStorSimple | Documenti Microsoft
description: Viene descritto come toouse hello tooview snap-in MMC di StorSimple Snapshot Manager e gestire i processi di backup pianificati, attualmente in esecuzione e completati.
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
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="b82c1-103">Utilizzare Gestione Snapshot StorSimple tooview e gestire i processi di backup</span><span class="sxs-lookup"><span data-stu-id="b82c1-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="b82c1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b82c1-104">Overview</span></span>
<span data-ttu-id="b82c1-105">Hello **processi** nodo hello **ambito** riquadro Mostra hello **pianificato**, **ultime 24 ore**, e **esecuzione**attività è stata avviata in modo interattivo o da criteri di configurazione di backup.</span><span class="sxs-lookup"><span data-stu-id="b82c1-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="b82c1-106">In questa esercitazione viene illustrato come utilizzare hello **processi** informazioni toodisplay nodo sui processi di backup attualmente in esecuzione, pianificati e recenti.</span><span class="sxs-lookup"><span data-stu-id="b82c1-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="b82c1-107">(elenco hello dei processi e delle informazioni corrispondenti vengono visualizzati nel hello **risultati** riquadro.) Inoltre, è possibile fare clic con il pulsante destro del mouse su un processo elencato e visualizzare un menu di scelta rapida in cui sono elencate le azioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="b82c1-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="b82c1-108">Visualizzazione dei processi pianificati</span><span class="sxs-lookup"><span data-stu-id="b82c1-108">View scheduled jobs</span></span>
<span data-ttu-id="b82c1-109">Hello utilizzare seguendo procedure tooview processi di backup pianificati.</span><span class="sxs-lookup"><span data-stu-id="b82c1-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="b82c1-110">processi pianificati tooview</span><span class="sxs-lookup"><span data-stu-id="b82c1-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="b82c1-111">Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b82c1-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="b82c1-112">In hello **ambito** riquadro espandere hello **processi** nodo e fare clic su **pianificato**.</span><span class="sxs-lookup"><span data-stu-id="b82c1-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="b82c1-113">Hello seguenti informazioni nella hello **risultati** riquadro:</span><span class="sxs-lookup"><span data-stu-id="b82c1-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="b82c1-114">**Nome** : hello nome dello snapshot pianificato hello</span><span class="sxs-lookup"><span data-stu-id="b82c1-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="b82c1-115">**Prossima esecuzione** : hello data e ora del successivo snapshot pianificato hello</span><span class="sxs-lookup"><span data-stu-id="b82c1-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="b82c1-116">**Ultima esecuzione** : hello data e l'ora dello snapshot pianificato più recente di hello</span><span class="sxs-lookup"><span data-stu-id="b82c1-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="b82c1-117">Per gli snapshot soli monouso, hello **prossima esecuzione** e **ultima esecuzione** sarà hello stesso.</span><span class="sxs-lookup"><span data-stu-id="b82c1-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![Processi di backup pianificati](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="b82c1-119">tooperform azioni aggiuntive su un processo specifico, fare doppio clic su nome del processo hello in hello **risultati** riquadro e selezionare una delle opzioni di menu hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="b82c1-120">Visualizzazione dei processi recenti</span><span class="sxs-lookup"><span data-stu-id="b82c1-120">View recent jobs</span></span>
<span data-ttu-id="b82c1-121">Utilizzare hello dopo il backup di routine tooview e ripristinare i processi completati nelle hello ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="b82c1-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="b82c1-122">processi recenti tooview</span><span class="sxs-lookup"><span data-stu-id="b82c1-122">tooview recent jobs</span></span>
1. <span data-ttu-id="b82c1-123">Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b82c1-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="b82c1-124">In hello **ambito** riquadro espandere hello **processi** nodo e fare clic su **ultime 24 ore**.</span><span class="sxs-lookup"><span data-stu-id="b82c1-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="b82c1-125">Hello **risultati** riquadro vengono visualizzati i processi di backup per hello ultime 24 ore (tooa massimo di 64 processi).</span><span class="sxs-lookup"><span data-stu-id="b82c1-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="b82c1-126">Hello seguenti informazioni nella hello **risultati** riquadro, a seconda di hello **vista** opzioni:</span><span class="sxs-lookup"><span data-stu-id="b82c1-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="b82c1-127">**Nome** : hello nome dello snapshot pianificato hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="b82c1-128">**Avvio** : hello data e l'ora di inizio snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="b82c1-129">**Arrestato** : hello data e l'ora dello snapshot hello completata o è stato terminato.</span><span class="sxs-lookup"><span data-stu-id="b82c1-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="b82c1-130">**Trascorso** : hello periodo di tempo tra hello **Started** e **arrestato** volte.</span><span class="sxs-lookup"><span data-stu-id="b82c1-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="b82c1-131">**Stato** : hello lo stato di processo hello completato di recente.</span><span class="sxs-lookup"><span data-stu-id="b82c1-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="b82c1-132">**Esito positivo** indica che il backup hello è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b82c1-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="b82c1-133">**Non è stato possibile** indica che il processo di hello non è stato eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="b82c1-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="b82c1-134">**Informazioni** : hello motivo dell'errore hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="b82c1-135">**Byte elaborati (MB)** : quantità di hello dei dati dal gruppo di volumi hello (in MB) è stato elaborato.</span><span class="sxs-lookup"><span data-stu-id="b82c1-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Processi eseguiti in hello ultime 24 ore](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="b82c1-137">tooperform azioni aggiuntive su un processo specifico, fare doppio clic su nome del processo hello in hello **risultati** riquadro e selezionare una delle opzioni di menu hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![Eliminare un processo](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="b82c1-139">Visualizzazione dei processi attualmente in esecuzione</span><span class="sxs-lookup"><span data-stu-id="b82c1-139">View currently running jobs</span></span>
<span data-ttu-id="b82c1-140">Utilizzare hello seguenti processi tooview procedure attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b82c1-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="b82c1-141">tooview processi attualmente in esecuzione</span><span class="sxs-lookup"><span data-stu-id="b82c1-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="b82c1-142">Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b82c1-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="b82c1-143">In hello **ambito** riquadro espandere hello **processi** nodo e fare clic su **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="b82c1-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="b82c1-144">A seconda di hello **vista** opzioni specificate, le seguenti informazioni hello viene visualizzato in hello **risultati** riquadro:</span><span class="sxs-lookup"><span data-stu-id="b82c1-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="b82c1-145">**Nome** : hello nome dello snapshot pianificato hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="b82c1-146">**Avvio** : hello data e l'ora di inizio snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="b82c1-147">**Checkpoint** : azione corrente backup hello hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="b82c1-148">**Stato** : hello percentuale di completamento.</span><span class="sxs-lookup"><span data-stu-id="b82c1-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="b82c1-149">**Trascorso** : quantità di hello di tempo trascorso dall'inizio backup hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="b82c1-150">**Velocità effettiva Media (MB)** : percentuale totale di byte di dati elaborati toothat del tempo totale impiegato per l'elaborazione (MB).</span><span class="sxs-lookup"><span data-stu-id="b82c1-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="b82c1-151">**Byte elaborati (MB)** : totale dei byte di dati elaborati (in MB).</span><span class="sxs-lookup"><span data-stu-id="b82c1-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="b82c1-152">**Byte scritti (MB)** : totale dei byte scritti (in MB).</span><span class="sxs-lookup"><span data-stu-id="b82c1-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="b82c1-153">Include dati hello nonché i metadati di hello e pertanto è in genere maggiore di hello byte elaborati.</span><span class="sxs-lookup"><span data-stu-id="b82c1-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![Processi attualmente in esecuzione](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="b82c1-155">tooperform azioni aggiuntive su un processo specifico, fare doppio clic su nome del processo hello in hello **risultati** riquadro e selezionare una delle opzioni di menu hello.</span><span class="sxs-lookup"><span data-stu-id="b82c1-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b82c1-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b82c1-156">Next steps</span></span>
* <span data-ttu-id="b82c1-157">Informazioni su come troppo[usare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="b82c1-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="b82c1-158">Informazioni su come troppo[utilizzare catalogo di backup di gestione Snapshot StorSimple toomanage hello](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="b82c1-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

