---
title: Utilizzare Modern Backup Storage con il server di Backup di Azure v2 | Microsoft Docs
description: "Informazioni sulle nuove funzionalità del server di Backup di Azure v2. In questo articolo viene descritto come aggiornare l'installazione del server di backup."
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
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="13ad8-104">Aggiungere spazio di archiviazione al server di Backup di Azure v2</span><span class="sxs-lookup"><span data-stu-id="13ad8-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="13ad8-105">Il server di Backup di Azure v2 include Modern Backup Storage di System Center 2016 Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="13ad8-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="13ad8-106">Modern Backup Storage garantisce un risparmio del 50% sullo spazio di archiviazione, backup tre volte più veloci e un'archiviazione più efficiente.</span><span class="sxs-lookup"><span data-stu-id="13ad8-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="13ad8-107">Offre anche l'archiviazione con riconoscimento del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="13ad8-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="13ad8-108">Per utilizzare Modern Backup Storage, è necessario eseguire il server di Backup v2 in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="13ad8-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="13ad8-109">Se si esegue il server di Backup v2 in una versione precedente di Windows Server, il server di Backup di Azure non può avvalersi di Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="13ad8-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="13ad8-110">Invece, i carichi di lavoro vengono protetti come avviene nel server di Backup v1.</span><span class="sxs-lookup"><span data-stu-id="13ad8-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="13ad8-111">Per ulteriori informazioni, vedere la [matrice di protezione](backup-mabs-protection-matrix.md) della versione del server di backup.</span><span class="sxs-lookup"><span data-stu-id="13ad8-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="13ad8-112">Volumi nel server di Backup v2</span><span class="sxs-lookup"><span data-stu-id="13ad8-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="13ad8-113">Il server di Backup v2 accetta volumi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="13ad8-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="13ad8-114">Quando si aggiunge un volume, il server di backup formatta il volume in Resilient File System (ReFS), richiesto da Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="13ad8-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="13ad8-115">Per aggiungere un volume ed espanderlo in un secondo momento se necessario, è consigliabile utilizzare questo flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="13ad8-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="13ad8-116">Configurare il server di Backup v2 in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13ad8-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="13ad8-117">Creare un volume su un disco virtuale in un pool di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="13ad8-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="13ad8-118">Aggiungere un disco a un pool di archiviazione e creare un disco virtuale con layout semplice.</span><span class="sxs-lookup"><span data-stu-id="13ad8-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="13ad8-119">Aggiungere altri dischi ed estendere il disco virtuale.</span><span class="sxs-lookup"><span data-stu-id="13ad8-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="13ad8-120">Creare volumi nel disco virtuale.</span><span class="sxs-lookup"><span data-stu-id="13ad8-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="13ad8-121">Aggiungere i volumi al server di backup.</span><span class="sxs-lookup"><span data-stu-id="13ad8-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="13ad8-122">Configurare l'archiviazione con riconoscimento del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="13ad8-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="13ad8-123">Creare un volume per Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="13ad8-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="13ad8-124">L'utilizzo del server di Backup v2 con volumi come archiviazione su disco consente di mantenere il controllo sull'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="13ad8-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="13ad8-125">Un volume può essere un singolo disco.</span><span class="sxs-lookup"><span data-stu-id="13ad8-125">A volume can be a single disk.</span></span> <span data-ttu-id="13ad8-126">Tuttavia, se si desidera estendere l'archiviazione in futuro, creare un volume da un disco creato utilizzando spazi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="13ad8-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="13ad8-127">Ciò può essere utile se si desidera espandere il volume per l'archiviazione di backup.</span><span class="sxs-lookup"><span data-stu-id="13ad8-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="13ad8-128">In questa sezione sono presentate le procedure consigliate per la creazione di un volume con questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="13ad8-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="13ad8-129">In Server Manager selezionare **Servizi file e archiviazione** > **Volumi** > **Pool di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="13ad8-130">In **DISCHI FISICI**, selezionare **Nuovo pool di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Creare un nuovo pool di archiviazione](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="13ad8-132">Nella casella di riepilogo a discesa **ATTIVITÀ** selezionare **Nuovo disco virtuale**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Aggiungere un disco virtuale](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="13ad8-134">Selezionare il pool di archiviazione e quindi selezionare **Aggiungi disco fisico**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![Aggiungere un disco fisico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="13ad8-136">Selezionare il disco fisico e quindi **Estendi disco virtuale**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Estendere il disco virtuale](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="13ad8-138">Selezionare il disco virtuale e quindi **Nuovo volume**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![Creare un nuovo volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="13ad8-140">Nella finestra di dialogo **Selezionare il server e il disco** selezionare il server e il nuovo disco.</span><span class="sxs-lookup"><span data-stu-id="13ad8-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="13ad8-141">Quindi selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-141">Then, select **Next**.</span></span>

    ![Selezionare il server e il disco](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="13ad8-143">Aggiungere i volumi all'archiviazione su disco del server di backup</span><span class="sxs-lookup"><span data-stu-id="13ad8-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="13ad8-144">Per aggiungere un volume al server di backup, nel riquadro **Gestione** ripetere l'analisi dell'archiviazione e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="13ad8-145">Viene visualizzato un elenco di tutti i volumi disponibili per l'aggiunta per l'archiviazione del server di backup.</span><span class="sxs-lookup"><span data-stu-id="13ad8-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="13ad8-146">Dopo l'aggiunta dei volumi disponibili all'elenco dei volumi selezionati, è possibile assegnare loro un nome descrittivo per agevolarne la gestione.</span><span class="sxs-lookup"><span data-stu-id="13ad8-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="13ad8-147">Per formattare questi volumi in ReFS e consentire al server di backup di sfruttare i vantaggi di Modern Backup Storage, selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="13ad8-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![Aggiungere i volumi disponibili](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="13ad8-149">Configurare l'archiviazione con riconoscimento del carico di lavoro</span><span class="sxs-lookup"><span data-stu-id="13ad8-149">Set up workload-aware storage</span></span>

<span data-ttu-id="13ad8-150">Con l'archiviazione del carico di lavoro, è possibile selezionare i volumi in cui archiviare preferibilmente determinati tipi di carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="13ad8-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="13ad8-151">Ad esempio, è possibile configurare volumi costosi che supportano un numero elevato di operazioni di input/output al secondo (IOPS) per archiviare solo i carichi di lavoro che richiedono backup frequenti di volumi elevati.</span><span class="sxs-lookup"><span data-stu-id="13ad8-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="13ad8-152">Un esempio è SQL Server con i log delle transazioni.</span><span class="sxs-lookup"><span data-stu-id="13ad8-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="13ad8-153">Per il backup di altri carichi di lavoro, ad esempio le macchine virtuali, che viene eseguito meno frequentemente, utilizzare volumi a basso costo.</span><span class="sxs-lookup"><span data-stu-id="13ad8-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="13ad8-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="13ad8-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="13ad8-155">È possibile configurare l'archiviazione con riconoscimento del carico di lavoro utilizzando il cmdlet di PowerShell Update-DPMDiskStorage che aggiorna le proprietà di un volume nel pool di archiviazione di un server Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="13ad8-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="13ad8-156">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="13ad8-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="13ad8-157">Nella schermata seguente viene illustrato il cmdlet Update-DPMDiskStorage nella finestra di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13ad8-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![Comando Update-DPMDiskStorage nella finestra di PowerShell](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="13ad8-159">Le modifiche apportate tramite PowerShell vengono riflesse nella Console di amministrazione del server di backup.</span><span class="sxs-lookup"><span data-stu-id="13ad8-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![Dischi e volumi nella Console di amministrazione](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="13ad8-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13ad8-161">Next steps</span></span>
<span data-ttu-id="13ad8-162">Dopo aver installato il server di backup, leggere le informazioni su come preparare il server o iniziare a proteggere un carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="13ad8-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="13ad8-163">Preparare i carichi di lavoro del server di backup</span><span class="sxs-lookup"><span data-stu-id="13ad8-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="13ad8-164">Usare il server di backup per eseguire il backup di un server VMware</span><span class="sxs-lookup"><span data-stu-id="13ad8-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="13ad8-165">Usare il server di backup per eseguire il backup di SQL Server</span><span class="sxs-lookup"><span data-stu-id="13ad8-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

