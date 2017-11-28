---
title: la replica aaaEnable per macchine virtuali di Azure tooanother area di Azure con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello tooenable replica tooanother area di Azure è necessario per le macchine virtuali di Azure, tramite il servizio di Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="c5a40-103">Passaggio 5: Abilitare la replica per le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="c5a40-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="c5a40-104">Dopo aver impostato un [insieme di credenziali di servizi di ripristino](azure-to-azure-walkthrough-vault.md), utilizzare la replica tooenable articolo macchine virtuali (VM), tooanother area di Azure con [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c5a40-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="c5a40-105">replica tooenable, è possibile impostare le impostazioni di origine e di destinazione, verificare i criteri di replica hello e selezionare le macchine virtuali desiderate tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="c5a40-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="c5a40-106">Una volta terminato l'articolo hello, le macchine virtuali di Azure deve essere la replica toohello area secondaria di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5a40-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="c5a40-107">Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="c5a40-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="c5a40-108">La replica di macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="c5a40-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="c5a40-109">Selezionare l'origine hello</span><span class="sxs-lookup"><span data-stu-id="c5a40-109">Select hello source</span></span> 

1. <span data-ttu-id="c5a40-110">In insiemi di credenziali di servizi di ripristino, fare clic sul nome dell'insieme di credenziali di hello > **+ replicare**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="c5a40-111">In **Origine** selezionare **Azure - ANTEPRIMA**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="c5a40-112">In **percorso di origine**selezionare origine hello regione di Azure in cui le macchine virtuali attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c5a40-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="c5a40-113">Seleziona hello **il modello di distribuzione di macchina virtuale di Azure** per le macchine virtuali: **Gestione risorse** o **classico**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="c5a40-114">Seleziona hello **il gruppo di risorse di origine** per Gestione risorse di macchine virtuali o **servizio cloud** per le macchine virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="c5a40-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="c5a40-115">Fare clic su **OK** impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="c5a40-115">Click **OK** toosave hello settings.</span></span>

    ![Configurare l'origine hello](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="c5a40-117">Selezionare le macchine virtuali hello</span><span class="sxs-lookup"><span data-stu-id="c5a40-117">Select hello VMs</span></span>

<span data-ttu-id="c5a40-118">Il ripristino del sito recupera un elenco di macchine virtuali associate alla sottoscrizione hello e risorse gruppo/servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="c5a40-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="c5a40-119">In **macchine virtuali**, selezionare le macchine virtuali hello desiderato tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="c5a40-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="c5a40-120">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-120">Click **OK**.</span></span>

    ![Selezionare le VM](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="c5a40-122">Configurare le impostazioni</span><span class="sxs-lookup"><span data-stu-id="c5a40-122">Configure settings</span></span>

<span data-ttu-id="c5a40-123">Le impostazioni predefinite per l'area di destinazione hello (in base alle impostazioni area di origine hello), esegue il provisioning di Site Recovery e il criterio di replica hello:</span><span class="sxs-lookup"><span data-stu-id="c5a40-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="c5a40-124">**Percorso di destinazione**: area di destinazione hello desiderate toouse per il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="c5a40-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="c5a40-125">È consigliabile che il percorso di destinazione hello corrisponda percorso hello dell'insieme di credenziali di Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="c5a40-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="c5a40-126">**Il gruppo di risorse di destinazione**: gruppo di risorse toowhich macchine virtuali di Azure nell'area di destinazione hello apparterrà dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="c5a40-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="c5a40-127">Per impostazione predefinita, il ripristino del sito viene creato un nuovo gruppo di risorse nell'area di destinazione hello con un suffisso "asr".</span><span class="sxs-lookup"><span data-stu-id="c5a40-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="c5a40-128">**Rete virtuale di destinazione**: rete hello in cui le macchine virtuali di Azure in hello area di destinazione sarà posizionato dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="c5a40-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="c5a40-129">Per impostazione predefinita, il ripristino del sito crea una nuova rete virtuale (e le subnet) nell'area di destinazione hello con un suffisso "asr".</span><span class="sxs-lookup"><span data-stu-id="c5a40-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="c5a40-130">Questa rete è mappata tooyour rete di origine.</span><span class="sxs-lookup"><span data-stu-id="c5a40-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="c5a40-131">Si noti che è possibile assegnare un indirizzo IP specifico dopo il failover di una macchina virtuale, se è necessario tooretain hello stesso indirizzo IP in posizioni di origine e destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="c5a40-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="c5a40-132">**Memorizzare nella cache gli account di archiviazione**: il ripristino del sito Usa un account di archiviazione nell'area di origine hello.</span><span class="sxs-lookup"><span data-stu-id="c5a40-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="c5a40-133">Le modifiche apportate nelle macchine virtuali di origine vengono inviate toothis account, prima di percorso di destinazione di replica toohello.</span><span class="sxs-lookup"><span data-stu-id="c5a40-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="c5a40-134">**Gli account di archiviazione di destinazione**: per impostazione predefinita, il ripristino del sito viene creato un nuovo account di archiviazione nell'area di destinazione hello, origine hello toomirror account di archiviazione macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5a40-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="c5a40-135">**Set di disponibilità di destinazione**: per impostazione predefinita, il ripristino del sito viene creato un nuovo set di disponibilità in area di destinazione hello, con il suffisso "asr" hello.</span><span class="sxs-lookup"><span data-stu-id="c5a40-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="c5a40-136">**Nome del criterio di replica**: nome del criterio.</span><span class="sxs-lookup"><span data-stu-id="c5a40-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="c5a40-137">**Conservazione del punto di ripristino**: per impostazione predefinita, Site Recovery conserva i punti di ripristino per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="c5a40-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="c5a40-138">È possibile configurare un valore compreso tra 1 e 72 ore.</span><span class="sxs-lookup"><span data-stu-id="c5a40-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="c5a40-139">**Frequenza snapshot coerenti con l'app**: per impostazione predefinita, Site Recovery accetta uno snapshot coerente con l'app ogni 4 ore.</span><span class="sxs-lookup"><span data-stu-id="c5a40-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="c5a40-140">È possibile configurare un valore compreso tra 1 e 12 ore.</span><span class="sxs-lookup"><span data-stu-id="c5a40-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="c5a40-141">I dati vengono replicati in modo continuo:</span><span class="sxs-lookup"><span data-stu-id="c5a40-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="c5a40-142">I punti di ripristino coerenti con l'arresto anomalo conservano un ordine di scrittura dati coerente, se creati.</span><span class="sxs-lookup"><span data-stu-id="c5a40-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="c5a40-143">Questo tipo di punto di ripristino è in genere sufficiente se l'applicazione viene progettata toorecover dopo un arresto anomalo senza incoerenze dei dati</span><span class="sxs-lookup"><span data-stu-id="c5a40-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="c5a40-144">I punti di ripristino coerenti con l'arresto anomalo vengono generati ogni pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="c5a40-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="c5a40-145">Tramite questi toofail punti di ripristino su e ripristinare le macchine virtuali fornisce un obiettivo del punto di ripristino (RPO) in ordine di hello di minuti.</span><span class="sxs-lookup"><span data-stu-id="c5a40-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="c5a40-146">Punti di ripristino coerenti con l'App (in coerenza toowrite ordine di aggiunta) verificare che le applicazioni in esecuzione completare tutte le operazioni e scaricare i buffer toodisk (disattivazione dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="c5a40-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="c5a40-147">È consigliabile usare questi punti di ripristino per le app di database come Exchange, Oracle e SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c5a40-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Configurare le impostazioni](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="c5a40-149">Modificare le impostazioni</span><span class="sxs-lookup"><span data-stu-id="c5a40-149">Modify settings</span></span>

<span data-ttu-id="c5a40-150">Se si desiderano impostazioni di criteri di replica e di destinazione toomodify, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5a40-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="c5a40-151">tooview o modificare le impostazioni di destinazione, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="c5a40-152">Fare clic su impostazioni di destinazione predefinito hello toooverride, **Personalizza**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="c5a40-153">È possibile specificare un gruppo di risorse di destinazione, una rete virtuale, un set di disponibilità e account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c5a40-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="c5a40-154">Se le macchine virtuali fanno parte di un set nell'area di origine hello, è possibile aggiungere solo i set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c5a40-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![Configurare le impostazioni](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="c5a40-156">Fare clic su impostazioni di replica toooverride per i punti di ripristino e gli snapshot coerenti con l'app, **Personalizza** Avanti troppo**criteri di replica**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![Configurare le impostazioni](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="c5a40-158">Fare clic su risorse di destinazione hello provisioning toostart, **creare risorse di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="c5a40-159">Il provisioning richiede circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="c5a40-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="c5a40-160">Non chiudere il pannello hello durante il provisioning o avrai toostart su.</span><span class="sxs-lookup"><span data-stu-id="c5a40-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="c5a40-161">Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="c5a40-161">Enable replication</span></span>

1. <span data-ttu-id="c5a40-162">In **Impostazioni** fare clic su **Abilita replica**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="c5a40-163">In questo modo la replica iniziale di hello macchine virtuali è stata selezionata.</span><span class="sxs-lookup"><span data-stu-id="c5a40-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="c5a40-164">Lo stato della replica iniziale potrebbe richiedere alcuni toorefresh ora.</span><span class="sxs-lookup"><span data-stu-id="c5a40-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="c5a40-165">Fare clic su **aggiornamento** tooget stato più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="c5a40-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="c5a40-166">È possibile monitorare lo stato di avanzamento di hello **abilitare la protezione** processo **impostazioni** > **processi** > **processi di ripristino del sito**.</span><span class="sxs-lookup"><span data-stu-id="c5a40-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="c5a40-167">In **impostazioni** > **elementi replicati**, è possibile visualizzare lo stato di hello di macchine virtuali e hello stato della replica iniziale.</span><span class="sxs-lookup"><span data-stu-id="c5a40-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="c5a40-168">Fare clic su hello VM toodrill verso il basso nelle relative impostazioni.</span><span class="sxs-lookup"><span data-stu-id="c5a40-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c5a40-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5a40-169">Next steps</span></span>

<span data-ttu-id="c5a40-170">Andare troppo[passaggio 6: eseguire un failover di test](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="c5a40-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
