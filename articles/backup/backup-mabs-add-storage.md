---
title: aaaUse moderna archiviazione dei Backup con il Server di Backup di Azure v2 | Documenti Microsoft
description: "Informazioni sulle nuove funzionalità di hello Azure Backup Server v2. Questo articolo viene descritto come tooupgrade l'installazione del Server di Backup."
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
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="8759f-104">Aggiungere archiviazione tooAzure v2 Server Backup</span><span class="sxs-lookup"><span data-stu-id="8759f-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="8759f-105">Il server di Backup di Azure v2 include Modern Backup Storage di System Center 2016 Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="8759f-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="8759f-106">Modern Backup Storage garantisce un risparmio del 50% sullo spazio di archiviazione, backup tre volte più veloci e un'archiviazione più efficiente.</span><span class="sxs-lookup"><span data-stu-id="8759f-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="8759f-107">Offre anche l'archiviazione con riconoscimento del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8759f-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="8759f-108">toouse moderna archiviazione dei Backup, è necessario eseguire Backup Server v2 in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8759f-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="8759f-109">Se si esegue il server di Backup v2 in una versione precedente di Windows Server, il server di Backup di Azure non può avvalersi di Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="8759f-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="8759f-110">Invece, i carichi di lavoro vengono protetti come avviene nel server di Backup v1.</span><span class="sxs-lookup"><span data-stu-id="8759f-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="8759f-111">Per ulteriori informazioni, vedere versione del Server di Backup hello [matrice protezione](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="8759f-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="8759f-112">Volumi nel server di Backup v2</span><span class="sxs-lookup"><span data-stu-id="8759f-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="8759f-113">Il server di Backup v2 accetta volumi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8759f-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="8759f-114">Quando si aggiunge un volume, Backup Server formatta hello volume tooResilient File System (ReFS), che richiede l'archiviazione dei Backup moderne.</span><span class="sxs-lookup"><span data-stu-id="8759f-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="8759f-115">tooadd un volume, tooexpand e in un secondo momento, se necessario, si consiglia di utilizzare questo flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="8759f-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="8759f-116">Configurare il server di Backup v2 in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8759f-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="8759f-117">Creare un volume su un disco virtuale in un pool di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="8759f-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="8759f-118">Aggiungere un pool di archiviazione su disco tooa e creare un disco virtuale con layout semplice.</span><span class="sxs-lookup"><span data-stu-id="8759f-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="8759f-119">Aggiungere ulteriori dischi ed estendere disco virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8759f-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="8759f-120">Creare volumi nel disco virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8759f-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="8759f-121">Aggiungere hello volumi tooBackup Server.</span><span class="sxs-lookup"><span data-stu-id="8759f-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="8759f-122">Configurare l'archiviazione con riconoscimento del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8759f-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="8759f-123">Creare un volume per Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="8759f-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="8759f-124">L'utilizzo del server di Backup v2 con volumi come archiviazione su disco consente di mantenere il controllo sull'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8759f-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="8759f-125">Un volume può essere un singolo disco.</span><span class="sxs-lookup"><span data-stu-id="8759f-125">A volume can be a single disk.</span></span> <span data-ttu-id="8759f-126">Tuttavia, se si desidera archiviazione tooextend in hello future, creare un volume da un disco creato tramite spazi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8759f-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="8759f-127">Questo può aiutare se si desidera volume hello tooexpand per archiviazione di backup.</span><span class="sxs-lookup"><span data-stu-id="8759f-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="8759f-128">In questa sezione sono presentate le procedure consigliate per la creazione di un volume con questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="8759f-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="8759f-129">In Server Manager selezionare **Servizi file e archiviazione** > **Volumi** > **Pool di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="8759f-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="8759f-130">In **DISCHI FISICI**, selezionare **Nuovo pool di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="8759f-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Creare un nuovo pool di archiviazione](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="8759f-132">In hello **attività** casella di riepilogo a discesa, selezionare **nuovo disco virtuale**.</span><span class="sxs-lookup"><span data-stu-id="8759f-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Aggiungere un disco virtuale](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="8759f-134">Selezionare il pool di archiviazione hello e quindi selezionare **Aggiungi disco fisico**.</span><span class="sxs-lookup"><span data-stu-id="8759f-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Aggiungere un disco fisico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="8759f-136">Disco fisico hello, scegliere quindi **estendere disco virtuale**.</span><span class="sxs-lookup"><span data-stu-id="8759f-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Estendere disco virtuale hello](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="8759f-138">Selezionare i dischi virtuali hello, quindi **nuovo Volume**.</span><span class="sxs-lookup"><span data-stu-id="8759f-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Creare un nuovo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="8759f-140">In hello **selezionare server hello e il disco** finestra di dialogo, selezionare hello server e il disco di nuovo di hello.</span><span class="sxs-lookup"><span data-stu-id="8759f-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="8759f-141">Quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8759f-141">Then, select **Next**.</span></span>

    ![Selezionare disco e il server hello](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="8759f-143">Aggiungere spazio su disco Server tooBackup di volumi</span><span class="sxs-lookup"><span data-stu-id="8759f-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="8759f-144">tooadd tooBackup un volume Server, in hello **Management** riquadro Ripeti analisi archiviazione hello e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8759f-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="8759f-145">Viene visualizzato un elenco di tutti i hello volumi disponibili toobe aggiunto per l'archiviazione di Backup del Server.</span><span class="sxs-lookup"><span data-stu-id="8759f-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="8759f-146">Dopo che i volumi disponibili vengono aggiunte toohello elenco dei volumi selezionati, è possibile assegnare loro toohelp un nome descrittivo gestirli.</span><span class="sxs-lookup"><span data-stu-id="8759f-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="8759f-147">tooformat tooReFS questi volumi, in modo da Server di Backup può utilizzare i vantaggi di hello di archiviazione dei Backup moderna, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="8759f-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Aggiungere i volumi disponibili](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="8759f-149">Configurare l'archiviazione con riconoscimento del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="8759f-149">Set up workload-aware storage</span></span>

<span data-ttu-id="8759f-150">Con l'archiviazione in grado di riconoscere il carico di lavoro, è possibile selezionare volumi hello che archiviano preferibilmente determinati tipi di carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8759f-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="8759f-151">Ad esempio, è possibile impostare costosa volumi che supportano un numero elevato di operazioni di input/output al secondo (IOPS) toostore soli hello carichi di lavoro che richiedono frequenti backup volumi elevati.</span><span class="sxs-lookup"><span data-stu-id="8759f-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="8759f-152">Un esempio è SQL Server con i log delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="8759f-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="8759f-153">Altri carichi di lavoro che vengono sottoposti a backup meno frequentemente, ad esempio le macchine virtuali, eseguirne il backup toolow costo volumi.</span><span class="sxs-lookup"><span data-stu-id="8759f-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="8759f-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="8759f-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="8759f-155">È possibile impostare l'archiviazione del carico di lavoro tramite il cmdlet PowerShell hello aggiornamento DPMDiskStorage, che aggiorna le proprietà di hello di un volume nel pool di archiviazione hello in un server di Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="8759f-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="8759f-156">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="8759f-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="8759f-157">Hello seguente schermata mostra cmdlet Update-DPMDiskStorage hello nella finestra di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8759f-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![comando Update-DPMDiskStorage nella finestra di PowerShell hello Hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="8759f-159">Hello effettuate usando PowerShell vengono riflesse nell'hello Console di amministrazione di Server di Backup.</span><span class="sxs-lookup"><span data-stu-id="8759f-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![I dischi e volumi nella Console di amministrazione di hello](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="8759f-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8759f-161">Next steps</span></span>
<span data-ttu-id="8759f-162">Dopo aver installato il Server di Backup, informazioni su come tooprepare del server, o iniziare a proteggere un carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8759f-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="8759f-163">Preparare i carichi di lavoro del server di backup</span><span class="sxs-lookup"><span data-stu-id="8759f-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="8759f-164">Utilizzare tooback Server di Backup di un server VMware</span><span class="sxs-lookup"><span data-stu-id="8759f-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="8759f-165">Usare Backup Server tooback verticale di SQL Server</span><span class="sxs-lookup"><span data-stu-id="8759f-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

