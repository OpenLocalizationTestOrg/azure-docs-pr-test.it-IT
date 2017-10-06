---
title: aaaView e gestire i processi per StorSimple serie 8000 | Documenti Microsoft
description: "Viene descritto pannello processi del servizio di gestione di dispositivi StorSimple hello e come toouse è tootrack recenti, corrente e pianificate i processi di backup."
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
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="32b8e-103">Utilizzare tooview servizio di gestione di dispositivi StorSimple hello e gestire i processi (Update 3 e versioni successivo)</span><span class="sxs-lookup"><span data-stu-id="32b8e-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="32b8e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="32b8e-104">Overview</span></span>
<span data-ttu-id="32b8e-105">Hello **processi** pannello fornisce un unico portale centralizzato per la visualizzazione e gestione di processi avviati nei dispositivi connessi tooyour servizio di gestione di dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="32b8e-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="32b8e-106">È possibile visualizzare i processi pianificati, in esecuzione, completati, annullati e non riusciti per più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="32b8e-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="32b8e-107">I risultati vengono presentati in un formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="32b8e-107">Results are presented in a tabular format.</span></span>

![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="32b8e-109">È possibile trovare rapidamente i processi di hello desiderati applicando filtri ai campi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="32b8e-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="32b8e-110">**Stato**: i processi possono essere in corso, completati, annullati, non riusciti, annullati o completati con errori.</span><span class="sxs-lookup"><span data-stu-id="32b8e-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="32b8e-111">**Intervallo di tempo** : i processi possono essere intervallo di filtrato hello in base a data e ora.</span><span class="sxs-lookup"><span data-stu-id="32b8e-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="32b8e-112">gli intervalli hello sono oltre 1 ora, ultime 24 ore, negli ultimi 7 giorni, agli ultimi 30 giorni, l'anno o data personalizzato.</span><span class="sxs-lookup"><span data-stu-id="32b8e-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="32b8e-113">**Tipo** : il tipo di processo hello può essere pianificati backup, backup manuale, backup di ripristino, clonare volume, eseguire il failover contenitori di volumi, creare volume aggiunto in locale, modifica del volume, installare gli aggiornamenti, raccogliere i log di supporto e creare appliance di cloud.</span><span class="sxs-lookup"><span data-stu-id="32b8e-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="32b8e-114">**Dispositivi** : i processi vengono avviati in un determinato servizio tooyour di dispositivo connesso.</span><span class="sxs-lookup"><span data-stu-id="32b8e-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="32b8e-115">Hello processi filtrati possono quindi essere caratterizzati sulla base di hello della hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="32b8e-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="32b8e-116">**Nome**: backup pianificato, backup manuale, backup di ripristino, volume clone, contenitori dei volumi con failover, volume aggiunto in locale, volume modificato, installazione di aggiornamenti, raccolta di log di supporto e creazione di appliance cloud.</span><span class="sxs-lookup"><span data-stu-id="32b8e-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="32b8e-117">**Stato** : in esecuzione, completati, annullati, non riusciti, in fase di annullamento o completati con errori.</span><span class="sxs-lookup"><span data-stu-id="32b8e-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="32b8e-118">**Entità** – processi hello possono essere associati a un volume, un criterio di backup o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="32b8e-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="32b8e-119">Ad esempio, un processo di clonazione è associato a un volume, mentre un processo di backup pianificato è associato a un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="32b8e-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="32b8e-120">Viene creato un processo di dispositivo a causa di un ripristino di emergenza (DR) o di un'operazione di ripristino.</span><span class="sxs-lookup"><span data-stu-id="32b8e-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="32b8e-121">**Dispositivo** : hello nome di dispositivo hello in cui hello processo è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="32b8e-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="32b8e-122">**Avviato su** : ora di hello inizio processo hello.</span><span class="sxs-lookup"><span data-stu-id="32b8e-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="32b8e-123">**Durata** : processo di hello hello timer toocomplete obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="32b8e-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="32b8e-124">elenco di Hello dei processi viene aggiornato ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="32b8e-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="32b8e-125">È possibile eseguire hello seguenti le azioni correlate al processo in questa pagina:</span><span class="sxs-lookup"><span data-stu-id="32b8e-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="32b8e-126">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="32b8e-126">View job details</span></span>
* <span data-ttu-id="32b8e-127">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="32b8e-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="32b8e-128">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="32b8e-128">View job details</span></span>
<span data-ttu-id="32b8e-129">Eseguire i seguenti passaggi tooview hello dettagli di qualsiasi processo hello.</span><span class="sxs-lookup"><span data-stu-id="32b8e-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="32b8e-130">dettagli dei processi tooview</span><span class="sxs-lookup"><span data-stu-id="32b8e-130">tooview job details</span></span>
1. <span data-ttu-id="32b8e-131">Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **processi**.</span><span class="sxs-lookup"><span data-stu-id="32b8e-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="32b8e-132">In hello **processi** blade, visualizzazione hello processi desiderati eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="32b8e-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="32b8e-133">È possibile cercare processi completati, in esecuzione o annullati.</span><span class="sxs-lookup"><span data-stu-id="32b8e-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="32b8e-135">Selezionare e fare clic su un processo.</span><span class="sxs-lookup"><span data-stu-id="32b8e-135">Select and click a job.</span></span>

    ![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="32b8e-137">Nel Pannello di dettagli processo hello, è possibile visualizzare lo stato di hello, dettagli, le statistiche temporali e le statistiche sui dati.</span><span class="sxs-lookup"><span data-stu-id="32b8e-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Dettagli del processo](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="32b8e-139">Annullare un processo</span><span class="sxs-lookup"><span data-stu-id="32b8e-139">Cancel a job</span></span>
<span data-ttu-id="32b8e-140">Eseguire hello seguendo i passaggi toocancel un processo in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="32b8e-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="32b8e-141">Alcuni processi, ad esempio modifica di un tipo di volume hello toochange volume o espansione di un volume, non possono essere annullati.</span><span class="sxs-lookup"><span data-stu-id="32b8e-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="32b8e-142">toocancel un processo</span><span class="sxs-lookup"><span data-stu-id="32b8e-142">toocancel a job</span></span>
1. <span data-ttu-id="32b8e-143">In hello **processi** pagina, visualizzare i processi in esecuzione di hello che si desidera toocancel eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="32b8e-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="32b8e-144">Selezionare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="32b8e-144">Select hello job.</span></span>

2. <span data-ttu-id="32b8e-145">Fare clic sul menu di scelta rapida hello tooinvoke hello processo selezionato e fare clic su **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="32b8e-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![Dettagli del processo](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="32b8e-147">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="32b8e-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="32b8e-148">Questo processo ora viene annullato.</span><span class="sxs-lookup"><span data-stu-id="32b8e-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32b8e-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32b8e-149">Next steps</span></span>
* <span data-ttu-id="32b8e-150">Informazioni su come troppo[gestire i criteri di backup di StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="32b8e-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="32b8e-151">Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="32b8e-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

