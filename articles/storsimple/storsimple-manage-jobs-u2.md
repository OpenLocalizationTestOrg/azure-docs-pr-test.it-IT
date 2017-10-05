---
title: Consente di visualizzare e gestire i processi di StorSimple | Microsoft Docs
description: Descrive la pagina relativa ai processi del servizio StorSimple Manager e come utilizzarlo per tenere traccia dei processi di backup recenti, correnti e pianificati.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 6df1b27ce76de7a781ecc40af8430114d80b20d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="e2972-103">Utilizzare il servizio StorSimple Manager per visualizzare e gestire i processi di StorSimple (aggiornamento 2)</span><span class="sxs-lookup"><span data-stu-id="e2972-103">Use the StorSimple Manager service to view and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="e2972-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e2972-104">Overview</span></span>
<span data-ttu-id="e2972-105">La pagina **processi** fornisce un unico portale centralizzato per la visualizzazione e la gestione di processi avviati sui dispositivi connessi al servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="e2972-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="e2972-106">È possibile visualizzare i processi pianificati, in esecuzione, completati, annullati e non riusciti per più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="e2972-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="e2972-107">I risultati vengono presentati in un formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="e2972-107">Results are presented in a tabular format.</span></span> 

![Pagina dei processi](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="e2972-109">È possibile trovare rapidamente i processi desiderati filtrando i campi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e2972-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="e2972-110">**Stato** : i processi possono essere in esecuzione, completati, annullati, non riusciti, in fase di annullamento o completati con errori.</span><span class="sxs-lookup"><span data-stu-id="e2972-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="e2972-111">**Da e a** : i processi possono essere filtrati in base all'intervallo di data e ora.</span><span class="sxs-lookup"><span data-stu-id="e2972-111">**From and To** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="e2972-112">**Tipo** – il tipo di processo può essere backup, backup manuale, ripristino, clonazione, failover del dispositivo, creazione di un volume aggiunto in locale, modifica del volume, aggiornamento, pacchetto di supporto o provisioning del dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2972-112">**Type** – The job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="e2972-113">**Dispositivi** : i processi vengono avviati in un determinato dispositivo connesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="e2972-113">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  <span data-ttu-id="e2972-114">I processi filtrati vengono quindi elaborati in base ai seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="e2972-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
  * <span data-ttu-id="e2972-115">**Tipo** : backup, backup manuale, ripristino, clonazione, failover del dispositivo, creazione di un volume aggiunto in locale, modifica del volume, aggiornamento, pacchetto di supporto o provisioning del dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2972-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="e2972-116">**Stato** : in esecuzione, completati, annullati, non riusciti, in fase di annullamento o completati con errori.</span><span class="sxs-lookup"><span data-stu-id="e2972-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="e2972-117">**Entità** : i processi possono essere associati a un volume, un criterio di backup o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2972-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="e2972-118">Ad esempio, un processo di clonazione è associato a un volume, mentre un processo di backup pianificato è associato a un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="e2972-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="e2972-119">Viene creato un processo di dispositivo a causa di un ripristino di emergenza (DR) o di un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e2972-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="e2972-120">**Dispositivo** : il nome del dispositivo su cui è stato avviato il processo.</span><span class="sxs-lookup"><span data-stu-id="e2972-120">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="e2972-121">**Avviato alle** : l'ora di inizio del processo.</span><span class="sxs-lookup"><span data-stu-id="e2972-121">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="e2972-122">**Stato di avanzamento** : la percentuale di completamento di un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e2972-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="e2972-123">Per un processo completato deve sempre essere 100%.</span><span class="sxs-lookup"><span data-stu-id="e2972-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="e2972-124">L'elenco dei processi viene aggiornato ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="e2972-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="e2972-125">In questa pagina è possibile eseguire le seguenti azioni relative ai processi:</span><span class="sxs-lookup"><span data-stu-id="e2972-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="e2972-126">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="e2972-126">View job details</span></span>
* <span data-ttu-id="e2972-127">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="e2972-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="e2972-128">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="e2972-128">View job details</span></span>
<span data-ttu-id="e2972-129">Eseguire la procedura seguente per visualizzare i dettagli di qualsiasi processo.</span><span class="sxs-lookup"><span data-stu-id="e2972-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="e2972-130">Per visualizzare i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="e2972-130">To view job details</span></span>
1. <span data-ttu-id="e2972-131">Nella pagina **Processi** , visualizzare i processi desiderati eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="e2972-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="e2972-132">È possibile cercare processi completati, in esecuzione o annullati.</span><span class="sxs-lookup"><span data-stu-id="e2972-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="e2972-133">Selezionare un processo.</span><span class="sxs-lookup"><span data-stu-id="e2972-133">Select a job.</span></span>
3. <span data-ttu-id="e2972-134">Nella parte inferiore della pagina, fare clic su **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="e2972-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="e2972-135">Nella finestra di dialogo **Dettagli del processo di Backup** è possibile visualizzare la stato, i dettagli, le statistiche temporali e le statistiche sui dati.</span><span class="sxs-lookup"><span data-stu-id="e2972-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Pagina dettagli del processo](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="e2972-137">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="e2972-137">Cancel a job</span></span>
<span data-ttu-id="e2972-138">Eseguire la procedura seguente per annullare un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e2972-138">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="e2972-139">Alcuni processi, ad esempio la modifica di un volume per cambiare il tipo di volume o espandere un volume, non possono essere annullati.</span><span class="sxs-lookup"><span data-stu-id="e2972-139">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="to-cancel-a-job"></a><span data-ttu-id="e2972-140">Per annullare un processo</span><span class="sxs-lookup"><span data-stu-id="e2972-140">To cancel a job</span></span>
1. <span data-ttu-id="e2972-141">Nella pagina **Processi** , visualizzare i processi in esecuzione che si desidera annullare eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="e2972-141">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="e2972-142">Selezionare il processo.</span><span class="sxs-lookup"><span data-stu-id="e2972-142">Select the job.</span></span>
3. <span data-ttu-id="e2972-143">Nella parte inferiore della pagina fare clic su **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="e2972-143">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="e2972-144">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="e2972-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="e2972-145">Questo processo ora viene annullato.</span><span class="sxs-lookup"><span data-stu-id="e2972-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2972-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2972-146">Next steps</span></span>
* <span data-ttu-id="e2972-147">Informazioni su come [gestire i criteri di backup di StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e2972-147">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="e2972-148">Informazioni su come [utilizzare il servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e2972-148">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

