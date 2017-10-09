---
title: Server di Backup di Azure v2 aaaInstall | Documenti Microsoft
description: "Il server di Backup di Azure v2 offre funzionalità avanzate di backup per la protezione di VM, file e cartelle, carichi di lavoro e altro ancora. Informazioni su come tooAzure tooinstall o aggiornare il Server di Backup v2."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="04d33-104">Installare il server di Backup di Azure v2</span><span class="sxs-lookup"><span data-stu-id="04d33-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="04d33-105">Il server di Backup di Azure consente di proteggere macchine virtuali (VM), carichi di lavoro, file e cartelle, e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="04d33-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="04d33-106">Il server di Backup di Azure v2 si basa sul server di Backup di Azure v1 e offre nuove funzionalità che non sono disponibili nella v1.</span><span class="sxs-lookup"><span data-stu-id="04d33-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="04d33-107">Per un confronto delle funzionalità fra la v1 e la v2, vedere [Matrice di protezione del server di Backup di Azure](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="04d33-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="04d33-108">funzionalità aggiuntive di Hello v2 Server Backup sono un aggiornamento da Server di Backup v1.</span><span class="sxs-lookup"><span data-stu-id="04d33-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="04d33-109">Tuttavia, il server di backup v1 non è un prerequisito per l'installazione del server di backup v2.</span><span class="sxs-lookup"><span data-stu-id="04d33-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="04d33-110">Se si desidera tooupgrade dal Server di Backup v1 tooBackup v2 Server, installare v2 Server di Backup nel server di protezione hello Backup Server.</span><span class="sxs-lookup"><span data-stu-id="04d33-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="04d33-111">Le impostazioni del server di backup esistenti rimangono invariate.</span><span class="sxs-lookup"><span data-stu-id="04d33-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="04d33-112">È possibile installare il server di backup v2 in Windows Server 2012 R2 o in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="04d33-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="04d33-113">tootake le nuove funzionalità quali la archiviazione System Center 2016 Data Protection Manager moderno Backup, è necessario installare il Server di Backup v2 in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="04d33-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="04d33-114">Prima di aggiornare tooor install v2 Backup Server, informazioni hello [prerequisiti di installazione](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="04d33-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="04d33-115">Server di Backup di Azure è hello stessa codebase come System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="04d33-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="04d33-116">Backup Server v1 è equivalente tooData Protection Manager 2012 R2 e v2 Server Backup è equivalente tooData Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="04d33-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="04d33-117">In questo articolo fa riferimento in alcuni casi la documentazione di Data Protection Manager hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="04d33-118">Aggiornamento Server di Backup toov2</span><span class="sxs-lookup"><span data-stu-id="04d33-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="04d33-119">tooupgrade dal Server di Backup v1 tooBackup v2 Server, assicurarsi che l'installazione contenga gli aggiornamenti necessario hello:</span><span class="sxs-lookup"><span data-stu-id="04d33-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="04d33-120">[Aggiornare gli agenti protezione hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) su hello server protetti.</span><span class="sxs-lookup"><span data-stu-id="04d33-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="04d33-121">Eseguire l'aggiornamento di Windows Server 2012 R2 tooWindows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="04d33-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="04d33-122">Aggiornare Azure Backup Server Remote Administrator in tutti i server di produzione.</span><span class="sxs-lookup"><span data-stu-id="04d33-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="04d33-123">Verificare che i backup sono impostati toocontinue senza dover riavviare il server di produzione.</span><span class="sxs-lookup"><span data-stu-id="04d33-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="04d33-124">Passaggi di aggiornamento per il server di backup v2</span><span class="sxs-lookup"><span data-stu-id="04d33-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="04d33-125">Nell'area Download, hello [scaricare installazione guidata di aggiornamento hello](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="04d33-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="04d33-126">Dopo l'installazione guidata di hello estrazione, assicurarsi che **eseguire setup.exe** è selezionata, quindi fare clic **fine**.</span><span class="sxs-lookup"><span data-stu-id="04d33-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Programma di installazione - Eseguire il programma di installazione](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="04d33-128">Nella procedura guidata di Microsoft Azure Backup Server hello, in **installare**selezionare **il Server di Backup di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="04d33-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Programma di installazione - Selezionare cosa installare](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="04d33-130">In hello **iniziale** pagina, rivedere gli avvisi di hello e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![Programma di installazione - Pagina di benvenuto](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="04d33-132">installazione guidata di Hello esegue controlli dei prerequisiti toomake che può aggiornare l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="04d33-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="04d33-133">In hello **Prerequisite Checks** selezionare **controllare**.</span><span class="sxs-lookup"><span data-stu-id="04d33-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![Programma di installazione - Pagina del controllo dei prerequisiti](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="04d33-135">L'ambiente deve superare i controlli dei prerequisiti hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="04d33-136">Se l'ambiente non superano i controlli di hello, tenere presente hello e correggerli.</span><span class="sxs-lookup"><span data-stu-id="04d33-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="04d33-137">Selezionare quindi **Controlla di nuovo**.</span><span class="sxs-lookup"><span data-stu-id="04d33-137">Then, select **Check Again**.</span></span> <span data-ttu-id="04d33-138">Dopo avere passato i controlli dei prerequisiti hello, selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![Programma di installazione - Pulsante per ripetere il controllo](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="04d33-140">In hello **impostazioni SQL** pagina, l'opzione hello rilevanti per l'installazione di SQL e quindi selezionare **controlla e installa**.</span><span class="sxs-lookup"><span data-stu-id="04d33-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Programma di installazione - Pagina delle impostazioni di SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="04d33-142">controlli Hello potrebbero richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="04d33-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="04d33-143">Quando i controlli di hello sono finiti, selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-143">When hello checks are finished, select **Next**.</span></span>

  ![Programma di installazione - Controllo delle impostazioni di SQL e pulsante di installazione](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="04d33-145">In hello **le impostazioni di installazione** pagina di qualsiasi percorso toohello modifiche in cui è installato il Server di Backup, o toohello percorso dei file temporanei.</span><span class="sxs-lookup"><span data-stu-id="04d33-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="04d33-146">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-146">Select **Next**.</span></span>

  ![Programma di installazione - Pagina delle impostazioni di installazione](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="04d33-148">toofinish hello installazione guidata selezionare **fine**.</span><span class="sxs-lookup"><span data-stu-id="04d33-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![Programma di installazione - Fine](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="04d33-150">Aggiungere spazio di archiviazione per Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="04d33-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="04d33-151">l'efficienza di archiviazione di backup tooimprove, v2 Server di Backup aggiunge supporto per i volumi.</span><span class="sxs-lookup"><span data-stu-id="04d33-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="04d33-152">Come il server di backup v1, la v2 supporta i dischi.</span><span class="sxs-lookup"><span data-stu-id="04d33-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="04d33-153">Aggiungere volumi e dischi</span><span class="sxs-lookup"><span data-stu-id="04d33-153">Add volumes and disks</span></span>
<span data-ttu-id="04d33-154">Se si eseguono Backup Server v2 in Windows Server 2016, è possibile utilizzare dati di backup di volumi toostore.</span><span class="sxs-lookup"><span data-stu-id="04d33-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="04d33-155">I volumi consentono di risparmiare spazio di archiviazione e offrono backup più veloci.</span><span class="sxs-lookup"><span data-stu-id="04d33-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="04d33-156">Poiché i volumi sono tooBackup nuovo Server, è necessario aggiungerli.</span><span class="sxs-lookup"><span data-stu-id="04d33-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="04d33-157">Quando si aggiunge un Server di tooBackup volume, è possibile assegnare un nome descrittivo volume hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="04d33-158">Fare clic su hello **nome descrittivo** colonna del volume hello desiderato tooname.</span><span class="sxs-lookup"><span data-stu-id="04d33-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="04d33-159">È possibile modificare il nome di hello in un secondo momento, se necessario.</span><span class="sxs-lookup"><span data-stu-id="04d33-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="04d33-160">È inoltre possibile utilizzare PowerShell tooadd o modificare i nomi descrittivi per i volumi.</span><span class="sxs-lookup"><span data-stu-id="04d33-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="04d33-161">un volume nella Console di amministrazione di hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="04d33-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="04d33-162">Nella Console di amministrazione di Server di Backup di Azure hello, selezionare **Management** > **archiviazione su disco** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="04d33-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Procedura guidata Aggiungi archiviazione su disco hello aperto](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="04d33-164">Verrà visualizzata una procedura guidata Aggiungi archiviazione su disco hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="04d33-165">In hello **aggiungere archiviazione su disco** pagina hello **volumi disponibili** , selezionare un volume e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="04d33-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="04d33-166">In hello **selezionato volumi** , immettere un nome descrittivo per il volume di hello e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="04d33-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![Procedura guidata Aggiungi spazio di archiviazione su disco - Aggiungi volume](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="04d33-168">Se si desidera tooadd un disco, disco hello deve appartenere a gruppo protezione dati tooa legacy di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="04d33-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="04d33-169">Tali dischi possono essere usati solo per questi gruppi protezione dati.</span><span class="sxs-lookup"><span data-stu-id="04d33-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="04d33-170">Se Backup Server non dispone di origini che hanno la protezione legacy, non è elencato disco hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="04d33-171">Per ulteriori informazioni sull'aggiunta di dischi, vedere [aggiungere dischi di archiviazione legacy tooincrease](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="04d33-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="04d33-172">È possibile assegnare un nome descrittivo al disco.</span><span class="sxs-lookup"><span data-stu-id="04d33-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="04d33-173">Assegnare i carichi di lavoro toovolumes</span><span class="sxs-lookup"><span data-stu-id="04d33-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="04d33-174">Nel Server di Backup, specificare carichi di lavoro assegnati toowhich volumi.</span><span class="sxs-lookup"><span data-stu-id="04d33-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="04d33-175">Ad esempio, è possibile impostare costosa volumi che supportano un numero elevato di operazioni di input/output al secondo (IOPS) toostore soli i carichi di lavoro che richiedono frequenti backup volumi elevati.</span><span class="sxs-lookup"><span data-stu-id="04d33-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="04d33-176">Un esempio è SQL Server con i log delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="04d33-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="04d33-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="04d33-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="04d33-178">proprietà hello tooupdate volume nel pool di archiviazione hello nel Server di Backup, utilizzare il cmdlet di PowerShell hello DPMDiskStorage di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="04d33-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="04d33-179">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="04d33-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="04d33-180">Tutte le modifiche apportate tramite PowerShell vengono riflesse in hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="04d33-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="04d33-181">Proteggere le origini dati</span><span class="sxs-lookup"><span data-stu-id="04d33-181">Protect data sources</span></span>
<span data-ttu-id="04d33-182">toobegin proteggono le origini dati, creare un gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="04d33-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="04d33-183">Hello seguendo i passaggi evidenziazione modifiche o aggiunte toohello nuovo guidata gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="04d33-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="04d33-184">toocreate un gruppo protezione dati:</span><span class="sxs-lookup"><span data-stu-id="04d33-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="04d33-185">Nella Console di amministrazione di Server di Backup hello, selezionare **protezione**.</span><span class="sxs-lookup"><span data-stu-id="04d33-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="04d33-186">Sulla barra multifunzione dello strumento di hello, selezionare **New**.</span><span class="sxs-lookup"><span data-stu-id="04d33-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="04d33-187">Verrà visualizzata una procedura guidata Crea nuovo gruppo protezione dati hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-187">This opens hello Create New Protection Group wizard.</span></span>

  ![Procedura guidata Crea nuovo gruppo protezione dati](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="04d33-189">In hello **iniziale** selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="04d33-190">In hello **Selezione tipo di gruppo protezione dati** pagina, selezionare il tipo di hello del gruppo protezione dati desiderato toocreate e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![Pagina Seleziona tipo di gruppo di protezione dati](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="04d33-192">In hello **Seleziona membri del gruppo** pagina hello **membri disponibili** riquadro, i membri di hello sono elencati gli agenti protezione.</span><span class="sxs-lookup"><span data-stu-id="04d33-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="04d33-193">Per questo esempio, selezionare il volume D:\ ed E:\ e li aggiunge toohello **i membri selezionati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="04d33-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="04d33-194">Selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-194">Select **Next**.</span></span>

  ![Pagina Seleziona membri del gruppo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="04d33-196">In hello **Selezione metodo protezione dati** pagina, immettere un **nome del gruppo protezione dati**, selezionare il metodo di protezione hello e quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="04d33-197">Se si desidera protezione a breve termine, è necessario selezionare hello **disco** metodo di backup.</span><span class="sxs-lookup"><span data-stu-id="04d33-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![Pagina Seleziona metodo protezione dati](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="04d33-199">In hello **Specifica obiettivi a breve termine** , hello selezionare i dettagli della pagina per **mantenimento** e **frequenza di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="04d33-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="04d33-200">Quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-200">Then, select **Next**.</span></span> <span data-ttu-id="04d33-201">Facoltativamente, toochange hello pianificazione quando i punti di ripristino vengono prelevati, selezionare **modifica**.</span><span class="sxs-lookup"><span data-stu-id="04d33-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Pagina Specifica obiettivi a breve termine](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="04d33-203">In hello **Verifica allocazione archiviazione dischi** pagina, esaminare i dettagli sulle origini dati hello è stata selezionata, le dimensioni e i valori per il provisioning di hello spazio toobe e hello volume di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="04d33-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![Pagina di verifica allocazione dell'archiviazione su disco](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="04d33-205">Volumi di archiviazione si basano sull'allocazione di volume del carico di lavoro hello (impostato tramite PowerShell) e hello spazio di archiviazione disponibile.</span><span class="sxs-lookup"><span data-stu-id="04d33-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="04d33-206">È possibile modificare i volumi di archiviazione hello selezionando altri volumi nel menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="04d33-207">Se si modifica il valore di hello per **archiviazione di destinazione**, hello valore per **archiviazione su disco disponibile** modificata in modo dinamico i valori tooreflect in **spazio** e **Underprovisioned spazio**.</span><span class="sxs-lookup"><span data-stu-id="04d33-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="04d33-208">Se le origini dati hello crescere come pianificato, hello valore per hello **Underprovisioned spazio** colonna **archiviazione su disco disponibile** riflette hello quantità di spazio di archiviazione aggiuntivo è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="04d33-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="04d33-209">Utilizzare questo piano toohelp valore le esigenze di archiviazione per i backup smooth.</span><span class="sxs-lookup"><span data-stu-id="04d33-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="04d33-210">Se il valore di hello è zero, non esistono alcun potenziali problemi di archiviazione in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="04d33-211">Se il valore di hello è un numero diverso da zero, non è sufficiente spazio di archiviazione allocato (basato su protezione hello e criteri di quelle dei dati dei membri protetti).</span><span class="sxs-lookup"><span data-stu-id="04d33-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![Spazio di archiviazione su disco sottoallocato](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="04d33-213">toofinish la creazione di una procedura guidata hello completo, gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="04d33-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="04d33-214">Eseguire la migrazione archiviazione legacy tooModern archiviazione dei Backup</span><span class="sxs-lookup"><span data-stu-id="04d33-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="04d33-215">Dopo aver aggiornato tooor install v2 Server Backup e hello aggiornamento del sistema operativo tooWindows Server 2016, aggiornare il toouse di gruppi protezione dati moderni archiviazione dei Backup.</span><span class="sxs-lookup"><span data-stu-id="04d33-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="04d33-216">Per impostazione predefinita, i gruppi protezione dati non vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="04d33-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="04d33-217">Continuano toofunction che sono stati inizialmente impostate.</span><span class="sxs-lookup"><span data-stu-id="04d33-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="04d33-218">L'aggiornamento di gruppi di protezione toouse moderna archiviazione dei Backup è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="04d33-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="04d33-219">gruppo di protezione dati hello tooupdate, arrestare la protezione di tutte le origini dati utilizzando hello opzione di mantenimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="04d33-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="04d33-220">Aggiungere quindi hello dati origini tooa nuovo gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="04d33-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="04d33-221">Nella Console di amministrazione di hello, selezionare hello **protezione** funzionalità.</span><span class="sxs-lookup"><span data-stu-id="04d33-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="04d33-222">In hello **membro del gruppo protezione dati** elenco, fare doppio clic su membro hello e quindi selezionare **Arresta protezione dati del membro**.</span><span class="sxs-lookup"><span data-stu-id="04d33-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![Arresto della protezione del membro](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="04d33-224">In hello **rimuovere dal gruppo** la finestra di dialogo, lo spazio su disco utilizzato hello di revisione e hello spazio disponibile per il pool di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="04d33-225">valore predefinito di Hello è tooleave hello punti di ripristino disco hello e consentire loro tooexpire per criteri di conservazione associati.</span><span class="sxs-lookup"><span data-stu-id="04d33-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="04d33-226">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="04d33-226">Click **OK**.</span></span>

  <span data-ttu-id="04d33-227">Se si desidera il pool di archiviazione disponibile toohello tooimmediately restituito hello utilizzato disco spazio, selezionare hello **Elimina replica su disco** dati di backup di casella di controllo toodelete hello (e i punti di ripristino) associata a tale membro.</span><span class="sxs-lookup"><span data-stu-id="04d33-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![Rimozione dalla finestra di dialogo del gruppo](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="04d33-229">Creare un gruppo protezione dati che usa Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="04d33-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="04d33-230">Includere origini dati hello non protetto.</span><span class="sxs-lookup"><span data-stu-id="04d33-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="04d33-231">Aggiungere spazio di archiviazione dischi tooincrease legacy</span><span class="sxs-lookup"><span data-stu-id="04d33-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="04d33-232">Se si desidera toouse archiviazione legacy con il Server di Backup, si potrebbe essere necessario archiviazione legacy di tooadd dischi tooincrease.</span><span class="sxs-lookup"><span data-stu-id="04d33-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="04d33-233">archiviazione su disco tooadd:</span><span class="sxs-lookup"><span data-stu-id="04d33-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="04d33-234">Nella Console di amministrazione di hello, selezionare **Management** > **archiviazione su disco** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="04d33-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Finestra di dialogo Aggiungi spazio di archiviazione su disco](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="04d33-236">In hello **aggiungere archiviazione su disco** finestra di dialogo Seleziona **aggiungere dischi**.</span><span class="sxs-lookup"><span data-stu-id="04d33-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="04d33-237">Nell'elenco di hello dei dischi disponibili, selezionare i dischi di hello da tooadd, selezionare **Aggiungi**, quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="04d33-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="04d33-238">Aggiornare l'agente protezione Data Protection Manager di hello</span><span class="sxs-lookup"><span data-stu-id="04d33-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="04d33-239">Backup Server Usa l'agente protezione di System Center Data Protection Manager hello per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="04d33-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="04d33-240">Se si sta aggiornando un agente protezione che non sia connessa toohello rete, è possibile utilizzare hello Console di amministrazione di Data Protection Manager toocomplete un aggiornamento dell'agente connesso.</span><span class="sxs-lookup"><span data-stu-id="04d33-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="04d33-241">È necessario aggiornare l'agente protezione hello in un ambiente di dominio non attivo.</span><span class="sxs-lookup"><span data-stu-id="04d33-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="04d33-242">Fino al computer client hello rete toohello connesso, Console di amministrazione di Data Protection Manager viene illustrato l'aggiornamento dell'agente protezione che hello hello è in sospeso.</span><span class="sxs-lookup"><span data-stu-id="04d33-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="04d33-243">Hello sezioni seguenti descrivono come tooupdate gli agenti di protezione per i computer client connessi e i computer client che non si è connessi.</span><span class="sxs-lookup"><span data-stu-id="04d33-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="04d33-244">Aggiornare un agente protezione per un computer client connesso</span><span class="sxs-lookup"><span data-stu-id="04d33-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="04d33-245">Nella Console di amministrazione di Server di Backup hello, selezionare **Management** > **agenti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="04d33-246">Nel riquadro di visualizzazione hello, selezionare i computer client hello per cui si desidera l'agente di protezione tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="04d33-247">Hello **aggiornamenti agente** colonna indica quando un aggiornamento dell'agente protezione è disponibile per ogni computer protetto.</span><span class="sxs-lookup"><span data-stu-id="04d33-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="04d33-248">In hello **azioni** riquadro, hello **aggiornamento** azione è disponibile solo quando è selezionato un computer protetto e sono disponibili aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="04d33-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="04d33-249">tooinstall aggiornare gli agenti protezione nei computer selezionato hello, hello **azioni** riquadro, selezionare **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="04d33-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="04d33-250">Aggiornare un agente protezione in un computer client non connesso</span><span class="sxs-lookup"><span data-stu-id="04d33-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="04d33-251">Nella Console di amministrazione di Server di Backup hello, selezionare **Management** > **agenti**.</span><span class="sxs-lookup"><span data-stu-id="04d33-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="04d33-252">Nel riquadro di visualizzazione hello, selezionare i computer client hello per cui si desidera l'agente di protezione tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="04d33-253">Hello **aggiornamenti agente** colonna indica quando un aggiornamento dell'agente protezione è disponibile per ogni computer protetto.</span><span class="sxs-lookup"><span data-stu-id="04d33-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="04d33-254">In hello **azioni** riquadro, hello **aggiornamento** azione non è disponibile quando si seleziona un computer protetto, a meno che non sono disponibili aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="04d33-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="04d33-255">tooinstall aggiornare gli agenti protezione nei computer hello selezionato, selezionare **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="04d33-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="04d33-256">Per un computer client che non è connesso rete toohello, fino al computer hello rete toohello connesso, hello **lo stato dell'agente** colonna viene visualizzato lo stato **aggiornamento in sospeso**.</span><span class="sxs-lookup"><span data-stu-id="04d33-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="04d33-257">Dopo che un computer client è connesso toohello dalla rete, hello **aggiornamenti agente** colonna per i computer client hello viene visualizzato lo stato **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="04d33-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="04d33-258">Spostare i gruppi protezione dati legacy da precedente e la nuova versione hello sincronizzazione con Azure</span><span class="sxs-lookup"><span data-stu-id="04d33-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="04d33-259">Una volta che vengono aggiornati sia il Server di Backup di Azure e hello del sistema operativo, si è pronti tooprotect nuove origini dati mediante spazio di memorizzazione Backup moderne.</span><span class="sxs-lookup"><span data-stu-id="04d33-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="04d33-260">Origini dati, tuttavia è già protetto continuerà toobe protette hello legacy modo come fossero nel Server di Backup di Azure, ma tutti nuovo gruppo protezione dati utilizzerà moderna archiviazione dei Backup.</span><span class="sxs-lookup"><span data-stu-id="04d33-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="04d33-261">I passaggi successivi sono origini dati toomigrate dalla modalità legacy protezione tooModern archiviazione di backup.</span><span class="sxs-lookup"><span data-stu-id="04d33-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="04d33-262">• Aggiungere hello nuovi volumi toohello pool di archiviazione DPM e assegnare i tag di origine di dati e i nomi descrittivi se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="04d33-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="04d33-263">• Per ogni origine dati che è in modalità legacy, arresta la protezione delle origini dati hello e "Mantieni dati protetti".</span><span class="sxs-lookup"><span data-stu-id="04d33-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="04d33-264">Questo permetterà il ripristino dei vecchi punti di recupero dopo la migrazione.</span><span class="sxs-lookup"><span data-stu-id="04d33-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="04d33-265">• Creare un nuovo gruppo protezione dati e selezionare le origini dati hello che sono toobe memorizzati nel nuovo formato.</span><span class="sxs-lookup"><span data-stu-id="04d33-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="04d33-266">• DPM eseguirà una copia della replica di archiviazione dei backup legacy hello in hello volume di archiviazione di Backup più recenti in locale.</span><span class="sxs-lookup"><span data-stu-id="04d33-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="04d33-267">Nota: questo verrà considerato un processo dell'operazione successiva al ripristino • Tutti i nuovi punti di sincronizzazione e recupero verranno quindi archiviati nell'archiviazione dei backup moderna.</span><span class="sxs-lookup"><span data-stu-id="04d33-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="04d33-268">• Vecchi punti di ripristino saranno eliminati che sono in scadenza e alla fine di liberare spazio su disco hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="04d33-269">• Dopo tutti i volumi legacy hello vengono eliminati dalla risorsa di archiviazione precedente hello, disco hello possono essere rimossi dal sistema di backup e hello Azure.</span><span class="sxs-lookup"><span data-stu-id="04d33-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="04d33-270">• Eseguire un backup di hello Azure DPMDB.</span><span class="sxs-lookup"><span data-stu-id="04d33-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="04d33-271">Parte 2:-elementi importanti > hello nuovo server dovrà essere toobe denominato stesso come server di Backup di Azure originale hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="04d33-272">Non è possibile modificare il nome di hello del server di backup Azure nuovo hello se si desidera toouse precedente pool di archiviazione e i punti di ripristino tooretain DPMDB - deve avere il backup di DPMDB sarà necessario ripristinare toobe</span><span class="sxs-lookup"><span data-stu-id="04d33-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="04d33-273">Arresto hello server di backup di Azure originale o portarlo off transito hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="04d33-274">Reimpostare l'account del computer hello in active directory.</span><span class="sxs-lookup"><span data-stu-id="04d33-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="04d33-275">Installare Server 2016 nel nuovo computer e il nome hello stesso nome di computer come server di Backup di Azure originale hello.</span><span class="sxs-lookup"><span data-stu-id="04d33-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="04d33-276">Creare un join hello dominio</span><span class="sxs-lookup"><span data-stu-id="04d33-276">Join hello Domain</span></span>
5) <span data-ttu-id="04d33-277">Installare il server di Backup di Azure V2 (spostare i dischi del pool di archiviazione DPM dal vecchio server ed eseguire l'importazione)</span><span class="sxs-lookup"><span data-stu-id="04d33-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="04d33-278">Ripristinare hello DPMDB eseguita dalla fine della parte 2</span><span class="sxs-lookup"><span data-stu-id="04d33-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="04d33-279">Collega archiviazione hello da hello originale backup toohello nuovo server.</span><span class="sxs-lookup"><span data-stu-id="04d33-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="04d33-280">Dal ripristino di SQL hello DPMDB</span><span class="sxs-lookup"><span data-stu-id="04d33-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="04d33-281">Dalla riga di comando di amministratore nel nuovo server cd tooMicrosoft Backup di Azure installare posizione e la cartella bin</span><span class="sxs-lookup"><span data-stu-id="04d33-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="04d33-282">Esempio di percorso: C:\windows\system32>cd "c:\Programmi\Microsoft Azure Backup\DPM\DPM\bin\"</span><span class="sxs-lookup"><span data-stu-id="04d33-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="04d33-283">backup tooAzure eseguire DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="04d33-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="04d33-284">Eseguire DPMSYNC-SYNC Nota Se è stato aggiunto nuovo pool di archiviazione di DPM toohello dischi anziché spostare hello quelle meno recenti, quindi eseguire DPMSYNC - Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="04d33-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="04d33-285">Nuovi cmdlet PowerShell della v2</span><span class="sxs-lookup"><span data-stu-id="04d33-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="04d33-286">Quando si installa il server di Backup di Azure v2, sono disponibili due nuovi cmdlet:</span><span class="sxs-lookup"><span data-stu-id="04d33-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="04d33-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="04d33-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="04d33-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="04d33-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="04d33-289">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="04d33-289">Next steps</span></span>

<span data-ttu-id="04d33-290">Informazioni su come tooprepare il server o iniziare a proteggere un carico di lavoro:</span><span class="sxs-lookup"><span data-stu-id="04d33-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="04d33-291">Preparare i carichi di lavoro del server di backup</span><span class="sxs-lookup"><span data-stu-id="04d33-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="04d33-292">Utilizzare tooback Server di Backup di un server VMware</span><span class="sxs-lookup"><span data-stu-id="04d33-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="04d33-293">Usare Backup Server tooback verticale di SQL Server</span><span class="sxs-lookup"><span data-stu-id="04d33-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="04d33-294">Usare Modern Backup Storage con il server di backup</span><span class="sxs-lookup"><span data-stu-id="04d33-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

