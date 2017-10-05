---
title: Criteri di backup di StorSimple Snapshot Manager | Microsoft Docs
description: Viene descritto come utilizzare lo snap-in MMC di Gestione snapshot StorSimple per creare e gestire i criteri di backup che consentono di controllare i backup pianificati.
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
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a><span data-ttu-id="0d6f4-103">Utilizzo di Gestione snapshot StorSimple per creare e gestire i criteri di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-103">Use StorSimple Snapshot Manager to create and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="0d6f4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0d6f4-104">Overview</span></span>
<span data-ttu-id="0d6f4-105">Un criterio di backup consente di creare una pianificazione di backup dei dati del volume in locale o nel cloud.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span></span> <span data-ttu-id="0d6f4-106">Quando si crea un criterio di backup, è inoltre possibile specificare un criterio di conservazione.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="0d6f4-107">(È possibile conservare un massimo di 64 snapshot). Per altre informazioni sui criteri di backup, vedere [Tipi di backup](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) nell'articolo relativo a [StorSimple serie 8000: una soluzione cloud ibrida](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d6f4-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="0d6f4-108">In questa esercitazione viene illustrato come:</span><span class="sxs-lookup"><span data-stu-id="0d6f4-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="0d6f4-109">Creare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-109">Create a backup policy</span></span>
* <span data-ttu-id="0d6f4-110">Modifica di un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-110">Edit a backup policy</span></span>
* <span data-ttu-id="0d6f4-111">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="0d6f4-112">Creare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-112">Create a backup policy</span></span>
<span data-ttu-id="0d6f4-113">Utilizzare la procedura seguente per creare un nuovo criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-113">Use the following procedure to create a new backup policy.</span></span>

