---
title: 'Eseguire la replica di VM di Azure tra aree di Azure per esigenze di ripristino di emergenza: da Azure ad Azure| Microsoft Docs'
description: Riepiloga la procedura necessaria per la replica di VM di Azure tra aree di Azure (da Azure ad Azure) con il servizio Azure Site Recovery per esigenze di ripristino di emergenza.
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
ms.openlocfilehash: 9ca33057f6030fdcc233f6053fdc392d62f8f9f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="0fccc-103">Eseguire la replica delle VM di Azure tra le aree con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0fccc-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="0fccc-104">La replica di Azure Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="0fccc-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="0fccc-105">Questo articolo illustra come eseguire la replica delle VM di Azure tra aree di Azure mediante il servizio [Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fccc-105">This article describes how to replicate Azure VMs between Azure regions by using the [Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="0fccc-106">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum su Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0fccc-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="0fccc-107">Ripristino di emergenza in Azure</span><span class="sxs-lookup"><span data-stu-id="0fccc-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="0fccc-108">Le funzionalità dell'infrastruttura e le funzionalità di Azure predefinite consentono di ottenere una strategia di disponibilità affidabile e resiliente per i carichi di lavoro in esecuzione nelle VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fccc-108">Built-in Azure infrastructure capabilities and features contribute to a robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="0fccc-109">È tuttavia necessario pianificare in modo autonomo il ripristino di emergenza tra aree di Azure per diversi motivi:</span><span class="sxs-lookup"><span data-stu-id="0fccc-109">However, there are many reasons why you need to plan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="0fccc-110">È necessario soddisfare le indicazioni di conformità per app e carichi di lavoro specifici che richiedono una strategia BCDR (Business Continuity and Disaster Recovery).</span><span class="sxs-lookup"><span data-stu-id="0fccc-110">You need to meet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="0fccc-111">Si vogliono proteggere e ripristinare le VM di Azure in base alle decisioni aziendali specifiche e non solo in base alle funzionalità predefinite di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fccc-111">You want the ability to protect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="0fccc-112">È necessario testare il failover e il ripristino in base alle esigenze aziendali e di conformità, senza impatti sulla produzione.</span><span class="sxs-lookup"><span data-stu-id="0fccc-112">You need to test failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="0fccc-113">È necessario eseguire il failover nell'area di ripristino in caso di disastro ed eseguire il failback all'area di origine originale senza problemi.</span><span class="sxs-lookup"><span data-stu-id="0fccc-113">You need to fail over to the recovery region in the event of a disaster and fail back to the original source region seamlessly.</span></span>

<span data-ttu-id="0fccc-114">Usare Site Recovery per la replica di VM da Azure ad Azure per semplificare l'esecuzione di tutte queste attività.</span><span class="sxs-lookup"><span data-stu-id="0fccc-114">Use Site Recovery for Azure-to-Azure VM replication to help you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="0fccc-115">Perché usare Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="0fccc-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="0fccc-116">Site Recovery offre un modo semplice per eseguire la replica di VM di Azure tra le aree:</span><span class="sxs-lookup"><span data-stu-id="0fccc-116">Site Recovery provides a simple way to replicate Azure VMs between regions:</span></span>

- <span data-ttu-id="0fccc-117">**Distribuzione automatica**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-117">**Automatic deployment**.</span></span> <span data-ttu-id="0fccc-118">A differenza di un modello di replica attivo-attivo, non è necessaria alcuna infrastruttura costosa e complessa nell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="0fccc-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in the secondary region.</span></span> <span data-ttu-id="0fccc-119">Quando si abilita la replica, Site Recovery crea automaticamente le risorse necessarie nell'area di destinazione, in base alle impostazioni dell'area di origine.</span><span class="sxs-lookup"><span data-stu-id="0fccc-119">When you enable replication, Site Recovery automatically creates the required resources in the target region, based on source region settings.</span></span>
- <span data-ttu-id="0fccc-120">**Aree di controllo**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-120">**Control regions**.</span></span> <span data-ttu-id="0fccc-121">Con Site Recovery è possibile eseguire la replica da qualsiasi area a qualsiasi area in un continente specifico.</span><span class="sxs-lookup"><span data-stu-id="0fccc-121">With Site Recovery, you can replicate from any region to any region within a continent.</span></span> <span data-ttu-id="0fccc-122">È possibile confrontare questo approccio con l'archiviazione con ridondanza geografica e accesso in lettura, che esegue la replica asincrona solo tra [aree abbinate](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span><span class="sxs-lookup"><span data-stu-id="0fccc-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="0fccc-123">L'archiviazione con ridondanza geografica e accesso in lettura fornisce l'accesso di sola lettura ai dati nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0fccc-123">Read-access geo-redundant storage provides read-only access to the data in the target region.</span></span>
- <span data-ttu-id="0fccc-124">**Replica automatica**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-124">**Automated replication**.</span></span> <span data-ttu-id="0fccc-125">Site Recovery fornisce la replica continua automatica.</span><span class="sxs-lookup"><span data-stu-id="0fccc-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="0fccc-126">È possibile attivare il failover e il failback con un singolo clic.</span><span class="sxs-lookup"><span data-stu-id="0fccc-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="0fccc-127">**RTO e RPO**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-127">**RTO and RPO**.</span></span> <span data-ttu-id="0fccc-128">Site Recovery sfrutta i vantaggi dell'infrastruttura di rete di Azure che connette le aree per mantenere valori di RTO e RPO molto bassi.</span><span class="sxs-lookup"><span data-stu-id="0fccc-128">Site Recovery takes advantage of the Azure network infrastructure that connects regions to keep RTO and RPO very low.</span></span>
- <span data-ttu-id="0fccc-129">**Test**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-129">**Testing**.</span></span> <span data-ttu-id="0fccc-130">È possibile eseguire esercitazioni per il ripristino di emergenza con failover di test su richiesta, quando necessario, senza influire sui carichi di lavoro di produzione o sulla replica continua.</span><span class="sxs-lookup"><span data-stu-id="0fccc-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="0fccc-131">**Piani di ripristino**</span><span class="sxs-lookup"><span data-stu-id="0fccc-131">**Recovery plans**.</span></span> <span data-ttu-id="0fccc-132">È possibile usare i piani di ripristino per orchestrare il failover e il failback dell'intera applicazione in esecuzione in più VM.</span><span class="sxs-lookup"><span data-stu-id="0fccc-132">You can use recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="0fccc-133">La funzionalità del piano di ripristino include l'integrazione di qualità elevata con i runbook di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fccc-133">The recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="0fccc-134">Riepilogo della distribuzione</span><span class="sxs-lookup"><span data-stu-id="0fccc-134">Deployment summary</span></span>

<span data-ttu-id="0fccc-135">Ecco un riepilogo delle operazioni necessarie per la configurazione della replica di VM tra le aree di Azure:</span><span class="sxs-lookup"><span data-stu-id="0fccc-135">Here's a summary of what you need to do to set up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="0fccc-136">Creare un insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fccc-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="0fccc-137">L'insieme di credenziali contiene le impostazioni di configurazione e orchestra la replica.</span><span class="sxs-lookup"><span data-stu-id="0fccc-137">The vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="0fccc-138">Abilitare la replica per le VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fccc-138">Enable replication for the Azure VMs.</span></span>
3. <span data-ttu-id="0fccc-139">Eseguire un failover di test per verificare che tutti gli elementi funzionino come previsto.</span><span class="sxs-lookup"><span data-stu-id="0fccc-139">Run a test failover to make sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="0fccc-140">È possibile controllare la [matrice di supporto per la replica di VM di Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0fccc-140">You can check the [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="0fccc-141">Per informazioni su come configurare la connettività di rete in uscita necessaria per le VM di Azure per la replica con Site Recovery, vedere il [documento di indicazioni sulla rete](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="0fccc-141">For information on how to configure the required network outbound connectivity for Azure VMs for Site Recovery replication, see the [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="0fccc-142">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0fccc-142">Before you start</span></span>

* <span data-ttu-id="0fccc-143">L'account utente di Azure deve avere determinate [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) per abilitare la replica di una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0fccc-143">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="0fccc-144">È necessario che la sottoscrizione di Azure sia abilitata per la creazione di VM nella posizione di destinazione da usare come area per il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="0fccc-144">Your Azure subscription should be enabled to create VMs in the target location that you want to use as the disaster recovery region.</span></span> <span data-ttu-id="0fccc-145">Contattare il supporto tecnico per abilitare la quota necessaria.</span><span class="sxs-lookup"><span data-stu-id="0fccc-145">Contact support to enable the required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="0fccc-146">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="0fccc-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="0fccc-147">È consigliabile creare l'insieme di credenziali dei servizi di ripristino nella posizione in cui si vuole che vengano replicate le VM.</span><span class="sxs-lookup"><span data-stu-id="0fccc-147">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="0fccc-148">Ad esempio, se la posizione di destinazione è Stati Uniti centrali, creare l'insieme di credenziali in **Stati Uniti centrali**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-148">For example, if your target location is the central US, create the vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="0fccc-149">Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="0fccc-149">Enable replication</span></span>

<span data-ttu-id="0fccc-150">In **Insiemi di credenziali dei servizi di ripristino** selezionare il nome dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="0fccc-150">In **Recovery Services vaults**, click the vault name.</span></span> <span data-ttu-id="0fccc-151">Nell'insieme di credenziali fare clic sul pulsante **+Replica**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-151">In the vault, click the **+Replicate** button.</span></span>

### <a name="step-1-configure-the-source"></a><span data-ttu-id="0fccc-152">Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="0fccc-152">Step 1.</span></span> <span data-ttu-id="0fccc-153">Configurare l'origine</span><span class="sxs-lookup"><span data-stu-id="0fccc-153">Configure the source</span></span>
1. <span data-ttu-id="0fccc-154">In **Origine** selezionare **Azure - ANTEPRIMA**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="0fccc-155">In **Percorso di origine** selezionare l'area di Azure di origine in cui le VM sono attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0fccc-155">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="0fccc-156">Selezionare il modello di distribuzione delle VM: **Resource Manager** o **Classica**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-156">Select the deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="0fccc-157">Selezionare il **Source resource group** (Gruppo di risorse di origine) per VM di tipo Resource Manager o **Servizio cloud** per le VM classiche.</span><span class="sxs-lookup"><span data-stu-id="0fccc-157">Select the **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configurare l'origine](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="0fccc-159">Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="0fccc-159">Step 2.</span></span> <span data-ttu-id="0fccc-160">Selezionare le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="0fccc-160">Select virtual machines</span></span>

* <span data-ttu-id="0fccc-161">Selezionare le VM da replicare e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-161">Select the VMs you want to replicate, and then click **OK**.</span></span>

    ![Selezionare le VM](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="0fccc-163">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="0fccc-163">Step 3.</span></span> <span data-ttu-id="0fccc-164">Configurare le impostazioni</span><span class="sxs-lookup"><span data-stu-id="0fccc-164">Configure settings</span></span>

1. <span data-ttu-id="0fccc-165">Per eseguire l'override delle impostazioni di destinazione predefinite e specificare le impostazioni da usare, fare clic su **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-165">To override the default target settings and specify the settings of your choice, click **Customize**.</span></span> <span data-ttu-id="0fccc-166">Per altre informazioni, vedere [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources) (Personalizzare le risorse di destinazione).</span><span class="sxs-lookup"><span data-stu-id="0fccc-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Configurare le impostazioni](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="0fccc-168">Per impostazione predefinita, Site Recovery crea un criterio di replica che crea snapshot coerenti con l'app ogni 4 ore e conserva i punti di ripristino per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="0fccc-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="0fccc-169">Per creare un criterio con impostazioni diverse, fare clic su **Personalizza** accanto a **Criteri di replica**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-169">To create a policy with different settings, click **Customize** next to **Replication Policy**.</span></span>

    ![Personalizzare i criteri](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="0fccc-171">Per avviare il provisioning delle risorse di destinazione, fare clic su **Create target resources** (Crea risorse di destinazione).</span><span class="sxs-lookup"><span data-stu-id="0fccc-171">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="0fccc-172">Il provisioning richiede circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="0fccc-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="0fccc-173">Non chiudere il pannello durante il provisioning, altrimenti sarà necessario ripetere l'operazione.</span><span class="sxs-lookup"><span data-stu-id="0fccc-173">Don't close the blade during provisioning, or you need to start over.</span></span>

4. <span data-ttu-id="0fccc-174">Per attivare la replica della VM selezionata, fare clic su **Abilita replica**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-174">To trigger replication of the selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="0fccc-175">È possibile tenere traccia dello stato del processo **Abilita protezione** in **Impostazioni** > **Processi** > **Processi di Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-175">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="0fccc-176">In **Impostazioni** > **Elementi replicati** è possibile visualizzare lo stato delle VM e lo stato della replica iniziale.</span><span class="sxs-lookup"><span data-stu-id="0fccc-176">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="0fccc-177">Fare clic sulla VM per visualizzare nel dettaglio le rispettive impostazioni.</span><span class="sxs-lookup"><span data-stu-id="0fccc-177">Click the VM to drill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="0fccc-178">Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="0fccc-178">Run a test failover</span></span>

<span data-ttu-id="0fccc-179">Dopo aver completato la configurazione, eseguire un failover di test per verificare che tutti gli elementi funzionino come previsto.</span><span class="sxs-lookup"><span data-stu-id="0fccc-179">After you set up everything, run a test failover to make sure everything's working as expected:</span></span>

1. <span data-ttu-id="0fccc-180">Per eseguire il failover di una singola macchina, in **Impostazioni** > **Elementi replicati** fare clic sulla VM e quindi sull'icona **+Failover di test**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-180">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="0fccc-181">Per eseguire il failover di un piano di ripristino, in **Impostazioni** > **Piani di ripristino** fare clic con il pulsante destro del mouse sul piano e quindi scegliere **Failover di test**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-181">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan **Test Failover**.</span></span> <span data-ttu-id="0fccc-182">Per creare un piano di ripristino, [seguire queste istruzioni](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="0fccc-182">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="0fccc-183">In **Failover di test** selezionare la rete virtuale di Azure di destinazione a cui si connetteranno le VM di Azure dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="0fccc-183">In **Test Failover**, select the target Azure virtual network to which Azure VMs are connected after the failover occurs.</span></span>

4. <span data-ttu-id="0fccc-184">Per avviare il failover, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-184">To start the failover, click **OK**.</span></span> <span data-ttu-id="0fccc-185">Per verificare lo stato dell'operazione, fare clic sulla VM per visualizzare le rispettive proprietà.</span><span class="sxs-lookup"><span data-stu-id="0fccc-185">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="0fccc-186">In alternativa, è possibile fare clic sul processo **Failover di test** nel nome dell'insieme di credenziali, quindi su **Impostazioni** > **Processi** > **Site Recovery jobs** (Processi di Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="0fccc-186">Or you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="0fccc-187">Al termine del failover, la macchina virtuale di Azure di replica viene visualizzata nel portale di Azure in **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="0fccc-187">After the failover finishes, the replica Azure machine appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="0fccc-188">Verificare che la macchina virtuale sia delle dimensioni appropriate, che sia connessa alla rete giusta e che sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0fccc-188">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="0fccc-189">Per eliminare le VM create durante il failover di test, fare clic su **Cleanup test failover** (Pulizia failover di test) nell'elemento replicato o nel piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0fccc-189">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="0fccc-190">Fare clic su **Note** per registrare e salvare eventuali osservazioni associate al failover di test.</span><span class="sxs-lookup"><span data-stu-id="0fccc-190">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="0fccc-191">[Altre informazioni](site-recovery-test-failover-to-azure.md) sui failover di test.</span><span class="sxs-lookup"><span data-stu-id="0fccc-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0fccc-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0fccc-192">Next steps</span></span>

<span data-ttu-id="0fccc-193">Al termine del test della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="0fccc-193">After you test the deployment:</span></span>

- <span data-ttu-id="0fccc-194">Altre informazioni sui diversi tipi di failover e su come eseguirli sono disponibili [qui](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="0fccc-194">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="0fccc-195">Altre informazioni sull'[uso dei piani di ripristino](site-recovery-create-recovery-plans.md) per la riduzione di RTO.</span><span class="sxs-lookup"><span data-stu-id="0fccc-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
