---
title: esercitazione backup di Azure StorSimple Virtual Array aaaMicrosoft | Documenti Microsoft
description: Viene descritto come tooback configurazione di StorSimple Virtual Array condivisioni e volumi.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="8c3b8-103">Eseguire il backup di condivisioni o volumi nell'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="8c3b8-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="8c3b8-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8c3b8-104">Overview</span></span>

<span data-ttu-id="8c3b8-105">Hello Array virtuale StorSimple è un ibrido cloud archiviazione nel dispositivo virtuale locale che può essere configurato come un file server o server iSCSI.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="8c3b8-106">array virtuale Hello consente backup pianificato e manuale di tutti i volumi o condivisioni hello hello utente toocreate sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="8c3b8-107">Quando viene configurato come file server, consente anche il ripristino a livello di elemento.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="8c3b8-108">In questa esercitazione viene descritto come toocreate pianificata e backup manuali ed eseguire il ripristino a livello di elemento toorestore un file eliminato sull'array virtuale.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="8c3b8-109">Questa esercitazione si applica matrici solo di toohello StorSimple virtuale.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="8c3b8-110">Per informazioni sulla 8000 serie, andare troppo[creare un backup per i dispositivi 8000 serie](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="8c3b8-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="8c3b8-111">Backup di condivisioni e volumi</span><span class="sxs-lookup"><span data-stu-id="8c3b8-111">Back up shares and volumes</span></span>

