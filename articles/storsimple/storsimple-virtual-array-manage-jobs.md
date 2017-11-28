---
title: aaaView e gestire i processi di Array virtuale StorSimple | Documenti Microsoft
description: "Viene descritto pagina processi del servizio di gestione di dispositivi StorSimple hello e come toouse è tootrack recenti e corrente dei processi di hello Array virtuale StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="bbcb0-103">Utilizzare processi tooview del servizio di gestione di dispositivi StorSimple hello per hello Array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="bbcb0-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="bbcb0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bbcb0-104">Overview</span></span>
<span data-ttu-id="bbcb0-105">Hello **processi** pannello fornisce un unico portale centralizzato per visualizzare e gestire i processi avviati su array virtuale che sono connessi tooyour servizio di gestione di dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="bbcb0-106">È possibile visualizzare i processi in esecuzione, completati e non riusciti per più dispositivi virtuali.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="bbcb0-107">I risultati vengono presentati in un formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-107">Results are presented in a tabular format.</span></span>

![Pannello Processi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="bbcb0-109">È possibile trovare rapidamente i processi di hello desiderati applicando filtri ai campi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="bbcb0-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="bbcb0-110">**Intervallo di tempo** : i processi possono essere intervallo di filtrato hello in base a data e ora.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="bbcb0-111">**Dispositivi** : i processi vengono avviati in un servizio tooyour specifico dispositivo connesso.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="bbcb0-112">Hello processi filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bbcb0-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="bbcb0-113">**Nome** : nome del processo hello può essere **tutti**, **Backup**, **Clone**, **failover**, **scaricare gli aggiornamenti** , o **installare gli aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="bbcb0-114">**Stato**: i processi possono essere **Tutto**, **In corso**, **Riuscito**, **Operazione non riuscita** o **Annullato**.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="bbcb0-115">**Entità** – processi hello possono essere associati a un volume, condivisione o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="bbcb0-116">**Dispositivo** : hello nome di dispositivo hello in cui hello processo è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="bbcb0-117">**Avviato su** : ora di hello inizio processo hello.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="bbcb0-118">**Durata** : hello durata per il processo di hello è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="bbcb0-119">**Stato** : è possibile cercare tutti i processi in esecuzione, completati o non riusciti.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="bbcb0-120">**Tipo di processo** : tipo di processo hello può essere all, eseguire il backup, ripristino failover, scaricare gli aggiornamenti o installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="bbcb0-121">elenco di Hello dei processi viene aggiornato ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="bbcb0-122">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="bbcb0-122">View job details</span></span>
<span data-ttu-id="bbcb0-123">Eseguire i seguenti passaggi tooview hello dettagli di qualsiasi processo hello.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="bbcb0-124">dettagli dei processi tooview</span><span class="sxs-lookup"><span data-stu-id="bbcb0-124">tooview job details</span></span>
1. <span data-ttu-id="bbcb0-125">In hello **processi** blade, visualizzazione hello processi desiderati eseguendo una query con filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="bbcb0-126">È possibile cercare processi completati o in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="bbcb0-127">Selezionare un processo dall'elenco tabulare di hello dei processi.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![Pannello Processi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="bbcb0-129">Nella parte inferiore di hello della pagina hello, fare clic su **dettagli**.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="bbcb0-130">In hello **dettagli** nella finestra di dialogo è possibile visualizzare lo stato, dettagli e le statistiche temporali.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="bbcb0-131">Hello nella figura seguente viene illustrato un esempio di hello **dettagli dei processi di Backup** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![Dettagli del processo](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="bbcb0-133">Errore del processo quando viene sospesa macchina virtuale hello nell'hypervisor hello</span><span class="sxs-lookup"><span data-stu-id="bbcb0-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="bbcb0-134">Quando un processo è in corso nel dispositivo hello (macchina virtuale in hypervisor provisioning) e Array virtuale StorSimple è sospeso per più di 15 minuti, hello processo non riesce.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="bbcb0-135">Questa scadenza ora Array virtuale StorSimple tooyour viene sincronizzata con il tempo di Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="bbcb0-136">Verrà visualizzato il seguente errore hello: "l'ora del dispositivo non è sincronizzato con il tempo di Microsoft Azure hello da più di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="bbcb0-137">Verificare che hello hypervisor e tempi di hello dispositivo siano sincronizzati con un NTP si trova.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="bbcb0-138">Assicurarsi che non vi siano problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="bbcb0-139">problemi di connettività tootroubleshoot, eseguire i test diagnostici da hello interfaccia web locale del dispositivo virtuale."</span><span class="sxs-lookup"><span data-stu-id="bbcb0-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="bbcb0-140">Questi errori si applicano i processi toobackup, ripristino, aggiornamento e il failover.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="bbcb0-141">Se viene eseguito il provisioning di macchina virtuale in Hyper-V, macchina hello infine Sincronizza ora con l'hypervisor.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="bbcb0-142">Quando ciò accade, è possibile riavviare il processo.</span><span class="sxs-lookup"><span data-stu-id="bbcb0-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbcb0-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bbcb0-143">Next steps</span></span>
<span data-ttu-id="bbcb0-144">[Informazioni su come toouse hello tooadminister dell'interfaccia utente web locale l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="bbcb0-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

