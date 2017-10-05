---
title: Gestire i backup delle macchine virtuali distribuite con Resource Manager | Microsoft Docs
description: Informazioni su come gestire e monitorare i backup delle macchine virtuali distribuite con Resource Manager
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 35a21cb99ca4bad124a9f764cef9da453e1fe47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="1a384-103">Gestire i backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1a384-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a384-104">Gestire i backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="1a384-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="1a384-105">Gestire i backup delle macchine virtuali classiche</span><span class="sxs-lookup"><span data-stu-id="1a384-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="1a384-106">Questo articolo contiene indicazioni sulla gestione dei backup delle VM e illustra le informazioni degli avvisi relativi al backup disponibili nel dashboard del portale.</span><span class="sxs-lookup"><span data-stu-id="1a384-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="1a384-107">Le informazioni aggiuntive incluse in questo articolo si applicano all'uso di macchine virtuali con gli insiemi di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1a384-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="1a384-108">Questo articolo non illustra la creazione di macchine virtuali, né come proteggerle.</span><span class="sxs-lookup"><span data-stu-id="1a384-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="1a384-109">Per una panoramica della protezione di macchine virtuali distribuite tramite Azure Resource Manager con un insieme di credenziali di Servizi di ripristino, vedere [Primi passi: eseguire il backup di VM di Azure Resource Manager in un insieme di credenziali dei servizi di ripristino](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1a384-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="1a384-110">Gestire gli insiemi di credenziali e le macchine virtuali protette</span><span class="sxs-lookup"><span data-stu-id="1a384-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="1a384-111">Nel portale di Azure il dashboard dell'insieme di credenziali di Servizi di ripristino consente di accedere alle informazioni relative all'insieme di credenziali, quali:</span><span class="sxs-lookup"><span data-stu-id="1a384-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="1a384-112">Snapshot di backup più recente, che corrisponde anche al punto di ripristino più recente <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="1a384-113">Criteri di backup <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-113">the backup policy <br\></span></span>
* <span data-ttu-id="1a384-114">Dimensioni totali di tutti gli snapshot di backup <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="1a384-115">Numero di macchine virtuali protette con l'insieme di credenziali <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="1a384-116">Molte attività di gestione per il backup di una macchina virtuale iniziano con l'apertura dell'insieme di credenziali nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="1a384-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="1a384-117">Dato che gli insiemi di credenziali possono essere usati per proteggere più elementi (o più VM), tuttavia, per visualizzare i dettagli relativi a una determinata VM aprire il dashboard dell'elemento dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1a384-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="1a384-118">La procedura seguente illustra come aprire il *dashboard dell'insieme di credenziali* per poi passare al *dashboard dell'elemento dell'insieme di credenziali*.</span><span class="sxs-lookup"><span data-stu-id="1a384-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="1a384-119">Entrambe le procedure includono "suggerimenti" che indicano come aggiungere l'insieme di credenziali e l'elemento dell'insieme di credenziali al dashboard di Azure tramite il comando Aggiungi al dashboard.</span><span class="sxs-lookup"><span data-stu-id="1a384-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="1a384-120">L'aggiunta al dashboard è un modo per creare un collegamento all'insieme di credenziali o a un elemento.</span><span class="sxs-lookup"><span data-stu-id="1a384-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="1a384-121">Dal collegamento è anche possibile eseguire comandi comuni.</span><span class="sxs-lookup"><span data-stu-id="1a384-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="1a384-122">Se sono aperti più dashboard e pannelli, usare il dispositivo di scorrimento blu nella parte inferiore della finestra per scorrere in modo bidirezionale il dashboard di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a384-122">If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.</span></span>
>
>