<span data-ttu-id="8c3b8-112">I backup garantiscono la protezione temporizzata, migliorano la recuperabilità e riducono al minimo i tempi di ripristino per le condivisioni e i volumi.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="8c3b8-113">È possibile eseguire il backup di una condivisione o di un volume sul dispositivo StorSimple in due modi: **Pianificato** o **Manuale**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="8c3b8-114">Ciascuno dei metodi hello è descritto nelle seguenti sezioni hello.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="8c3b8-115">Modificare l'ora di inizio backup hello</span><span class="sxs-lookup"><span data-stu-id="8c3b8-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="8c3b8-116">In questa versione, i backup pianificati vengono creati tramite un criterio predefinito che viene eseguito quotidianamente in un momento specificato ed esegue il backup di tutti i volumi o condivisioni hello dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="8c3b8-117">Non è possibile toocreate criteri personalizzati per i backup pianificati in questo momento.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="8c3b8-118">L'Array virtuale StorSimple è un criterio di backup predefinito che inizia in corrispondenza di un'ora specificata del giorno (22:30) ed esegue il backup di tutti i volumi o condivisioni hello dispositivo hello una volta al giorno.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="8c3b8-119">È possibile modificare il tempo di hello quali avvio del backup hello, ma la frequenza di hello e hello conservazione (che specifica il numero di hello di backup tooretain) non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="8c3b8-120">Durante questi backup, il dispositivo virtuale intera hello viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="8c3b8-121">Questo potrebbe potenzialmente hello delle prestazioni del dispositivo hello e influire sui carichi di lavoro hello distribuiti nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="8c3b8-122">È pertanto consigliabile pianificare queste operazioni in orari di scarso traffico.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="8c3b8-123">ora di inizio di toochange hello predefinite di backup, eseguire i passaggi hello hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8c3b8-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="8c3b8-124">hello toochange ora di inizio per criteri di backup predefinito hello</span><span class="sxs-lookup"><span data-stu-id="8c3b8-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="8c3b8-125">Andare troppo**dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-125">Go too**Devices**.</span></span> <span data-ttu-id="8c3b8-126">verrà visualizzato l'elenco di Hello di dispositivi registrati con il servizio di gestione di dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![passare toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="8c3b8-128">Selezionare e fare clic sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-128">Select and click your device.</span></span> <span data-ttu-id="8c3b8-129">Hello **impostazioni** pannello verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="8c3b8-130">Andare troppo**Gestisci > Criteri di Backup**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-130">Go too**Manage > Backup policies**.</span></span>
   
    ![selezionare il dispositivo](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="8c3b8-132">In hello **criteri di Backup** pannello, ora di inizio predefinita hello è 22:30.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="8c3b8-133">È possibile specificare hello nuova ora di inizio per la pianificazione giornaliera hello nel fuso orario del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![passare toobackup criteri](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="8c3b8-135">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="8c3b8-136">Creazione di un backup manuale</span><span class="sxs-lookup"><span data-stu-id="8c3b8-136">Take a manual backup</span></span>

<span data-ttu-id="8c3b8-137">Inoltre tooscheduled backup, è possibile eseguire un backup manuale (su richiesta) di dati del dispositivo in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="8c3b8-138">toocreate un backup manuale</span><span class="sxs-lookup"><span data-stu-id="8c3b8-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="8c3b8-139">Andare troppo**dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-139">Go too**Devices**.</span></span> <span data-ttu-id="8c3b8-140">Selezionare il dispositivo e fare doppio clic su **...**  all'estrema destra hello nella riga selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="8c3b8-141">Selezionare il menu di scelta rapida hello **eseguire backup**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-141">From hello context menu, select **Take backup**.</span></span>
   
    ![passare tootake backup](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="8c3b8-143">In hello **eseguire backup** pannello, fare clic su **eseguire backup**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="8c3b8-144">Si eseguirà il backup tutte le condivisioni in file server di hello hello o tutti i volumi di hello del server iSCSI.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![avvio di backup](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="8c3b8-146">Viene avviato un backup su richiesta e visualizzata una notifica indicante che il processo di backup è in corso.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![avvio di backup](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="8c3b8-148">Al termine il processo di hello, ricevono una notifica nuovamente.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="8c3b8-149">processo di backup di Hello viene quindi avviato.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-149">hello backup process then starts.</span></span>
   
    ![processo di backup creato](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="8c3b8-151">stato di avanzamento hello tootrack di backup hello ed esaminare i dettagli dei processi hello, fare clic su notifica hello.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="8c3b8-152">Consente di andare troppo **dettagli del processo**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-152">This takes you too **Job details**.</span></span>
   
     ![dettagli del processo di backup](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="8c3b8-154">Dopo il backup di hello è completo, andare troppo**gestione > catalogo di Backup**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="8c3b8-155">Verrà visualizzato uno snapshot nel cloud di tutte le condivisioni di hello (o i volumi) nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Backup completato](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="8c3b8-157">Visualizzare i backup esistenti</span><span class="sxs-lookup"><span data-stu-id="8c3b8-157">View existing backups</span></span>
<span data-ttu-id="8c3b8-158">tooview hello i backup esistenti, eseguire operazioni nel portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="8c3b8-159">backup esistenti tooview</span><span class="sxs-lookup"><span data-stu-id="8c3b8-159">tooview existing backups</span></span>

1. <span data-ttu-id="8c3b8-160">Andare troppo**dispositivi** blade.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-160">Go too**Devices** blade.</span></span> <span data-ttu-id="8c3b8-161">Selezionare e fare clic sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-161">Select and click your device.</span></span> <span data-ttu-id="8c3b8-162">In hello **impostazioni** pannello andare troppo**gestione > catalogo di Backup**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Passare toobackup catalogo](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="8c3b8-164">Specificare hello toobe criteri utilizzato per il filtro seguente:</span><span class="sxs-lookup"><span data-stu-id="8c3b8-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="8c3b8-165">**Intervallo di tempo**: può essere **Ultima ora**, **Ultime 24 ore**, **Ultimi 7 giorni**, **Ultimi 30 giorni**, **Ultimo anno** e **Data personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="8c3b8-166">**Dispositivi** : selezionare dall'elenco di hello del file server o server iSCSI registrati con il servizio di gestione di dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="8c3b8-167">**Avviato**: può essere **Pianificato** automaticamente tramite criteri di backup o avviato **Manualmente** dall'utente.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filtro backup](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="8c3b8-169">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-169">Click **Apply**.</span></span> <span data-ttu-id="8c3b8-170">Hello elenco filtrato di backup viene visualizzato in hello **catalogo di Backup** blade.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="8c3b8-171">Si noti che è possibile visualizzare solo 100 elementi di backup alla volta.</span><span class="sxs-lookup"><span data-stu-id="8c3b8-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Catalogo di backup aggiornato](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="8c3b8-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c3b8-173">Next steps</span></span>

<span data-ttu-id="8c3b8-174">Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="8c3b8-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