#### <a name="to-create-a-backup-policy"></a><span data-ttu-id="0d6f4-114">Per creare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-114">To create a backup policy</span></span>
1. <span data-ttu-id="0d6f4-115">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-115">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="0d6f4-116">Nel riquadro **Ambito** fare clic con il pulsante destro del mouse su **Criteri di backup**, quindi fare clic su **Crea criteri di backup**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Creare un criterio di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="0d6f4-118">Viene visualizzata la finestra di dialogo **Crea un criterio** .</span><span class="sxs-lookup"><span data-stu-id="0d6f4-118">The **Create a Policy** dialog box appears.</span></span>

    ![Creazione di un criterio - scheda Generale](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="0d6f4-120">Nella scheda **Generale** , completare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d6f4-120">On the **General** tab, complete the following information:</span></span>

   1. <span data-ttu-id="0d6f4-121">Nella casella di testo **Nome** , digitare un nome per il criterio.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-121">In the **Name** text box, type a name for the policy.</span></span>
   2. <span data-ttu-id="0d6f4-122">Nella casella di testo **Gruppo di volumi** digitare il nome del gruppo di volumi associati ai criteri.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span></span>
   3. <span data-ttu-id="0d6f4-123">Selezionare **Snapshot locale** o **Snapshot cloud**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="0d6f4-124">Selezionare il numero di snapshot da conservare.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-124">Select the number of snapshots to retain.</span></span> <span data-ttu-id="0d6f4-125">Se si seleziona **Tutti**, verranno conservati 64 snapshot (il massimo).</span><span class="sxs-lookup"><span data-stu-id="0d6f4-125">If you select **All**, 64 snapshots will be retained (the maximum).</span></span>
4. <span data-ttu-id="0d6f4-126">Fare clic sulla scheda **Pianificazione** .</span><span class="sxs-lookup"><span data-stu-id="0d6f4-126">Click the **Schedule** tab.</span></span>

    ![Creazione un criterio - scheda Pianificazione](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="0d6f4-128">Nella scheda **Pianificazione** , completare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d6f4-128">On the **Schedule** tab, complete the following information:</span></span>

   1. <span data-ttu-id="0d6f4-129">Fare clic sulla casella di controllo **Abilita** per pianificare il backup successivo.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-129">Click the **Enable** check box to schedule the next backup.</span></span>
   2. <span data-ttu-id="0d6f4-130">In **Impostazioni** selezionare **Una sola volta**, **Giornaliera**, **Settimanale** o **Mensile**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="0d6f4-131">Nella casella di controllo **Avvio** , fare clic sull'icona del calendario e selezionare una data di avvio.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-131">In the **Start** text box, click the calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="0d6f4-132">In **Impostazioni avanzate**, è possibile impostare pianificazioni ripetute facoltative e una data di fine.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="0d6f4-133">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-133">Click **OK**.</span></span>

<span data-ttu-id="0d6f4-134">Dopo aver creato un criterio di backup, nel riquadro **Risultati** vengono visualizzate le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0d6f4-134">After you create a backup policy, the following information appears in the **Results** pane:</span></span>

* <span data-ttu-id="0d6f4-135">**Nome** : il nome del criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-135">**Name** – the name of backup policy.</span></span>
* <span data-ttu-id="0d6f4-136">**Tipo** : snapshot locale o cloud.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="0d6f4-137">**Gruppo di volumi** : il gruppo di volumi associato al criterio.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-137">**Volume Group** – the volume group associated with the policy.</span></span>
* <span data-ttu-id="0d6f4-138">**Conservazione** : il numero di snapshot conservati (il massimo è 64).</span><span class="sxs-lookup"><span data-stu-id="0d6f4-138">**Retention** – the number of snapshots retained; the maximum is 64.</span></span>
* <span data-ttu-id="0d6f4-139">**Creato** : la data in cui è stato creato questo criterio.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-139">**Created** – the date that this policy was created.</span></span>
* <span data-ttu-id="0d6f4-140">**Abilitato**: se il criterio è attualmente attivo (**True** indica che è attivo, **False** indica che non è attivo).</span><span class="sxs-lookup"><span data-stu-id="0d6f4-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="0d6f4-141">Modifica di un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-141">Edit a backup policy</span></span>
<span data-ttu-id="0d6f4-142">Utilizzare la procedura seguente per modificare un criterio di backup esistente.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-142">Use the following procedure to edit an existing backup policy.</span></span>

#### <a name="to-edit-a-backup-policy"></a><span data-ttu-id="0d6f4-143">Per modificare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-143">To edit a backup policy</span></span>
1. <span data-ttu-id="0d6f4-144">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-144">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="0d6f4-145">Nel riquadro **Ambito** fare clic sul nodo **Criteri di backup**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-145">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="0d6f4-146">Nel riquadro **Risultati** vengono visualizzati tutti i criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-146">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="0d6f4-147">Fare clic con il pulsante destro del mouse sul criterio che si desidera modificare, quindi fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-147">Right-click the policy that you want to edit, and then click **Edit**.</span></span>

    ![Modifica di un criterio di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="0d6f4-149">Quando viene visualizzata la finestra **Crea un criterio**, apportare le modifiche, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="0d6f4-150">Eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-150">Delete a backup policy</span></span>
<span data-ttu-id="0d6f4-151">Utilizzare la procedura seguente per eliminare un criterio di backup.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-151">Use the following procedure to delete a backup policy.</span></span>

#### <a name="to-delete-a-backup-policy"></a><span data-ttu-id="0d6f4-152">Per eliminare un criterio di backup</span><span class="sxs-lookup"><span data-stu-id="0d6f4-152">To delete a backup policy</span></span>
1. <span data-ttu-id="0d6f4-153">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="0d6f4-154">Nel riquadro **Ambito** fare clic sul nodo **Criteri di backup**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-154">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="0d6f4-155">Nel riquadro **Risultati** vengono visualizzati tutti i criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-155">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="0d6f4-156">Fare clic con il pulsante destro del mouse sui criteri di backup da eliminare e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span></span>
4. <span data-ttu-id="0d6f4-157">Quando viene visualizzato il messaggio di conferma, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="0d6f4-157">When the confirmation message appears, click **Yes**.</span></span>

    ![Eliminazione della conferma dei criteri di backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="0d6f4-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d6f4-159">Next steps</span></span>
* <span data-ttu-id="0d6f4-160">Informazioni su come [Usare Gestione Snapshot StorSimple per amministrare la soluzione di StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="0d6f4-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="0d6f4-161">Informazioni su come [utilizzare Gestione snapshot StorSimple per visualizzare e gestire i processi di backup](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="0d6f4-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