![Visualizzazione completa con il dispositivo di scorrimento](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="1a384-124">Aprire un insieme di credenziali di Servizi di ripristino nel dashboard:</span><span class="sxs-lookup"><span data-stu-id="1a384-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="1a384-125">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1a384-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1a384-126">Scegliere **Sfoglia** dal menu Hub e digitare **Servizi di ripristino** nell'elenco di risorse.</span><span class="sxs-lookup"><span data-stu-id="1a384-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="1a384-127">Non appena si inizia a digitare, l'elenco viene filtrato in base all'input.</span><span class="sxs-lookup"><span data-stu-id="1a384-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="1a384-128">Fare clic su **Insieme di credenziali dei servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="1a384-128">Click **Recovery Services vault**.</span></span>

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="1a384-130">Viene visualizzato l'elenco di insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1a384-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="1a384-131">Elenco di insiemi di credenziali dei Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="1a384-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="1a384-132">Se si aggiunge un insieme di credenziali al dashboard di Azure, sarà immediatamente accessibile quando si apre il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a384-132">If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal.</span></span> <span data-ttu-id="1a384-133">Per aggiungere un insieme di credenziali al dashboard, nell'elenco di insiemi di credenziali fare clic con il pulsante destro del mouse sull'insieme desiderato e scegliere **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="1a384-133">To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.</span></span>
   >
   >
3. <span data-ttu-id="1a384-134">Nell'elenco di insiemi di credenziali selezionare quello per cui si vuole aprire il dashboard.</span><span class="sxs-lookup"><span data-stu-id="1a384-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="1a384-135">Quando si seleziona l'insieme di credenziali, vengono aperti il dashboard corrispondente e il relativo pannello **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="1a384-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="1a384-136">Nella figura seguente è evidenziato il dashboard **Contoso-vault** .</span><span class="sxs-lookup"><span data-stu-id="1a384-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![Aprire il dashboard dell'insieme di credenziali e il pannello Impostazioni](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="1a384-138">Aprire il dashboard di un elemento dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="1a384-138">Open a vault item dashboard</span></span>
<span data-ttu-id="1a384-139">Nella procedura precedente è stato aperto il dashboard dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1a384-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="1a384-140">Per aprire il dashboard di un elemento dell'insieme di credenziali:</span><span class="sxs-lookup"><span data-stu-id="1a384-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="1a384-141">Nel riquadro **Elementi di backup** del dashboard dell'insieme di credenziali fare clic su **Macchine virtuali di Azure**.</span><span class="sxs-lookup"><span data-stu-id="1a384-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Aprire il riquadro Elementi di backup](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="1a384-143">Il pannello **Macchine virtuali di Azure** elenca l'ultimo processo di backup per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="1a384-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="1a384-144">In questo esempio è presente una sola macchina virtuale, demovm-markgal, protetta da questo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1a384-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Riquadro Elementi di backup](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="1a384-146">Per facilitare l'accesso, è possibile aggiungere un elemento dell'insieme di credenziali al dashboard di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a384-146">For ease of access, you can pin a vault item to the Azure Dashboard.</span></span> <span data-ttu-id="1a384-147">Per aggiungere un elemento dell'insieme di credenziali, nell'elenco di insiemi di credenziali fare clic con il pulsante destro del mouse sull'elemento desiderato e scegliere **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="1a384-147">To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.</span></span>
   >
   >
2. <span data-ttu-id="1a384-148">Nel pannello **Elementi di backup** fare clic sull'elemento per aprire il dashboard dell'elemento dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1a384-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![Riquadro Elementi di backup](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="1a384-150">Verranno visualizzati il dashboard dell'elemento dell'insieme di credenziali e il relativo pannello **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="1a384-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![Dashboard degli elementi di backup con il pannello Impostazioni](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="1a384-152">Dal dashboard dell'elemento dell'insieme di credenziali è possibile eseguire molte attività di gestione importanti, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1a384-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="1a384-153">Modificare i criteri o creare nuovi criteri di backup<br\></span><span class="sxs-lookup"><span data-stu-id="1a384-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="1a384-154">Visualizzare i punti di ripristino e vedere il relativo stato di coerenza <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="1a384-155">Eseguire il backup su richiesta di una macchina virtuale <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="1a384-156">Arrestare la protezione delle macchine virtuali <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="1a384-157">Riprendere la protezione delle macchine virtuali <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="1a384-158">Eliminare i dati di un backup o un punto di ripristino <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="1a384-159">[ripristinare i dischi di backup](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="1a384-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="1a384-160">Per le procedure seguenti, il punto di partenza è il dashboard dell'elemento dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1a384-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="1a384-161">Gestire i criteri di backup</span><span class="sxs-lookup"><span data-stu-id="1a384-161">Manage backup policies</span></span>
1. <span data-ttu-id="1a384-162">Nel [dashboard dell'elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard) fare clic su **All Settings** (Tutte le impostazioni) per aprire il pannello **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="1a384-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![Pannello Criteri di backup](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="1a384-164">Nel pannello **Impostazioni** fare clic su **Criteri di backup** per aprire il pannello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="1a384-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="1a384-165">Nel pannello vengono visualizzati i dettagli relativi a intervallo di conservazione e frequenza di backup.</span><span class="sxs-lookup"><span data-stu-id="1a384-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![Pannello Criteri di backup](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="1a384-167">Dal menu **Scegliere i criteri di backup** :</span><span class="sxs-lookup"><span data-stu-id="1a384-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="1a384-168">Per modificare i criteri, selezionare criteri diversi e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1a384-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="1a384-169">Il nuovo criterio verrà immediatamente applicato all'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="1a384-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="1a384-170"><br\></span><span class="sxs-lookup"><span data-stu-id="1a384-170"><br\></span></span>
   * <span data-ttu-id="1a384-171">Per creare i criteri, selezionare **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="1a384-171">To create a policy, select **Create New**.</span></span>

     ![Backup di una macchina virtuale](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="1a384-173">Per istruzioni sulla creazione di criteri di backup, vedere [Definizione di un criterio di backup](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="1a384-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="1a384-174">Durante la gestione dei criteri di backup, assicurarsi di seguire le [procedure consigliate](backup-azure-vms-introduction.md#best-practices) per garantire prestazioni di backup ottimali</span><span class="sxs-lookup"><span data-stu-id="1a384-174">While managing backup policies, make sure to follow the [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="1a384-175">Backup su richiesta di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1a384-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="1a384-176">È possibile eseguire il backup su richiesta di una macchina virtuale dopo averla configurata per la protezione.</span><span class="sxs-lookup"><span data-stu-id="1a384-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="1a384-177">Se il backup iniziale è in sospeso, il backup su richiesta crea una copia completa della macchina virtuale nell'insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1a384-177">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="1a384-178">Se il backup iniziale è stato completato, un backup su richiesta invierà all'insieme di credenziali dei servizi di ripristino solo le modifiche rispetto allo snapshot precedente.</span><span class="sxs-lookup"><span data-stu-id="1a384-178">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="1a384-179">I backup successivi sono sempre incrementali.</span><span class="sxs-lookup"><span data-stu-id="1a384-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="1a384-180">L'intervallo di conservazione per un backup su richiesta è il valore di conservazione specificato nei criteri per il punto di backup giornaliero.</span><span class="sxs-lookup"><span data-stu-id="1a384-180">The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy.</span></span> <span data-ttu-id="1a384-181">Se il punto di backup giornaliero non è selezionato, verrà usato quello settimanale.</span><span class="sxs-lookup"><span data-stu-id="1a384-181">If no Daily backup point is selected, then the weekly backup point is used.</span></span>
>
>

<span data-ttu-id="1a384-182">Per attivare un backup su richiesta di una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="1a384-182">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="1a384-183">Nel [dashboard dell'elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard)fare clic su **Esegui backup ora**.</span><span class="sxs-lookup"><span data-stu-id="1a384-183">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Pulsante Esegui backup ora](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="1a384-185">Il portale richiede di confermare l'avvio del processo di backup su richiesta.</span><span class="sxs-lookup"><span data-stu-id="1a384-185">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="1a384-186">Per avviarlo, fare clic su **Sì** .</span><span class="sxs-lookup"><span data-stu-id="1a384-186">Click **Yes** to start the backup job.</span></span>

    ![Pulsante Esegui backup ora](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="1a384-188">Il processo di backup crea un punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1a384-188">The backup job creates a recovery point.</span></span> <span data-ttu-id="1a384-189">L'intervallo di conservazione del punto di ripristino è uguale a quello specificato nei criteri associati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1a384-189">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="1a384-190">Per tenere traccia dello stato di avanzamento del processo, nel dashboard dell'insieme di credenziali fare clic sul riquadro **Processi di backup** .</span><span class="sxs-lookup"><span data-stu-id="1a384-190">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="1a384-191">Arrestare la protezione delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1a384-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="1a384-192">Se si sceglie di arrestare la protezione di una macchina virtuale, viene chiesto se si vogliono mantenere i punti di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1a384-192">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="1a384-193">Per arrestare la protezione delle macchine virtuali è possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="1a384-193">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="1a384-194">interrompere tutti i processi di backup futuri ed eliminare tutti i punti di ripristino oppure</span><span class="sxs-lookup"><span data-stu-id="1a384-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="1a384-195">interrompere tutti i processi di backup futuri mantenendo però i punti di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1a384-195">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="1a384-196">Al mantenimento dei punti di ripristino nella risorsa di archiviazione è associato un costo.</span><span class="sxs-lookup"><span data-stu-id="1a384-196">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="1a384-197">Tuttavia, la possibilità di mantenere i punti di ripristino per ripristinare la macchina virtuale in un secondo momento, se necessario, costituisce un vantaggio.</span><span class="sxs-lookup"><span data-stu-id="1a384-197">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="1a384-198">Per informazioni sul costo associato al mantenimento dei punti di ripristino, vedere [Dettagli prezzi](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="1a384-198">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="1a384-199">Se si sceglie di eliminare tutti i punti di ripristino, non sarà possibile ripristinare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1a384-199">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="1a384-200">Per arrestare la protezione per una macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="1a384-200">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="1a384-201">Nel [dashboard dell'elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard)fare clic su **Interrompi backup**.</span><span class="sxs-lookup"><span data-stu-id="1a384-201">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Pulsante Arresta backup](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="1a384-203">Verrà visualizzato il pannello Arresta backup.</span><span class="sxs-lookup"><span data-stu-id="1a384-203">The Stop Backup blade opens.</span></span>

    ![Pannello Arresta backup](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="1a384-205">Nel pannello **Interrompi backup** scegliere se mantenere o eliminare i dati di backup.</span><span class="sxs-lookup"><span data-stu-id="1a384-205">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="1a384-206">La casella delle informazioni include i dettagli sulla scelta effettuata.</span><span class="sxs-lookup"><span data-stu-id="1a384-206">The information box provides details about your choice.</span></span>

    ![Arresta protezione](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="1a384-208">Se si è scelto di mantenere i dati di backup, andare al passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="1a384-208">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="1a384-209">Se si è scelto di eliminare i dati di backup, confermare l'arresto dei processi di backup ed eliminare i punti di ripristino, digitando il nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="1a384-209">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![Arresta verifica](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="1a384-211">Se non si è certi del nome dell'elemento, passare il puntatore sul punto esclamativo per visualizzarlo.</span><span class="sxs-lookup"><span data-stu-id="1a384-211">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="1a384-212">Il nome dell'elemento si trova anche nella parte superiore del pannello **Interrompi backup** .</span><span class="sxs-lookup"><span data-stu-id="1a384-212">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="1a384-213">L'aggiunta di un **motivo** o **commento** è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1a384-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="1a384-214">Per arrestare il processo di backup per l'elemento corrente, fare clic su ![backup pulsante di arresto](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="1a384-214">To stop the backup job for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="1a384-215">Un messaggio di notifica informa che i processi di backup sono stati arrestati.</span><span class="sxs-lookup"><span data-stu-id="1a384-215">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![Conferma arresto protezione](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="1a384-217">Riprendere la protezione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1a384-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="1a384-218">Se quando è stata arrestata la protezione della macchina virtuale è stata scelta l'opzione **Conserva i dati di backup** , è possibile riprendere la protezione.</span><span class="sxs-lookup"><span data-stu-id="1a384-218">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="1a384-219">Se è stata scelta l'opzione **Elimina dati di backup** , la protezione della macchina virtuale non può essere ripresa.</span><span class="sxs-lookup"><span data-stu-id="1a384-219">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="1a384-220">Per riprendere la protezione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1a384-220">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="1a384-221">Nel [dashboard dell'elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard)fare clic su **Riprendi backup**.</span><span class="sxs-lookup"><span data-stu-id="1a384-221">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Riprendere la protezione](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="1a384-223">Verrà visualizzato il pannello Criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="1a384-223">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1a384-224">Quando si riattiva la protezione della macchina virtuale, è possibile scegliere un criterio diverso rispetto ai criteri con cui la macchina virtuale è stata protetta inizialmente.</span><span class="sxs-lookup"><span data-stu-id="1a384-224">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="1a384-225">Per assegnare i criteri della macchina virtuale, seguire la procedura descritta in [Gestire i criteri di backup](backup-azure-manage-vms.md#manage-backup-policies).</span><span class="sxs-lookup"><span data-stu-id="1a384-225">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="1a384-226">Dopo l'applicazione dei criteri di backup alla macchina virtuale, verrà visualizzato il messaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="1a384-226">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![Macchina virtuale protetta correttamente](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="1a384-228">Elimina dati di backup</span><span class="sxs-lookup"><span data-stu-id="1a384-228">Delete Backup data</span></span>
<span data-ttu-id="1a384-229">È possibile eliminare i dati di backup associati a una macchina virtuale durante il processo **Interrompi backup** o in qualsiasi momento dopo il completamento del backup.</span><span class="sxs-lookup"><span data-stu-id="1a384-229">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="1a384-230">Attendere settimane o mesi prima di eliminare i punti di ripristino potrebbe anche essere utile.</span><span class="sxs-lookup"><span data-stu-id="1a384-230">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="1a384-231">A differenza del recupero dei punti di ripristino, quando si eliminano i dati di backup, non è possibile scegliere di eliminare punti di ripristino specifici.</span><span class="sxs-lookup"><span data-stu-id="1a384-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="1a384-232">Se si sceglie di eliminare i dati di backup, vengono eliminati tutti i punti di ripristino associati all'elemento.</span><span class="sxs-lookup"><span data-stu-id="1a384-232">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="1a384-233">Nella procedura seguente si presuppone che il processo di backup per la macchina virtuale sia stato arrestato o disabilitato.</span><span class="sxs-lookup"><span data-stu-id="1a384-233">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="1a384-234">Dopo che è stato disabilitato il processo di backup, nel dashboard dell'elemento dell'insieme di credenziali sono disponibili le opzioni **Riprendi backup** ed **Elimina backup**.</span><span class="sxs-lookup"><span data-stu-id="1a384-234">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![Pulsanti Riprendi ed Elimina](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="1a384-236">Per eliminare i dati di backup in una macchina virtuale con il *backup disabilitato*:</span><span class="sxs-lookup"><span data-stu-id="1a384-236">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="1a384-237">Nel [dashboard dell'elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard)fare clic su **Elimina dati di backup**.</span><span class="sxs-lookup"><span data-stu-id="1a384-237">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="1a384-239">Verrà visualizzato il pannello **Elimina dati di backup** .</span><span class="sxs-lookup"><span data-stu-id="1a384-239">The **Delete Backup Data** blade opens.</span></span>

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="1a384-241">È necessario digitare il nome dell'elemento per confermare l'eliminazione dei punti di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1a384-241">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![Arresta verifica](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="1a384-243">Se non si è certi del nome dell'elemento, passare il puntatore sul punto esclamativo per visualizzarlo.</span><span class="sxs-lookup"><span data-stu-id="1a384-243">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="1a384-244">Il nome dell'elemento si trova anche nella parte superiore del pannello **Elimina dati backup** .</span><span class="sxs-lookup"><span data-stu-id="1a384-244">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="1a384-245">L'aggiunta di un **motivo** o **commento** è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="1a384-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="1a384-246">Per eliminare i dati di backup per l'elemento corrente, fare clic su ![backup pulsante di arresto](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="1a384-246">To delete the backup data for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="1a384-247">Un messaggio di notifica informa che i dati di backup sono stati eliminati.</span><span class="sxs-lookup"><span data-stu-id="1a384-247">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a384-248">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a384-248">Next steps</span></span>
<span data-ttu-id="1a384-249">Per informazioni su come ricreare una macchina virtuale da un punto di ripristino, vedere [Ripristinare macchine virtuali in Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="1a384-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="1a384-250">Per informazioni sulla protezione delle macchine virtuali, vedere [Primo approccio: Proteggere le VM di Azure con un insieme di credenziali dei servizi di ripristino](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1a384-250">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="1a384-251">Per informazioni sul monitoraggio degli eventi, vedere [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md)(Monitorare gli avvisi per i backup delle macchine virtuali di Azure).</span><span class="sxs-lookup"><span data-stu-id="1a384-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
