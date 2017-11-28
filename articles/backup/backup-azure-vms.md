---
title: aaaBack le credenziali di backup tooa distribuito classica macchine virtuali di Azure | Documenti Microsoft
description: Individuare, registrare ed eseguire il backup delle macchine virtuali usando queste procedure per il backup di macchine virtuali di Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup della macchina virtuale; eseguire il backup della macchina virtuale; backup e ripristino di emergenza; backup di vm
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="7eea2-104">Eseguire il backup di macchine virtuali di Azure (portale classico)</span><span class="sxs-lookup"><span data-stu-id="7eea2-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7eea2-105">Eseguire il backup dell'insieme di credenziali di macchine virtuali tooRecovery servizi</span><span class="sxs-lookup"><span data-stu-id="7eea2-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="7eea2-106">Eseguire il backup dell'insieme di credenziali tooBackup macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7eea2-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="7eea2-107">In questo articolo vengono descritte le procedure hello per il backup di un insieme di credenziali Backup tooa distribuito classica macchina virtuale di Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="7eea2-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="7eea2-108">Esistono alcune attività, che è necessario tootake care di poter eseguire il backup di una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7eea2-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="7eea2-109">Se non è già in questo caso, tutte le hello [prerequisiti](backup-azure-vms-prepare.md) tooprepare l'ambiente per il backup delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7eea2-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="7eea2-110">Per ulteriori informazioni, vedere gli articoli di hello in [pianificazione dell'infrastruttura di backup di VM in Azure](backup-azure-vms-introduction.md) e [macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="7eea2-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="7eea2-111">Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7eea2-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7eea2-112">Un insieme di credenziali per il backup consente di proteggere solo macchine virtuali distribuite con il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="7eea2-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="7eea2-113">Non è possibile proteggere le macchine virtuali distribuite con il modello di distribuzione Resource Manager usando un insieme di credenziali per il backup.</span><span class="sxs-lookup"><span data-stu-id="7eea2-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="7eea2-114">Vedere [eseguire il backup dell'insieme di credenziali di macchine virtuali tooRecovery servizi](backup-azure-arm-vms.md) per informazioni dettagliate sull'utilizzo dei servizi di ripristino di insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="7eea2-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="7eea2-115">L'esecuzione del backup di macchine virtuali di Azure prevede tre passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="7eea2-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Tooback tre passaggi di una macchina virtuale IaaS di Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="7eea2-117">Il backup di macchine virtuali è un processo locale.</span><span class="sxs-lookup"><span data-stu-id="7eea2-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="7eea2-118">È possibile eseguire il backup di macchine virtuali in una regione tooa insieme di credenziali backup in un'altra area.</span><span class="sxs-lookup"><span data-stu-id="7eea2-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="7eea2-119">È quindi necessario creare un insieme di credenziali per il backup in ogni area di Azure dove sono presenti VM di cui sarà seguito il backup.</span><span class="sxs-lookup"><span data-stu-id="7eea2-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="7eea2-120">A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.</span><span class="sxs-lookup"><span data-stu-id="7eea2-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="7eea2-121">È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery.</span><span class="sxs-lookup"><span data-stu-id="7eea2-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="7eea2-122">Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="7eea2-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="7eea2-123">Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="7eea2-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="7eea2-124">Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup.</span><span class="sxs-lookup"><span data-stu-id="7eea2-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="7eea2-125">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="7eea2-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="7eea2-126">Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="7eea2-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="7eea2-127">Si sarà in grado di tooaccess ai dati di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="7eea2-128">Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="7eea2-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="7eea2-129">Passaggio 1: Individuare le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7eea2-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="7eea2-130">tooensure ogni nuova sottoscrizione toohello aggiunta di macchine virtuali (VM) vengono identificati prima di registrare, eseguire il processo di individuazione di hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="7eea2-131">le query di processo di Hello Azure per elenco hello delle macchine virtuali nella sottoscrizione di hello, insieme a informazioni aggiuntive come nome del servizio cloud hello e area hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="7eea2-132">Accedi toohello [portale classico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="7eea2-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="7eea2-133">Nell'elenco di hello dei servizi Azure, fare clic su **servizi di ripristino** elenco hello tooopen degli insiemi di credenziali di Backup e ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="7eea2-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="7eea2-134">![Elenco dell'insieme di credenziali](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="7eea2-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="7eea2-135">Nell'elenco di hello degli insiemi di credenziali di Backup, selezionare hello insieme di credenziali tooback una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7eea2-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="7eea2-136">Se si tratta di un nuovo portale hello insieme di credenziali apre toohello **avvio rapido** pagina.</span><span class="sxs-lookup"><span data-stu-id="7eea2-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![Menu Elementi registrati aperto](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="7eea2-138">Se in precedenza è stato configurato l'insieme di credenziali hello, viene visualizzato il portale di hello menu toohello utilizzato più di recente.</span><span class="sxs-lookup"><span data-stu-id="7eea2-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="7eea2-139">Dal menu di insieme di credenziali hello (in alto hello hello pagina), fare clic su **elementi registrati**.</span><span class="sxs-lookup"><span data-stu-id="7eea2-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![Menu Elementi registrati aperto](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="7eea2-141">Da hello **tipo** dal menu **macchina virtuale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="7eea2-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="7eea2-143">Fare clic su **DISCOVER** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="7eea2-144">![Pulsante Individua](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="7eea2-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="7eea2-145">il processo di individuazione Hello potrebbe richiedere alcuni minuti hello le macchine virtuali sono in elencati in formato tabulare.</span><span class="sxs-lookup"><span data-stu-id="7eea2-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="7eea2-146">Vi è una notifica nella parte inferiore di hello della schermata Ciao che informa che il processo di hello sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7eea2-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Individuare le VM](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="7eea2-148">notifica Hello cambia quando il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="7eea2-149">Se il processo di individuazione hello non ha trovato hello le macchine virtuali, verificare che le macchine virtuali hello esistono.</span><span class="sxs-lookup"><span data-stu-id="7eea2-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="7eea2-150">Se le macchine virtuali hello esistono, verificare hello macchine virtuali sono in hello stessa area dell'insieme di credenziali di backup hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="7eea2-151">Se le macchine virtuali hello esistano e siano in hello stessa area, verificare che le macchine virtuali hello non sono già registrati tooa credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="7eea2-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="7eea2-152">Se una macchina virtuale è tooa assegnate credenziali di backup non è disponibile toobe assegnato tooother insiemi di credenziali backup.</span><span class="sxs-lookup"><span data-stu-id="7eea2-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![Individuazione completata](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="7eea2-154">Dopo aver individuato i nuovi elementi di hello, andare tooStep 2 e registrare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7eea2-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="7eea2-155">Passaggio 2: Registrare le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7eea2-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="7eea2-156">Si registra un tooassociate macchina virtuale di Azure con hello servizio Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="7eea2-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="7eea2-157">Questa attività viene in genere eseguita una sola volta.</span><span class="sxs-lookup"><span data-stu-id="7eea2-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="7eea2-158">Passare l'insieme di credenziali backup toohello in **servizi di ripristino** in hello portale di Azure e quindi fare clic su **elementi registrati**.</span><span class="sxs-lookup"><span data-stu-id="7eea2-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="7eea2-159">Selezionare **macchina virtuale di Azure** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Selezionare il carico di lavoro](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="7eea2-161">Fare clic su **registrare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="7eea2-162">![Pulsante Registra](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="7eea2-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="7eea2-163">In hello **registrare elementi** menu di scelta rapida, hello selezionare le macchine virtuali che si desidera tooregister.</span><span class="sxs-lookup"><span data-stu-id="7eea2-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="7eea2-164">Se sono presenti due o più macchine virtuali con hello stesso nome, utilizzare toodistinguish servizio cloud di hello tra di essi.</span><span class="sxs-lookup"><span data-stu-id="7eea2-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="7eea2-165">È possibile registrare più macchine virtuali contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="7eea2-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="7eea2-166">Viene creato un processo per ogni macchina virtuale selezionata.</span><span class="sxs-lookup"><span data-stu-id="7eea2-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="7eea2-167">Fare clic su **Visualizza processo** in hello notifica toogo toohello **processi** pagina.</span><span class="sxs-lookup"><span data-stu-id="7eea2-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Registrare il processo](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="7eea2-169">macchina virtuale Hello viene visualizzato anche nell'elenco di hello degli elementi registrati, insieme allo stato di hello dell'operazione di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Registering status 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="7eea2-171">Al termine dell'operazione di hello, lo stato di hello cambia hello tooreflect *registrato* stato.</span><span class="sxs-lookup"><span data-stu-id="7eea2-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Registration status 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="7eea2-173">Passaggio 3: Proteggere le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7eea2-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="7eea2-174">Ora è possibile impostare un criterio di backup e memorizzazione per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="7eea2-175">È possibile proteggere più macchine virtuali usando una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="7eea2-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="7eea2-176">Azure insiemi di credenziali di Backup creati dopo maggio 2015 forniti con un criterio predefinito creato nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="7eea2-177">Questi criteri predefiniti prevedono un periodo di conservazione predefinito di 30 giorni e una pianificazione per il backup una volta al giorno.</span><span class="sxs-lookup"><span data-stu-id="7eea2-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="7eea2-178">Passare l'insieme di credenziali backup toohello in **servizi di ripristino** in hello portale di Azure e quindi fare clic su **elementi registrati**.</span><span class="sxs-lookup"><span data-stu-id="7eea2-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="7eea2-179">Selezionare **macchina virtuale di Azure** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Select workload in portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="7eea2-181">Fare clic su **PROTEGGI** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="7eea2-182">Hello **guidata proteggere elementi** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="7eea2-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="7eea2-183">procedura guidata di Hello Elenca solo le macchine virtuali che vengono registrate e non protetti.</span><span class="sxs-lookup"><span data-stu-id="7eea2-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="7eea2-184">Selezionare le macchine virtuali hello che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="7eea2-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="7eea2-185">Se sono presenti due o più macchine virtuali con hello stesso nome, utilizzare hello cloud servizio toodistinguish tra le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="7eea2-186">È possibile proteggere più macchine virtuali contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="7eea2-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Configurare la protezione su vasta scala](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="7eea2-188">Scegliere un **pianificazione del backup** tooback backup di macchine virtuali hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="7eea2-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="7eea2-189">È possibile scegliere da un set di criteri esistenti o definirne di nuovi.</span><span class="sxs-lookup"><span data-stu-id="7eea2-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="7eea2-190">Ai singoli criteri di backup possono essere associate più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7eea2-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="7eea2-191">Tuttavia, hello macchina virtuale può solo essere associato a un criterio in qualsiasi punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="7eea2-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Proteggere con nuovi criteri](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="7eea2-193">Un criterio di backup include uno schema di memorizzazione per i backup pianificato hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="7eea2-194">Se si seleziona un criterio di backup, è possibile modificare le opzioni di memorizzazione hello nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="7eea2-195">Scegliere un **mantenimento** tooassociate con backup hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![Proteggere con criteri di conservazione flessibili](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="7eea2-197">Criteri di conservazione specificano durata hello per archiviare un backup.</span><span class="sxs-lookup"><span data-stu-id="7eea2-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="7eea2-198">È possibile specificare i criteri di conservazione diversi in base a quando viene eseguito il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="7eea2-199">Ad esempio, un punto di backup eseguito quotidianamente, che funge da punto di ripristino operativo, può essere conservato per 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="7eea2-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="7eea2-200">In confronto, un punto di backup eseguito alla fine hello ogni trimestre (per motivi di controllo) potrebbe essere necessario toobe mantenuti per numero di mesi o anni.</span><span class="sxs-lookup"><span data-stu-id="7eea2-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![Virtual machine is backed up with recovery point](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="7eea2-202">In questa immagine di esempio:</span><span class="sxs-lookup"><span data-stu-id="7eea2-202">In this example image:</span></span>

   * <span data-ttu-id="7eea2-203">**Criteri di conservazione giornaliera**: i backup eseguiti ogni giorno vengono archiviati per 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="7eea2-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="7eea2-204">**Criteri di conservazione settimanale**: i backup eseguiti ogni domenica vengono conservati per 104 settimane.</span><span class="sxs-lookup"><span data-stu-id="7eea2-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="7eea2-205">**Criteri di conservazione mensile**: i backup eseguiti su hello ultima domenica di ogni mese vengono conservati per 120 mesi.</span><span class="sxs-lookup"><span data-stu-id="7eea2-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="7eea2-206">**Criteri di conservazione annuale**: i backup eseguiti su hello prima domenica di ogni mese di gennaio vengono mantenuti per 99 anni.</span><span class="sxs-lookup"><span data-stu-id="7eea2-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="7eea2-207">Un processo viene creato criteri di protezione tooconfigure hello e associare criteri di toothat hello macchine virtuali per ogni macchina virtuale selezionata.</span><span class="sxs-lookup"><span data-stu-id="7eea2-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="7eea2-208">elenco di hello tooview di **configurazione della protezione** processi, nel menu hello gli insiemi di credenziali, fare clic su **processi** e selezionare **configurazione della protezione** da hello **operazione ** filtro.</span><span class="sxs-lookup"><span data-stu-id="7eea2-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![Configure protection job](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="7eea2-210">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="7eea2-210">Initial backup</span></span>
<span data-ttu-id="7eea2-211">Una volta macchina virtuale hello è protetto con un criterio, viene visualizzata in hello **elementi protetti** scheda con stato hello *Protected - (in sospeso il backup iniziale)*.</span><span class="sxs-lookup"><span data-stu-id="7eea2-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="7eea2-212">Per impostazione predefinita, backup pianificato prima hello è hello *backup iniziale*.</span><span class="sxs-lookup"><span data-stu-id="7eea2-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="7eea2-213">backup iniziale hello di tootrigger immediatamente dopo la configurazione di protezione:</span><span class="sxs-lookup"><span data-stu-id="7eea2-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="7eea2-214">Nella parte inferiore di hello di hello **elementi protetti** pagina, fare clic su **Esegui Backup**.</span><span class="sxs-lookup"><span data-stu-id="7eea2-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="7eea2-215">Hello servizio Backup di Azure crea un processo di backup per l'operazione di backup iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="7eea2-216">Fare clic su hello **processi** elenco della scheda tooview hello dei processi.</span><span class="sxs-lookup"><span data-stu-id="7eea2-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Backup in progress](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="7eea2-218">Durante l'operazione di backup hello, hello servizio Backup di Azure esegue un'estensione di backup toohello comando in ogni macchina virtuale di tooflush tutti i processi di scrittura e uno snapshot coerente.</span><span class="sxs-lookup"><span data-stu-id="7eea2-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="7eea2-219">Al termine di backup iniziale hello, lo stato di hello della macchina virtuale hello in hello **elementi protetti** scheda *Protected*.</span><span class="sxs-lookup"><span data-stu-id="7eea2-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![Virtual machine is backed up with recovery point](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="7eea2-221">Visualizzazione dello stato di backup e dei relativi dettagli</span><span class="sxs-lookup"><span data-stu-id="7eea2-221">Viewing backup status and details</span></span>
<span data-ttu-id="7eea2-222">Una volta protetto, aumenta anche il numero di macchine virtuali hello hello **Dashboard** pagina riepilogo.</span><span class="sxs-lookup"><span data-stu-id="7eea2-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="7eea2-223">Hello **Dashboard** pagina mostra anche il numero di hello di processi da hello ultime 24 ore che sono stati *ha esito positivo*, hanno *Impossibile*e sono *in corso*.</span><span class="sxs-lookup"><span data-stu-id="7eea2-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="7eea2-224">In hello **processi** pagina, utilizzare hello **stato**, **operazione**, o **da** e **a** toofilter menu processi di Hello.</span><span class="sxs-lookup"><span data-stu-id="7eea2-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![Status of backup in Dashboard page](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="7eea2-226">I valori nel dashboard di hello vengono aggiornati una volta ogni 24 ore.</span><span class="sxs-lookup"><span data-stu-id="7eea2-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="7eea2-227">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="7eea2-227">Troubleshooting errors</span></span>
<span data-ttu-id="7eea2-228">Se si verificano problemi durante il backup la macchina virtuale, esaminare hello [articolo sulla risoluzione dei problemi di VM](backup-azure-vms-troubleshoot.md) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="7eea2-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eea2-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7eea2-229">Next steps</span></span>
* [<span data-ttu-id="7eea2-230">Gestire e monitorare il backup delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="7eea2-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="7eea2-231">Ripristino di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7eea2-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
