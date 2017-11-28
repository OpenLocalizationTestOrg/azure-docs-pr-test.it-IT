---
title: criteri di backup di Snapshot Manager aaaStorSimple | Documenti Microsoft
description: Viene descritto come toouse hello toocreate snap-in MMC di StorSimple Snapshot Manager e gestire i criteri di backup hello che controllano i backup pianificati.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="a9497-103">Utilizzare Gestione Snapshot StorSimple toocreate e gestire i criteri di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="a9497-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a9497-104">Overview</span></span>
<span data-ttu-id="a9497-105">Un criterio di backup crea una pianificazione per il backup dei dati del volume in locale o cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a9497-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="a9497-106">Quando si crea un criterio di backup, è inoltre possibile specificare un criterio di conservazione.</span><span class="sxs-lookup"><span data-stu-id="a9497-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="a9497-107">(È possibile conservare un massimo di 64 snapshot). Per altre informazioni sui criteri di backup, vedere [Tipi di backup](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) nell'articolo relativo a [StorSimple serie 8000: una soluzione cloud ibrida](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9497-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="a9497-108">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="a9497-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="a9497-109">Creare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-109">Create a backup policy</span></span>
* <span data-ttu-id="a9497-110">Modifica di un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-110">Edit a backup policy</span></span>
* <span data-ttu-id="a9497-111">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="a9497-112">Creare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-112">Create a backup policy</span></span>
<span data-ttu-id="a9497-113">Utilizzare hello seguendo procedure toocreate nuovi criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="a9497-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="a9497-114">toocreate un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="a9497-115">Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a9497-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a9497-116">In hello **ambito** riquadro destro **criteri di Backup**, fare clic su **Crea criteri di Backup**.</span><span class="sxs-lookup"><span data-stu-id="a9497-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Creare un criterio di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="a9497-118">Hello **creare un criterio** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a9497-118">hello **Create a Policy** dialog box appears.</span></span>

    ![Creazione di un criterio - scheda Generale](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="a9497-120">In hello **generale** scheda, hello completa le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="a9497-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="a9497-121">In hello **nome** casella di testo, digitare un nome per il criterio di hello.</span><span class="sxs-lookup"><span data-stu-id="a9497-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="a9497-122">In hello **gruppo di volumi** casella di testo, nome del gruppo di volumi hello associata al criterio di hello hello di tipo.</span><span class="sxs-lookup"><span data-stu-id="a9497-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="a9497-123">Selezionare **Snapshot locale** o **Snapshot cloud**.</span><span class="sxs-lookup"><span data-stu-id="a9497-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="a9497-124">Selezionare il numero di hello di tooretain snapshot.</span><span class="sxs-lookup"><span data-stu-id="a9497-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="a9497-125">Se si seleziona **tutti**, verranno conservati 64 snapshot (Buongiorno massimo).</span><span class="sxs-lookup"><span data-stu-id="a9497-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="a9497-126">Fare clic su hello **pianificazione** scheda.</span><span class="sxs-lookup"><span data-stu-id="a9497-126">Click hello **Schedule** tab.</span></span>

    ![Creazione un criterio - scheda Pianificazione](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="a9497-128">In hello **pianificazione** scheda, hello completa le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="a9497-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="a9497-129">Fare clic su hello **abilitare** backup successivo hello tooschedule di casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="a9497-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="a9497-130">In **Impostazioni** selezionare **Una sola volta**, **Giornaliera**, **Settimanale** o **Mensile**.</span><span class="sxs-lookup"><span data-stu-id="a9497-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="a9497-131">In hello **avviare** casella di testo, fare clic sull'icona calendario hello e selezionare una data di inizio.</span><span class="sxs-lookup"><span data-stu-id="a9497-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="a9497-132">In **Impostazioni avanzate**, è possibile impostare pianificazioni ripetute facoltative e una data di fine.</span><span class="sxs-lookup"><span data-stu-id="a9497-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="a9497-133">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9497-133">Click **OK**.</span></span>

<span data-ttu-id="a9497-134">Dopo aver creato un criterio di backup, le seguenti informazioni hello viene visualizzato in hello **risultati** riquadro:</span><span class="sxs-lookup"><span data-stu-id="a9497-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="a9497-135">**Nome** : hello nome del criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="a9497-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="a9497-136">**Tipo** : snapshot locale o cloud.</span><span class="sxs-lookup"><span data-stu-id="a9497-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="a9497-137">**Gruppo di volumi** : hello gruppo di volumi associato criteri hello.</span><span class="sxs-lookup"><span data-stu-id="a9497-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="a9497-138">**Conservazione** : hello mantenuto il numero di snapshot; hello massimo è 64.</span><span class="sxs-lookup"><span data-stu-id="a9497-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="a9497-139">**Creato** – data hello che è stato creato questo criterio.</span><span class="sxs-lookup"><span data-stu-id="a9497-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="a9497-140">**Abilitato** : indica se i criteri di hello sono attualmente attivo: **True** indica che è attivo; **False** indica che non è attivo.</span><span class="sxs-lookup"><span data-stu-id="a9497-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="a9497-141">Modifica di un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-141">Edit a backup policy</span></span>
<span data-ttu-id="a9497-142">Utilizzare hello seguendo procedure tooedit un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="a9497-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="a9497-143">tooedit un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="a9497-144">Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a9497-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a9497-145">In hello **ambito** riquadro, fare clic su hello **criteri di Backup** nodo.</span><span class="sxs-lookup"><span data-stu-id="a9497-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="a9497-146">Vengono visualizzati tutti i criteri di backup hello in hello **risultati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="a9497-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="a9497-147">Mouse hello criterio che desidera tooedit e quindi fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="a9497-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![Modifica di un criterio di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="a9497-149">Quando hello **creare un criterio** verrà visualizzata la finestra, immettere le modifiche e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9497-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="a9497-150">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-150">Delete a backup policy</span></span>
<span data-ttu-id="a9497-151">Utilizzare hello seguendo procedure toodelete un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="a9497-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="a9497-152">toodelete un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="a9497-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="a9497-153">Fare clic su hello icona sul desktop toostart gestione Snapshot StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a9497-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a9497-154">In hello **ambito** riquadro, fare clic su hello **criteri di Backup** nodo.</span><span class="sxs-lookup"><span data-stu-id="a9497-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="a9497-155">Vengono visualizzati tutti i criteri di backup hello in hello **risultati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="a9497-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="a9497-156">Fare doppio clic su hello dei criteri di backup che desidera toodelete e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="a9497-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="a9497-157">Quando viene visualizzato il messaggio di conferma di hello, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="a9497-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![Eliminazione della conferma dei criteri di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="a9497-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9497-159">Next steps</span></span>
* <span data-ttu-id="a9497-160">Informazioni su come troppo[usare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a9497-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="a9497-161">Informazioni su come troppo[tooview StorSimple Snapshot Manager di utilizzare e gestire i processi di backup](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a9497-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
