---
title: aaaView e gestire i processi di StorSimple | Documenti Microsoft
description: "Descrive una pagina di processi del servizio StorSimple Manager hello e come toouse è tootrack recenti, corrente e pianificate i processi di backup."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a><span data-ttu-id="032bf-103">Utilizzare tooview servizio StorSimple Manager di hello e gestire i processi di StorSimple</span><span class="sxs-lookup"><span data-stu-id="032bf-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="032bf-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="032bf-104">Overview</span></span>
<span data-ttu-id="032bf-105">Hello **processi** pagina fornisce un unico portale centralizzato per la visualizzazione e gestione di processi avviati nei dispositivi connessi servizio StorSimple Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="032bf-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="032bf-106">È possibile visualizzare i processi pianificati, in esecuzione, completati e non riusciti per più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="032bf-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="032bf-107">I risultati vengono presentati in un formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="032bf-107">Results are presented in a tabular format.</span></span> 

![Pagina dei processi](./media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="032bf-109">È possibile trovare rapidamente i processi di hello desiderati applicando filtri ai campi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="032bf-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="032bf-110">**Stato** : i processi possono essere in esecuzione, pianificati, non riusciti, completati, in fase di annullamento o annullati.</span><span class="sxs-lookup"><span data-stu-id="032bf-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="032bf-111">**Tipo**: i processi possono essere creati come risultato di un backup su richiesta o pianificato (**Esegui backup**), di una clonazione, di un ripristino del dispositivo o di un'operazione di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="032bf-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="032bf-112">**Dispositivi** : i processi vengono avviati in un determinato servizio tooyour di dispositivo connesso.</span><span class="sxs-lookup"><span data-stu-id="032bf-112">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
* <span data-ttu-id="032bf-113">**Da e a** : i processi possono essere intervallo di filtrato hello in base a data e ora.</span><span class="sxs-lookup"><span data-stu-id="032bf-113">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>

<span data-ttu-id="032bf-114">Hello processi filtrati possono quindi essere caratterizzati sulla base di hello della hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="032bf-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>

* <span data-ttu-id="032bf-115">**Tipo** : backup, clonazione, ripristino, failover o aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="032bf-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="032bf-116">**Stato** : in esecuzione, pianificato, non è riuscito, completato, in fase di annullamento o annullato.</span><span class="sxs-lookup"><span data-stu-id="032bf-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="032bf-117">**Entità** – processi hello possono essere associati a un volume, un criterio di backup o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="032bf-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="032bf-118">Un processo di clonazione è associato a un volume, mentre un processo di backup pianificato è associato a un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="032bf-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="032bf-119">Viene creato un processo di dispositivo a causa di un ripristino di emergenza (DR) o di un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="032bf-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="032bf-120">**Dispositivo** : hello nome di dispositivo hello in cui hello processo è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="032bf-120">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="032bf-121">**Avvio** : ora di hello inizio processo hello.</span><span class="sxs-lookup"><span data-stu-id="032bf-121">**Started On** – hello time when hello job was started.</span></span>
* <span data-ttu-id="032bf-122">**Lo stato di avanzamento** : hello percentuale di completamento di un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="032bf-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="032bf-123">Per un processo completato deve sempre essere 100%.</span><span class="sxs-lookup"><span data-stu-id="032bf-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="032bf-124">elenco di Hello dei processi viene aggiornato ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="032bf-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="032bf-125">È possibile eseguire hello seguenti le azioni correlate al processo in questa pagina:</span><span class="sxs-lookup"><span data-stu-id="032bf-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="032bf-126">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="032bf-126">View job details</span></span>
* <span data-ttu-id="032bf-127">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="032bf-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="032bf-128">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="032bf-128">View job details</span></span>
<span data-ttu-id="032bf-129">Eseguire i seguenti passaggi tooview hello dettagli di qualsiasi processo hello.</span><span class="sxs-lookup"><span data-stu-id="032bf-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="032bf-130">dettagli dei processi tooview</span><span class="sxs-lookup"><span data-stu-id="032bf-130">tooview job details</span></span>
1. <span data-ttu-id="032bf-131">In hello **processi** pagina, visualizzare i processi di hello desiderati eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="032bf-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="032bf-132">È possibile cercare processi completati, in esecuzione o annullati.</span><span class="sxs-lookup"><span data-stu-id="032bf-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="032bf-133">Selezionare un processo.</span><span class="sxs-lookup"><span data-stu-id="032bf-133">Select a job.</span></span>
3. <span data-ttu-id="032bf-134">Nella parte inferiore di hello della pagina hello, fare clic su **dettagli**.</span><span class="sxs-lookup"><span data-stu-id="032bf-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="032bf-135">In hello **dettagli dei processi di Backup** nella finestra di dialogo è possibile visualizzare lo stato di hello, dettagli, le statistiche temporali e le statistiche sui dati.</span><span class="sxs-lookup"><span data-stu-id="032bf-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="032bf-136">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="032bf-136">Cancel a job</span></span>
<span data-ttu-id="032bf-137">Eseguire hello seguendo i passaggi toocancel un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="032bf-137">Perform hello following steps toocancel a running job.</span></span>

### <a name="toocancel-a-job"></a><span data-ttu-id="032bf-138">toocancel un processo</span><span class="sxs-lookup"><span data-stu-id="032bf-138">toocancel a job</span></span>
1. <span data-ttu-id="032bf-139">In hello **processi** pagina, visualizzare i processi in esecuzione di hello che si desidera toocancel eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="032bf-139">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="032bf-140">Selezionare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="032bf-140">Select hello job.</span></span>
3. <span data-ttu-id="032bf-141">Nella parte inferiore di hello della pagina hello, fare clic su **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="032bf-141">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="032bf-142">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="032bf-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="032bf-143">Questo processo ora viene annullato.</span><span class="sxs-lookup"><span data-stu-id="032bf-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="032bf-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="032bf-144">Next steps</span></span>
* <span data-ttu-id="032bf-145">Informazioni su come troppo[gestire i criteri di backup di StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="032bf-145">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="032bf-146">Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="032bf-146">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

