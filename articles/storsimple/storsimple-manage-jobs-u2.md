---
title: aaaView e gestire i processi di StorSimple | Documenti Microsoft
description: "Descrive una pagina di processi del servizio StorSimple Manager hello e come toouse è tootrack recenti, corrente e pianificate i processi di backup."
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
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="108ea-103">Utilizzare tooview servizio StorSimple Manager di hello e gestire i processi di StorSimple (Update 2)</span><span class="sxs-lookup"><span data-stu-id="108ea-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="108ea-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="108ea-104">Overview</span></span>
<span data-ttu-id="108ea-105">Hello **processi** pagina fornisce un unico portale centralizzato per la visualizzazione e gestione di processi avviati nei dispositivi connessi servizio StorSimple Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="108ea-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="108ea-106">È possibile visualizzare i processi pianificati, in esecuzione, completati, annullati e non riusciti per più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="108ea-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="108ea-107">I risultati vengono presentati in un formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="108ea-107">Results are presented in a tabular format.</span></span> 

![Pagina dei processi](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="108ea-109">È possibile trovare rapidamente i processi di hello desiderati applicando filtri ai campi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="108ea-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="108ea-110">**Stato** : i processi possono essere in esecuzione, completati, annullati, non riusciti, in fase di annullamento o completati con errori.</span><span class="sxs-lookup"><span data-stu-id="108ea-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="108ea-111">**Da e a** : i processi possono essere intervallo di filtrato hello in base a data e ora.</span><span class="sxs-lookup"><span data-stu-id="108ea-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="108ea-112">**Tipo** -tipo di processo hello è possibile eseguire il backup, backup manuale, ripristino, clonazione, failover del dispositivo, creare un volume aggiunto in locale, modifica del volume, aggiornare, supporta il pacchetto o provisioning del dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="108ea-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="108ea-113">**Dispositivi** : i processi vengono avviati in un determinato servizio tooyour di dispositivo connesso.</span><span class="sxs-lookup"><span data-stu-id="108ea-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="108ea-114">Hello processi filtrati possono quindi essere caratterizzati sulla base di hello della hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="108ea-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="108ea-115">**Tipo** : backup, backup manuale, ripristino, clonazione, failover del dispositivo, creazione di un volume aggiunto in locale, modifica del volume, aggiornamento, pacchetto di supporto o provisioning del dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="108ea-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="108ea-116">**Stato** : in esecuzione, completati, annullati, non riusciti, in fase di annullamento o completati con errori.</span><span class="sxs-lookup"><span data-stu-id="108ea-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="108ea-117">**Entità** – processi hello possono essere associati a un volume, un criterio di backup o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="108ea-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="108ea-118">Ad esempio, un processo di clonazione è associato a un volume, mentre un processo di backup pianificato è associato a un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="108ea-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="108ea-119">Viene creato un processo di dispositivo a causa di un ripristino di emergenza (DR) o di un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="108ea-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="108ea-120">**Dispositivo** : hello nome di dispositivo hello in cui hello processo è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="108ea-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="108ea-121">**Avviato su** : ora di hello inizio processo hello.</span><span class="sxs-lookup"><span data-stu-id="108ea-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="108ea-122">**Lo stato di avanzamento** : hello percentuale di completamento di un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="108ea-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="108ea-123">Per un processo completato deve sempre essere 100%.</span><span class="sxs-lookup"><span data-stu-id="108ea-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="108ea-124">elenco di Hello dei processi viene aggiornato ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="108ea-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="108ea-125">È possibile eseguire hello seguenti le azioni correlate al processo in questa pagina:</span><span class="sxs-lookup"><span data-stu-id="108ea-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="108ea-126">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="108ea-126">View job details</span></span>
* <span data-ttu-id="108ea-127">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="108ea-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="108ea-128">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="108ea-128">View job details</span></span>
<span data-ttu-id="108ea-129">Eseguire i seguenti passaggi tooview hello dettagli di qualsiasi processo hello.</span><span class="sxs-lookup"><span data-stu-id="108ea-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="108ea-130">dettagli dei processi tooview</span><span class="sxs-lookup"><span data-stu-id="108ea-130">tooview job details</span></span>
1. <span data-ttu-id="108ea-131">In hello **processi** pagina, visualizzare i processi di hello desiderati eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="108ea-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="108ea-132">È possibile cercare processi completati, in esecuzione o annullati.</span><span class="sxs-lookup"><span data-stu-id="108ea-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="108ea-133">Selezionare un processo.</span><span class="sxs-lookup"><span data-stu-id="108ea-133">Select a job.</span></span>
3. <span data-ttu-id="108ea-134">Nella parte inferiore di hello della pagina hello, fare clic su **dettagli**.</span><span class="sxs-lookup"><span data-stu-id="108ea-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="108ea-135">In hello **dettagli dei processi di Backup** nella finestra di dialogo è possibile visualizzare lo stato di hello, dettagli, le statistiche temporali e le statistiche sui dati.</span><span class="sxs-lookup"><span data-stu-id="108ea-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Pagina dettagli del processo](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="108ea-137">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="108ea-137">Cancel a job</span></span>
<span data-ttu-id="108ea-138">Eseguire hello seguendo i passaggi toocancel un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="108ea-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="108ea-139">Alcuni processi, ad esempio modifica di un tipo di volume hello toochange volume o espansione di un volume, non possono essere annullati.</span><span class="sxs-lookup"><span data-stu-id="108ea-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="108ea-140">toocancel un processo</span><span class="sxs-lookup"><span data-stu-id="108ea-140">toocancel a job</span></span>
1. <span data-ttu-id="108ea-141">In hello **processi** pagina, visualizzare i processi in esecuzione di hello che si desidera toocancel eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="108ea-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="108ea-142">Selezionare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="108ea-142">Select hello job.</span></span>
3. <span data-ttu-id="108ea-143">Nella parte inferiore di hello della pagina hello, fare clic su **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="108ea-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="108ea-144">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="108ea-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="108ea-145">Questo processo ora viene annullato.</span><span class="sxs-lookup"><span data-stu-id="108ea-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="108ea-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="108ea-146">Next steps</span></span>
* <span data-ttu-id="108ea-147">Informazioni su come troppo[gestire i criteri di backup di StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="108ea-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="108ea-148">Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="108ea-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

