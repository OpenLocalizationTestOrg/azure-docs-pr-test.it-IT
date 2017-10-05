---
title: Visualizzare e gestire i processi dell'array virtuale StorSimple | Documentazione Microsoft
description: "Descrive la pagina Processi del servizio Gestione dispositivi StorSimple e illustra come è possibile tenere traccia dei processi recenti e correnti per l'array virtuale StorSimple."
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
ms.openlocfilehash: 3fd1c262a8ce94d8e98f2b066a8028d974b15b1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="a30d9-103">Usare il servizio Gestione dispositivi StorSimple per visualizzare i processi per l'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="a30d9-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="a30d9-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a30d9-104">Overview</span></span>
<span data-ttu-id="a30d9-105">Il pannello **Processi** fornisce un unico portale centralizzato per la visualizzazione e la gestione dei processi avviati sugli array virtuali connessi al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a30d9-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="a30d9-106">È possibile visualizzare i processi in esecuzione, completati e non riusciti per più dispositivi virtuali.</span><span class="sxs-lookup"><span data-stu-id="a30d9-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="a30d9-107">I risultati vengono presentati in un formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="a30d9-107">Results are presented in a tabular format.</span></span>

![Pannello Processi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="a30d9-109">È possibile trovare rapidamente i processi desiderati filtrando i campi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a30d9-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="a30d9-110">**Intervallo di tempo**: i processi possono essere filtrati in base all'intervallo di data e ora.</span><span class="sxs-lookup"><span data-stu-id="a30d9-110">**Time range** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="a30d9-111">**Dispositivi** : i processi vengono avviati in un dispositivo specifico connesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="a30d9-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="a30d9-112">I processi filtrati vengono quindi catalogati in base ai seguenti attributi:</span><span class="sxs-lookup"><span data-stu-id="a30d9-112">The filtered jobs are then tabulated based on the following attributes:</span></span>
  
  * <span data-ttu-id="a30d9-113">**Nome**: il nome del processo può essere **Tutto**, **Backup**, **Clona**, **Effettua il failover**, **Scarica aggiornamenti** o **Installa aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="a30d9-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="a30d9-114">**Stato**: i processi possono essere **Tutto**, **In corso**, **Riuscito**, **Operazione non riuscita** o **Annullato**.</span><span class="sxs-lookup"><span data-stu-id="a30d9-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="a30d9-115">**Entità** : i processi possono essere associati a un volume, una condivisione o un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a30d9-115">**Entity** – The jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="a30d9-116">**Dispositivo** : il nome del dispositivo su cui è stato avviato il processo.</span><span class="sxs-lookup"><span data-stu-id="a30d9-116">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="a30d9-117">**Avviato alle** : l'ora di inizio del processo.</span><span class="sxs-lookup"><span data-stu-id="a30d9-117">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="a30d9-118">**Durata**: la durata di esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="a30d9-118">**Duration** – The duration for on which the job was run.</span></span>
* <span data-ttu-id="a30d9-119">**Stato** : è possibile cercare tutti i processi in esecuzione, completati o non riusciti.</span><span class="sxs-lookup"><span data-stu-id="a30d9-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="a30d9-120">**Tipo di processo**: il processo può essere di tipo tutto, backup, ripristino, failover, scarica aggiornamenti o installa aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="a30d9-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="a30d9-121">L'elenco dei processi viene aggiornato ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="a30d9-121">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="a30d9-122">Visualizza i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="a30d9-122">View job details</span></span>
<span data-ttu-id="a30d9-123">Eseguire la procedura seguente per visualizzare i dettagli di qualsiasi processo.</span><span class="sxs-lookup"><span data-stu-id="a30d9-123">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="a30d9-124">Per visualizzare i dettagli dei processi</span><span class="sxs-lookup"><span data-stu-id="a30d9-124">To view job details</span></span>
1. <span data-ttu-id="a30d9-125">Nel pannello **Processi** visualizzare i processi desiderati eseguendo una query con i filtri appropriati.</span><span class="sxs-lookup"><span data-stu-id="a30d9-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="a30d9-126">È possibile cercare processi completati o in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a30d9-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="a30d9-127">Selezionare un processo nell'elenco tabulare dei processi.</span><span class="sxs-lookup"><span data-stu-id="a30d9-127">Select a job from the tabular list of jobs.</span></span>
   
    ![Pannello Processi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="a30d9-129">Nella parte inferiore della pagina, fare clic su **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="a30d9-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="a30d9-130">Nella finestra di dialogo **Dettagli** è possibile visualizzare statistiche temporali, sullo stato e sui dettagli.</span><span class="sxs-lookup"><span data-stu-id="a30d9-130">In the **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="a30d9-131">La figura seguente mostra un esempio della finestra di dialogo relativa ai **dettagli del processo di backup** :</span><span class="sxs-lookup"><span data-stu-id="a30d9-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![Dettagli del processo](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="a30d9-133">Errori di processo quando la macchina virtuale viene sospesa nell'hypervisor</span><span class="sxs-lookup"><span data-stu-id="a30d9-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="a30d9-134">Se nell'array virtuale StorSimple è in corso un processo e il dispositivo (macchina virtuale con provisioning in hypervisor) viene sospeso per più di 15 minuti, il processo ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a30d9-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span></span> <span data-ttu-id="a30d9-135">Ciò è dovuto al fatto che l'ora dell'array virtuale StorSimple non è più sincronizzata con l'ora di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a30d9-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> 

<span data-ttu-id="a30d9-136">Verrà visualizzato un errore indicante che l'ora del dispositivo non è sincronizzata con l'ora di Microsoft Azure per un valore superiore a 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="a30d9-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="a30d9-137">Verificare che l'hypervisor e il dispositivo siano ora sincronizzati con un server NTP.</span><span class="sxs-lookup"><span data-stu-id="a30d9-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="a30d9-138">Assicurarsi che non vi siano problemi di connettività.</span><span class="sxs-lookup"><span data-stu-id="a30d9-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="a30d9-139">Per risolvere i problemi di connettività, eseguire i test diagnostici dall'interfaccia utente Web locale del dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="a30d9-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span></span>

<span data-ttu-id="a30d9-140">Questi errori possono verificarsi con processi di backup, ripristino, aggiornamento e failover.</span><span class="sxs-lookup"><span data-stu-id="a30d9-140">These failures apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="a30d9-141">Se il provisioning della macchina virtuale viene eseguito in Hyper-V, l'ora della macchina virtuale alla fine si sincronizza con l'hypervisor.</span><span class="sxs-lookup"><span data-stu-id="a30d9-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="a30d9-142">Quando ciò accade, è possibile riavviare il processo.</span><span class="sxs-lookup"><span data-stu-id="a30d9-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a30d9-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a30d9-143">Next steps</span></span>
<span data-ttu-id="a30d9-144">[Informazioni su come usare l'interfaccia utente Web locale per amministrare l'array virtuale StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a30d9-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

