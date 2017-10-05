---
title: StorSimple Snapshot Manager gruppi di volume | Microsoft Docs
description: Viene descritto come utilizzare lo snap-in MMC StorSimple Snapshot Manager per creare e gestire i gruppi di volumi.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 6067a88cd42d29c3d2f4b74580095424de77561e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-volume-groups"></a><span data-ttu-id="59b2f-103">Usare StorSimple Snapshot Manager per creare e gestire gruppi di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-103">Use StorSimple Snapshot Manager to create and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="59b2f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="59b2f-104">Overview</span></span>
<span data-ttu-id="59b2f-105">È possibile usare il nodo **Gruppi di volumi** nel riquadro **Ambito** per assegnare i volumi a gruppi di volumi, visualizzare le informazioni relative a un gruppo di volumi, pianificare i backup e modificare i gruppi di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-105">You can use the **Volume Groups** node on the **Scope** pane to assign volumes to volume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="59b2f-106">I gruppi di volumi sono pool di volumi correlati utilizzati per garantire che i backup siano coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="59b2f-106">Volume groups are pools of related volumes used to ensure that backups are application-consistent.</span></span> <span data-ttu-id="59b2f-107">Per altre informazioni, vedere [Volumi e gruppi di volumi](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) e [Integrazione con il servizio Copia Shadow del volume di Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="59b2f-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="59b2f-108">Tutti i volumi in un gruppo di volumi devono provenire da un singolo provider di servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="59b2f-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="59b2f-109">Quando si configurano gruppi di volumi, non combinare volumi condivisi cluster (CSV) e volumi non condivisi cluster nello stesso gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="59b2f-110">StorSimple Snapshot Manager non supporta una combinazione di volumi condivisi cluster e volumi non condivisi cluster nello stesso snapshot.</span><span class="sxs-lookup"><span data-stu-id="59b2f-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in the same snapshot.</span></span>

