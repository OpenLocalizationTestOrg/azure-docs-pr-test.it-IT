---
title: 'Replicare macchine virtuali di Azure tra le aree di Azure per il ripristino di emergenza deve: tooAzure Azure | Documenti Microsoft'
description: "Vengono riepilogati i passaggi di hello è necessario tooreplicate macchine virtuali di Azure tra le aree di Azure (Azure in Azure) con il servizio di Azure Site Recovery hello per esigenze di ripristino di emergenza."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="f9bde-103">Eseguire la replica delle VM di Azure tra le aree con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f9bde-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="f9bde-104">La replica di Azure Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="f9bde-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="f9bde-105">In questo articolo viene descritto come tooreplicate macchine virtuali di Azure tra le aree di Azure tramite hello [Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bde-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="f9bde-106">Inviare commenti e domande nella parte inferiore di hello di questo articolo o di hello [forum di servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f9bde-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="f9bde-107">Ripristino di emergenza in Azure</span><span class="sxs-lookup"><span data-stu-id="f9bde-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="f9bde-108">Caratteristiche e funzionalità predefinite dell'infrastruttura di Azure contribuiscono tooa strategia di disponibilità solida e flessibile per carichi di lavoro eseguiti su macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bde-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="f9bde-109">Tuttavia, esistono molti motivi per cui è necessario tooplan per il ripristino di emergenza tra aree di Azure manualmente:</span><span class="sxs-lookup"><span data-stu-id="f9bde-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="f9bde-110">È necessario toomeet linee guida di conformità per App specifiche e i carichi di lavoro che richiedono un continuità aziendale e una strategia di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="f9bde-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="f9bde-111">Si desidera tooprotect possibilità hello e il ripristino macchine virtuali di Azure in base a quanto deciso business e non solo in base alle funzionalità di Azure incorporata.</span><span class="sxs-lookup"><span data-stu-id="f9bde-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="f9bde-112">È necessario tootest failover e il ripristino in base alle esigenze aziendali e di conformità, senza alcun impatto sulla produzione.</span><span class="sxs-lookup"><span data-stu-id="f9bde-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="f9bde-113">È necessario toofail rispetto all'area di ripristino toohello nell'evento hello un'emergenza ed esito negativo toohello indietro area di origine originale senza problemi.</span><span class="sxs-lookup"><span data-stu-id="f9bde-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="f9bde-114">Utilizzare il ripristino del sito per la macchina virtuale di Azure in Azure replica toohelp tutte queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="f9bde-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="f9bde-115">Perché usare Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="f9bde-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="f9bde-116">Il ripristino del sito fornisce un modo semplice di tooreplicate macchine virtuali di Azure tra aree:</span><span class="sxs-lookup"><span data-stu-id="f9bde-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="f9bde-117">**Distribuzione automatica**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-117">**Automatic deployment**.</span></span> <span data-ttu-id="f9bde-118">A differenza di un modello di replica attivo-attivo, non è necessario per un'infrastruttura dispendiosa e complessa nell'area secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="f9bde-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="f9bde-119">Quando si abilita la replica, il ripristino del sito vengono automaticamente create hello necessarie risorse nell'area di destinazione hello, in base alle impostazioni di area di origine.</span><span class="sxs-lookup"><span data-stu-id="f9bde-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="f9bde-120">**Aree di controllo**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-120">**Control regions**.</span></span> <span data-ttu-id="f9bde-121">Con il ripristino del sito, è possibile replicare da un'area di tooany area all'interno di un continente.</span><span class="sxs-lookup"><span data-stu-id="f9bde-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="f9bde-122">È possibile confrontare questo approccio con l'archiviazione con ridondanza geografica e accesso in lettura, che esegue la replica asincrona solo tra [aree abbinate](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span><span class="sxs-lookup"><span data-stu-id="f9bde-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="f9bde-123">Archiviazione con ridondanza geografica e accesso in lettura fornisce accesso in sola lettura toohello dati area di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="f9bde-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="f9bde-124">**Replica automatica**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-124">**Automated replication**.</span></span> <span data-ttu-id="f9bde-125">Site Recovery fornisce la replica continua automatica.</span><span class="sxs-lookup"><span data-stu-id="f9bde-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="f9bde-126">È possibile attivare il failover e il failback con un singolo clic.</span><span class="sxs-lookup"><span data-stu-id="f9bde-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="f9bde-127">**RTO e RPO**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-127">**RTO and RPO**.</span></span> <span data-ttu-id="f9bde-128">Il ripristino del sito si avvale dell'infrastruttura di rete di Azure hello che si connette aree tookeep obiettivi RTO e RPO molto bassa.</span><span class="sxs-lookup"><span data-stu-id="f9bde-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="f9bde-129">**Test**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-129">**Testing**.</span></span> <span data-ttu-id="f9bde-130">È possibile eseguire esercitazioni per il ripristino di emergenza con failover di test su richiesta, quando necessario, senza influire sui carichi di lavoro di produzione o sulla replica continua.</span><span class="sxs-lookup"><span data-stu-id="f9bde-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="f9bde-131">**Piani di ripristino**</span><span class="sxs-lookup"><span data-stu-id="f9bde-131">**Recovery plans**.</span></span> <span data-ttu-id="f9bde-132">È possibile utilizzare i failover tooorchestrate piani di ripristino e il failback di hello tutta l'applicazione in esecuzione su più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f9bde-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="f9bde-133">funzionalità del piano di ripristino Hello dispone di integrazione di prima classe completa con i runbook di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bde-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="f9bde-134">Riepilogo della distribuzione</span><span class="sxs-lookup"><span data-stu-id="f9bde-134">Deployment summary</span></span>

<span data-ttu-id="f9bde-135">Di seguito è riportato un riepilogo di ciò che è necessario tooset toodo la replica delle macchine virtuali tra aree di Azure:</span><span class="sxs-lookup"><span data-stu-id="f9bde-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="f9bde-136">Creare un insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f9bde-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="f9bde-137">insieme di credenziali Hello contiene le impostazioni di configurazione e Orchestra la replica.</span><span class="sxs-lookup"><span data-stu-id="f9bde-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="f9bde-138">Abilitare la replica per hello macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bde-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="f9bde-139">Eseguire un toomake di failover di test assicurarsi che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="f9bde-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="f9bde-140">È possibile controllare hello [matrice del supporto per la replica di macchina virtuale di Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f9bde-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="f9bde-141">Per informazioni su come tooconfigure hello necessaria la connettività di rete in uscita per le macchine virtuali di Azure per la replica di Site Recovery, vedere hello [rete fornite nel documento](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="f9bde-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="f9bde-142">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="f9bde-142">Before you start</span></span>

* <span data-ttu-id="f9bde-143">L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica della macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bde-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="f9bde-144">La sottoscrizione di Azure deve essere abilitato toocreate macchine virtuali nel percorso di destinazione hello che si desidera toouse come area di ripristino di emergenza hello.</span><span class="sxs-lookup"><span data-stu-id="f9bde-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="f9bde-145">Contattare il supporto tecnico tooenable hello quota obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f9bde-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f9bde-146">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="f9bde-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="f9bde-147">Si consiglia di creare credenziali di servizi di ripristino hello in hello percorso in cui tooreplicate le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f9bde-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="f9bde-148">Ad esempio, se il percorso di destinazione è hello central US, creare un archivio di hello in **centrale Usa**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="f9bde-149">Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="f9bde-149">Enable replication</span></span>

<span data-ttu-id="f9bde-150">In **insiemi di credenziali di servizi di ripristino**, fare clic sul nome dell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="f9bde-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="f9bde-151">Nell'insieme di credenziali hello, fare clic su hello **+ replicare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f9bde-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="f9bde-152">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="f9bde-152">Step 1.</span></span> <span data-ttu-id="f9bde-153">Configurare l'origine hello</span><span class="sxs-lookup"><span data-stu-id="f9bde-153">Configure hello source</span></span>
1. <span data-ttu-id="f9bde-154">In **Origine** selezionare **Azure - ANTEPRIMA**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="f9bde-155">In **percorso di origine**selezionare origine hello regione di Azure in cui le macchine virtuali attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f9bde-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="f9bde-156">Modello di distribuzione selezionare hello delle macchine virtuali: **Gestione risorse** o **classico**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="f9bde-157">Seleziona hello **il gruppo di risorse di origine** per le macchine virtuali di gestione risorse o **servizio cloud** per le macchine virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="f9bde-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configurare l'origine hello](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="f9bde-159">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="f9bde-159">Step 2.</span></span> <span data-ttu-id="f9bde-160">Selezionare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f9bde-160">Select virtual machines</span></span>

* <span data-ttu-id="f9bde-161">Selezionare le macchine virtuali hello desidera tooreplicate e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Selezionare le VM](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="f9bde-163">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="f9bde-163">Step 3.</span></span> <span data-ttu-id="f9bde-164">Configurare le impostazioni</span><span class="sxs-lookup"><span data-stu-id="f9bde-164">Configure settings</span></span>

1. <span data-ttu-id="f9bde-165">valore predefinito di hello toooverride le impostazioni di destinazione e specificare le impostazioni di hello di propria scelta, fare clic su **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="f9bde-166">Per altre informazioni, vedere [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources) (Personalizzare le risorse di destinazione).</span><span class="sxs-lookup"><span data-stu-id="f9bde-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Configurare le impostazioni](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="f9bde-168">Per impostazione predefinita, Site Recovery crea un criterio di replica che crea snapshot coerenti con l'app ogni 4 ore e conserva i punti di ripristino per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="f9bde-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="f9bde-169">toocreate criteri con impostazioni diverse, fare clic su **Personalizza** Avanti troppo**criteri di replica**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![Personalizzare i criteri](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="f9bde-171">Fare clic su risorse di destinazione hello provisioning toostart, **creare risorse di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="f9bde-172">Il provisioning richiede circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="f9bde-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="f9bde-173">Non chiudere il pannello hello durante il provisioning o è necessario toostart su.</span><span class="sxs-lookup"><span data-stu-id="f9bde-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="f9bde-174">replica tootrigger di hello selezionata VM, fare clic su **abilitare la replica**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="f9bde-175">È possibile monitorare lo stato di avanzamento di hello **abilitare la protezione** processo **impostazioni** > **processi** > **processi di ripristino del sito**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="f9bde-176">In **impostazioni** > **elementi replicati**, è possibile visualizzare lo stato di hello di macchine virtuali e hello stato della replica iniziale.</span><span class="sxs-lookup"><span data-stu-id="f9bde-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="f9bde-177">Fare clic su hello VM toodrill verso il basso nelle relative impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f9bde-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="f9bde-178">Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="f9bde-178">Run a test failover</span></span>

<span data-ttu-id="f9bde-179">Dopo aver configurato tutti gli elementi, eseguire una toomake di failover di test che tutto funzioni come previsto:</span><span class="sxs-lookup"><span data-stu-id="f9bde-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="f9bde-180">toofail su un singolo computer, in **impostazioni** > **elementi replicati**, fare clic su hello VM **+ Test Failover** icona.</span><span class="sxs-lookup"><span data-stu-id="f9bde-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="f9bde-181">toofail sul ripristino di un piano, in **impostazioni** > **piani di ripristino**, piano hello rapida **Failover di Test**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="f9bde-182">un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="f9bde-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="f9bde-183">In **Failover di Test**selezionare toowhich di rete virtuale di Azure di destinazione hello macchine virtuali di Azure sono connesse dopo il failover hello.</span><span class="sxs-lookup"><span data-stu-id="f9bde-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="f9bde-184">toostart hello failover, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="f9bde-185">tootrack sullo stato di avanzamento, fare clic su hello VM tooopen le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="f9bde-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="f9bde-186">Oppure è possibile fare clic su hello **Failover di Test** processo nel nome dell'insieme di credenziali hello > **impostazioni** > **processi** > **iprocessidiripristinodelsito**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="f9bde-187">Hello failover termine, replica hello macchina di Azure viene visualizzato nel portale di Azure hello > **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="f9bde-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="f9bde-188">Assicurarsi che tale hello VM sia di dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f9bde-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="f9bde-189">Fare clic su toodelete hello macchine virtuali che sono stati creati durante il failover di test hello, **il failover di test di pulizia** su hello replicati hello o elemento piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f9bde-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="f9bde-190">In **note**, registrare e salvare eventuali commenti associati hello test failover.</span><span class="sxs-lookup"><span data-stu-id="f9bde-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="f9bde-191">[Altre informazioni](site-recovery-test-failover-to-azure.md) sui failover di test.</span><span class="sxs-lookup"><span data-stu-id="f9bde-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f9bde-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9bde-192">Next steps</span></span>

<span data-ttu-id="f9bde-193">Dopo aver test distribuzione hello:</span><span class="sxs-lookup"><span data-stu-id="f9bde-193">After you test hello deployment:</span></span>

- <span data-ttu-id="f9bde-194">[Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e modalità toorun li.</span><span class="sxs-lookup"><span data-stu-id="f9bde-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="f9bde-195">Altre informazioni, vedere [utilizzando i piani di ripristino](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="f9bde-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
