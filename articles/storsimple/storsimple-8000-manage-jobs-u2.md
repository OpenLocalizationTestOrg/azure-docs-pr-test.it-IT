---
title: Visualizzare e gestire i processi per il dispositivo StorSimple serie 8000 | Microsoft Docs
description: Descrive il pannello Processi del servizio Gestione dispositivi StorSimple e come usarlo per tenere traccia dei processi di backup recenti, correnti e pianificati.
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
ms.openlocfilehash: bf8038b7171053b75eeb9aed88bff4246e65a8a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="c2cc0-103">Usare il servizio Gestione dispositivi StorSimple per visualizzare e gestire i processi (Aggiornamento 3 e successivi)</span><span class="sxs-lookup"><span data-stu-id="c2cc0-103">Use the StorSimple Device Manager service to view and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="c2cc0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c2cc0-104">Overview</span></span>
<span data-ttu-id="c2cc0-105">Il pannello **Processi** rappresenta un portale centralizzato per la visualizzazione e la gestione dei processi avviati sui dispositivi connessi al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="c2cc0-106">È possibile visualizzare i processi pianificati, in esecuzione, completati, annullati e non riusciti per più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="c2cc0-107">I risultati vengono presentati in un formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-107">Results are presented in a tabular format.</span></span>

![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="c2cc0-109">È possibile trovare rapidamente i processi desiderati filtrando i campi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="c2cc0-110">**Stato**: i processi possono essere in corso, completati, annullati, non riusciti, annullati o completati con errori.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="c2cc0-111">**Intervallo di tempo**: i processi possono essere filtrati in base all'intervallo di data e ora.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-111">**Time range** – Jobs can be filtered based on the date and time range.</span></span> <span data-ttu-id="c2cc0-112">Può essere Ultima ora, Ultime 24 ore, Ultimi 7 giorni, Ultimi 30 giorni, Ultimo anno e Data personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-112">The ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="c2cc0-113">**Tipo**: il tipo di processo può essere backup pianificato, backup manuale, backup di ripristino, volume clone, contenitori dei volumi con failover, volume aggiunto in locale, volume modificato, installazione di aggiornamenti, raccolta di log di supporto e creazione di appliance cloud.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-113">**Type** – The job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="c2cc0-114">**Dispositivi** : i processi vengono avviati in un determinato dispositivo connesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-114">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  
<span data-ttu-id="c2cc0-115">I processi filtrati vengono quindi elaborati in base ai seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-115">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
* <span data-ttu-id="c2cc0-116">**Nome**: backup pianificato, backup manuale, backup di ripristino, volume clone, contenitori dei volumi con failover, volume aggiunto in locale, volume modificato, installazione di aggiornamenti, raccolta di log di supporto e creazione di appliance cloud.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="c2cc0-117">**Stato** : in esecuzione, completati, annullati, non riusciti, in fase di annullamento o completati con errori.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="c2cc0-118">**Entità** : i processi possono essere associati a un volume, un criterio di backup o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-118">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="c2cc0-119">Ad esempio, un processo di clonazione è associato a un volume, mentre un processo di backup pianificato è associato a un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="c2cc0-120">Viene creato un processo di dispositivo a causa di un ripristino di emergenza (DR) o di un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="c2cc0-121">**Dispositivo** : il nome del dispositivo su cui è stato avviato il processo.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-121">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="c2cc0-122">**Avviato alle** : l'ora di inizio del processo.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-122">**Started on** – The time when the job was started.</span></span>
* <span data-ttu-id="c2cc0-123">**Durata**: il tempo necessario per completare il processo.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-123">**Duration** – The time required to complete the job.</span></span>

<span data-ttu-id="c2cc0-124">L'elenco dei processi viene aggiornato ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="c2cc0-125">In questa pagina è possibile eseguire le seguenti azioni relative ai processi:</span><span class="sxs-lookup"><span data-stu-id="c2cc0-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="c2cc0-126">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="c2cc0-126">View job details</span></span>
* <span data-ttu-id="c2cc0-127">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="c2cc0-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="c2cc0-128">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="c2cc0-128">View job details</span></span>
<span data-ttu-id="c2cc0-129">Eseguire la procedura seguente per visualizzare i dettagli di qualsiasi processo.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="c2cc0-130">Per visualizzare i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="c2cc0-130">To view job details</span></span>
1. <span data-ttu-id="c2cc0-131">Passare al servizio Gestione dispositivi StorSimple, quindi fare clic su **Processi**.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-131">Go to your StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="c2cc0-132">Nel pannello **Processi**, visualizzare i processi desiderati eseguendo una query con i filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-132">In the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="c2cc0-133">È possibile cercare processi completati, in esecuzione o annullati.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="c2cc0-135">Selezionare e fare clic su un processo.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-135">Select and click a job.</span></span>

    ![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="c2cc0-137">Nella finestra di dialogo dei dettagli del processo è possibile visualizzare lo stato, i dettagli, le statistiche temporali e le statistiche sui dati.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-137">In the job details blade, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Dettagli del processo](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="c2cc0-139">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="c2cc0-139">Cancel a job</span></span>
<span data-ttu-id="c2cc0-140">Eseguire la procedura seguente per annullare un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-140">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="c2cc0-141">Alcuni processi, ad esempio la modifica di un volume per cambiare il tipo di volume o espandere un volume, non possono essere annullati.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-141">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="to-cancel-a-job"></a><span data-ttu-id="c2cc0-142">Per annullare un processo</span><span class="sxs-lookup"><span data-stu-id="c2cc0-142">To cancel a job</span></span>
1. <span data-ttu-id="c2cc0-143">Nella pagina **Processi** , visualizzare i processi in esecuzione che si desidera annullare eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-143">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span> <span data-ttu-id="c2cc0-144">Selezionare il processo.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-144">Select the job.</span></span>

2. <span data-ttu-id="c2cc0-145">Fare clic sul processo selezionato per richiamare il menu di scelta rapida e fare clic su **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-145">Right-click on the selected job to invoke the context menu and click **Cancel**.</span></span>

    ![Dettagli del processo](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="c2cc0-147">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="c2cc0-148">Questo processo ora viene annullato.</span><span class="sxs-lookup"><span data-stu-id="c2cc0-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2cc0-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2cc0-149">Next steps</span></span>
* <span data-ttu-id="c2cc0-150">Informazioni su come [gestire i criteri di backup di StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-150">Learn how to [manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="c2cc0-151">Informazioni su come [usare il servizio Gestione dispositivi StorSimple per gestire il dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c2cc0-151">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