![Nodo Gruppi di volumi](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="59b2f-112">**Figura 1: Nodo Gruppi di volumi di StorSimple Snapshot Manager**</span><span class="sxs-lookup"><span data-stu-id="59b2f-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="59b2f-113">Questa esercitazione illustra come usare StorSimple Snapshot Manager per:</span><span class="sxs-lookup"><span data-stu-id="59b2f-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="59b2f-114">Visualizzare le informazioni sui gruppi di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-114">View information about your volume groups</span></span>
* <span data-ttu-id="59b2f-115">Creare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-115">Create a volume group</span></span>
* <span data-ttu-id="59b2f-116">Eseguire il backup di un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-116">Back up a volume group</span></span>
* <span data-ttu-id="59b2f-117">Modificare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-117">Edit a volume group</span></span>
* <span data-ttu-id="59b2f-118">Eliminare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-118">Delete a volume group</span></span>

<span data-ttu-id="59b2f-119">Tutte queste azioni sono disponibili anche nel riquadro **Azioni** .</span><span class="sxs-lookup"><span data-stu-id="59b2f-119">All of these actions are also available on the **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="59b2f-120">Visualizzazione dei gruppi di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-120">View volume groups</span></span>
<span data-ttu-id="59b2f-121">Se si fa clic sul nodo **Gruppi di volumi**, nel riquadro **Risultati** vengono mostrate le informazioni seguenti su ciascun gruppo di volumi, a seconda delle colonne selezionate.</span><span class="sxs-lookup"><span data-stu-id="59b2f-121">If you click the **Volume Groups** node, the **Results** pane shows the following information about each volume group, depending on the column selections you make.</span></span> <span data-ttu-id="59b2f-122">Le colonne nel riquadro **Risultati** sono configurabili.</span><span class="sxs-lookup"><span data-stu-id="59b2f-122">(The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="59b2f-123">Fare clic con il pulsante destro del mouse sul nodo **Volumi**, selezionare **Visualizza**, quindi scegliere **Aggiungi/Rimuovi colonne**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-123">Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="59b2f-124">Colonna risultati</span><span class="sxs-lookup"><span data-stu-id="59b2f-124">Results column</span></span> | <span data-ttu-id="59b2f-125">Descrizione</span><span class="sxs-lookup"><span data-stu-id="59b2f-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="59b2f-126">Nome</span><span class="sxs-lookup"><span data-stu-id="59b2f-126">Name</span></span> |<span data-ttu-id="59b2f-127">La colonna **Nome** contiene il nome del gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-127">The **Name** column contains the name of the volume group.</span></span> |
| <span data-ttu-id="59b2f-128">Applicazione</span><span class="sxs-lookup"><span data-stu-id="59b2f-128">Application</span></span> |<span data-ttu-id="59b2f-129">La colonna **Applicazioni** mostra il numero di writer del Servizio snapshot del volume attualmente installati e in esecuzione sull'host Windows.</span><span class="sxs-lookup"><span data-stu-id="59b2f-129">The **Applications** column shows the number of VSS writers currently installed and running on the Windows host.</span></span> |
| <span data-ttu-id="59b2f-130">Selezionato</span><span class="sxs-lookup"><span data-stu-id="59b2f-130">Selected</span></span> |<span data-ttu-id="59b2f-131">La colonna **Selezionati** mostra il numero di volumi contenuti nel gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-131">The **Selected** column shows the number of volumes that are contained in the volume group.</span></span> <span data-ttu-id="59b2f-132">Zero (0) indica che nessuna applicazione è associata ai volumi nel gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-132">A zero (0) indicates that no application is associated with the volumes in the volume group.</span></span> |
| <span data-ttu-id="59b2f-133">Importati</span><span class="sxs-lookup"><span data-stu-id="59b2f-133">Imported</span></span> |<span data-ttu-id="59b2f-134">La colonna **Importati** mostra il numero di volumi importati.</span><span class="sxs-lookup"><span data-stu-id="59b2f-134">The **Imported** column shows the number of imported volumes.</span></span> <span data-ttu-id="59b2f-135">Se impostata su **True**, questa colonna indica che un gruppo di volumi è stato importato dal portale di Azure e non è stato creato in StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="59b2f-135">When set to **True**, this column indicates that a volume group was imported from the Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="59b2f-136">I gruppi di volumi di StorSimple Snapshot Manager vengono inoltre visualizzati nella scheda **Criteri di backup** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="59b2f-136">StorSimple Snapshot Manager volume groups are also displayed on the **Backup Policies** tab in the Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="59b2f-137">Creare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-137">Create a volume group</span></span>
<span data-ttu-id="59b2f-138">Utilizzare la procedura seguente per creare un gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-138">Use the following procedure to create a volume group.</span></span>

#### <a name="to-create-a-volume-group"></a><span data-ttu-id="59b2f-139">Per creare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-139">To create a volume group</span></span>
1. <span data-ttu-id="59b2f-140">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="59b2f-140">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="59b2f-141">Nel riquadro **Ambito** fare clic con il pulsante destro del mouse su **Gruppi di volumi**, quindi fare clic su **Crea gruppo di volumi**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-141">In the **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![Crea gruppo di volumi](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="59b2f-143">Viene visualizzata la finestra di dialogo **Crea un gruppo di volumi** .</span><span class="sxs-lookup"><span data-stu-id="59b2f-143">The **Create a volume group** dialog box appears.</span></span>
   
    ![Finestra di dialogo Crea un gruppo di volumi](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="59b2f-145">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="59b2f-145">Enter the following information:</span></span>
   
   1. <span data-ttu-id="59b2f-146">Nella casella **Nome** digitare un nome univoco per il nuovo gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-146">In the **Name** box, type a unique name for the new volume group.</span></span>
   2. <span data-ttu-id="59b2f-147">Nella casella **Applicazioni** selezionare le applicazioni associate ai volumi che verranno aggiunte al gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-147">In the **Applications** box, select applications associated with the volumes that you will be adding to the volume group.</span></span>
      
       <span data-ttu-id="59b2f-148">Nella casella **Applicazioni** vengono elencate solo le applicazioni che usano volumi StorSimple e per le quali è abilitato il componente VSS writer.</span><span class="sxs-lookup"><span data-stu-id="59b2f-148">The **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="59b2f-149">VSS writer è abilitato solo se tutti i volumi di cui è a conoscenza sono volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="59b2f-149">A VSS writer is enabled only if all the volumes that the writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="59b2f-150">Se la casella Applicazioni è vuota, non è stata installata alcuna applicazione che utilizza volumi StorSimple di Azure e che dispone di writer del Servizio snapshot del volume.</span><span class="sxs-lookup"><span data-stu-id="59b2f-150">If the Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="59b2f-151">(Attualmente, Azure StorSimple supporta Microsoft Exchange e SQL Server). Per altre informazioni sui writer del Servizio snapshot del volume, vedere [Integrazione con il servizio Copia Shadow del volume di Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="59b2f-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="59b2f-152">Se si seleziona un'applicazione, vengono selezionati automaticamente tutti i volumi associati ad essa.</span><span class="sxs-lookup"><span data-stu-id="59b2f-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="59b2f-153">Viceversa, se si selezionano i volumi associati a un'applicazione specifica, l'applicazione viene automaticamente selezionata nella casella **Applicazioni** .</span><span class="sxs-lookup"><span data-stu-id="59b2f-153">Conversely, if you select volumes associated with a specific application, the application is automatically selected in the **Applications** box.</span></span> 
   3. <span data-ttu-id="59b2f-154">Nella casella **Volumi** selezionare i volumi StorSimple da aggiungere al gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-154">In the **Volumes** box, select StorSimple volumes to add to the volume group.</span></span> 
      
      * <span data-ttu-id="59b2f-155">È possibile includere volumi con una o più partizioni.</span><span class="sxs-lookup"><span data-stu-id="59b2f-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="59b2f-156">(I volumi con più partizioni possono essere dischi dinamici o dischi di base con più partizioni.) Un volume che contiene più partizioni viene considerato come una singola unità.</span><span class="sxs-lookup"><span data-stu-id="59b2f-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="59b2f-157">Di conseguenza, se si aggiunge solo una delle partizioni a un gruppo di volumi, tutte le altre partizioni vengono automaticamente aggiunte a tale gruppo contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="59b2f-157">Consequently, if you add only one of the partitions to a volume group, all the other partitions are automatically added to that volume group at the same time.</span></span> <span data-ttu-id="59b2f-158">Dopo aver aggiunto un volume con più partizioni a un gruppo di volumi, il volume con più partizioni continua a essere considerato come una singola unità.</span><span class="sxs-lookup"><span data-stu-id="59b2f-158">After you add a multiple partition volume to a volume group, the multiple partition volume continues to be treated as a single unit.</span></span>
      * <span data-ttu-id="59b2f-159">È possibile creare gruppi di volumi vuoti non assegnando alcun volume a essi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-159">You can create empty volume groups by not assigning any volumes to them.</span></span> 
      * <span data-ttu-id="59b2f-160">Non combinare volumi condivisi cluster (CSV) e volumi non condivisi cluster nello stesso gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="59b2f-161">StorSimple Snapshot Manager non supporta una combinazione di volumi condivisi cluster e volumi non condivisi cluster nello stesso snapshot.</span><span class="sxs-lookup"><span data-stu-id="59b2f-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in the same snapshot.</span></span>
4. <span data-ttu-id="59b2f-162">Fare clic su **OK** per salvare il gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-162">Click **OK** to save the volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="59b2f-163">Eseguire il backup di un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-163">Back up a volume group</span></span>
<span data-ttu-id="59b2f-164">Utilizzare la procedura seguente per eseguire il backup di un gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-164">Use the following procedure to back up a volume group.</span></span>

#### <a name="to-back-up-a-volume-group"></a><span data-ttu-id="59b2f-165">Per eseguire il backup di un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-165">To back up a volume group</span></span>
1. <span data-ttu-id="59b2f-166">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="59b2f-166">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="59b2f-167">Nel riquadro **Ambito** espandere il nodo **Gruppi di volumi**, fare clic con il pulsante destro del mouse sul nome di un gruppo di volumi, quindi fare clic su **Esegui backup**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-167">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![Esecuzione immediata del backup del gruppo di volumi](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="59b2f-169">Nella finestra di dialogo **Esegui backup** selezionare **Snapshot locale** o **Snapshot cloud**, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-169">In the **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![Finestra di dialogo Esegui backup](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="59b2f-171">Per verificare che il backup sia in esecuzione, espandere il nodo **Processi**, quindi fare clic su **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-171">To confirm that the backup is running, expand the **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="59b2f-172">Il backup dovrebbe essere elencato.</span><span class="sxs-lookup"><span data-stu-id="59b2f-172">The backup should be listed.</span></span>
5. <span data-ttu-id="59b2f-173">Per visualizzare lo snapshot completato, espandere il nodo **Catalogo di backup**, espandere il nome del gruppo di volumi, quindi fare clic su **Snapshot locale** o **Snapshot cloud**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-173">To view the completed snapshot, expand the **Backup Catalog** node, expand the volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="59b2f-174">Il backup verrà elencato se è stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="59b2f-174">The backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="59b2f-175">Modificare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-175">Edit a volume group</span></span>
<span data-ttu-id="59b2f-176">Utilizzare la procedura seguente per modificare un gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-176">Use the following procedure to edit a volume group.</span></span>

#### <a name="to-edit-a-volume-group"></a><span data-ttu-id="59b2f-177">Per modificare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-177">To edit a volume group</span></span>
1. <span data-ttu-id="59b2f-178">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="59b2f-178">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="59b2f-179">Nel riquadro **Ambito** espandere il nodo **Gruppi di volumi**, fare clic con il pulsante destro del mouse sul nome di un gruppo di volumi, quindi fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-179">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="59b2f-180">Viene visualizzata la finestra di dialogo **Crea un gruppo di volumi**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-180">The **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="59b2f-181">È possibile modificare le voci **Nome**, **Applicazioni** e **Volumi**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-181">You can change the **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="59b2f-182">Fare clic su **OK** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="59b2f-182">Click **OK** to save your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="59b2f-183">Eliminare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-183">Delete a volume group</span></span>
<span data-ttu-id="59b2f-184">Utilizzare la procedura seguente per eliminare un gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-184">Use the following procedure to delete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="59b2f-185">Vengono eliminati anche tutti i backup associati al gruppo di volumi.</span><span class="sxs-lookup"><span data-stu-id="59b2f-185">This also deletes all the backups associated with the volume group.</span></span>
> 
> 

#### <a name="to-delete-a-volume-group"></a><span data-ttu-id="59b2f-186">Per eliminare un gruppo di volumi</span><span class="sxs-lookup"><span data-stu-id="59b2f-186">To delete a volume group</span></span>
1. <span data-ttu-id="59b2f-187">Fare clic sull’icona del desktop per avviare StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="59b2f-187">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="59b2f-188">Nel riquadro **Ambito** espandere il nodo **Gruppi di volumi**, fare clic con il pulsante destro del mouse sul nome di un gruppo di volumi, quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-188">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="59b2f-189">Viene visualizzata la finestra di dialogo **Elimina un gruppo di volumi** .</span><span class="sxs-lookup"><span data-stu-id="59b2f-189">The **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="59b2f-190">Digitare **Conferma** nella casella di testo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="59b2f-190">Type **Confirm** in the text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="59b2f-191">Il gruppo di volumi eliminato non è più presente nell'elenco del riquadro **Risultati** e tutti i backup associati a tale gruppo vengono eliminati dal catalogo di backup.</span><span class="sxs-lookup"><span data-stu-id="59b2f-191">The deleted volume group vanishes from the list in the **Results** pane and all backups that are associated with that volume group are deleted from the backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59b2f-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59b2f-192">Next steps</span></span>
* <span data-ttu-id="59b2f-193">Informazioni su come [usare StorSimple Snapshot Manager per amministrare la soluzione di StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="59b2f-193">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="59b2f-194">Informazioni su come [usare StorSimple Snapshot Manager per creare e gestire criteri di backup](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="59b2f-194">Learn how to [use StorSimple Snapshot Manager to create and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

