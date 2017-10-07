---
title: applicazioni aaaReplicate (Azure tooAzure) | Documenti Microsoft
description: In questo articolo viene descritto come tooset la replica di virtuale dei computer in esecuzione in un'area di Azure troppo un'altra area in Azure.
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="1535d-103">Replicare macchine virtuali di Azure tooanother area di Azure</span><span class="sxs-lookup"><span data-stu-id="1535d-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="1535d-104">La replica di Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="1535d-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="1535d-105">In questo articolo viene descritto come tooset la replica di virtuale dei computer in esecuzione in una regione di Azure tooanother area di Azure.</span><span class="sxs-lookup"><span data-stu-id="1535d-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1535d-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1535d-106">Prerequisites</span></span>

* <span data-ttu-id="1535d-107">Hello si presume che già si conoscono le Site Recovery e l'insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="1535d-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="1535d-108">È necessario toohave una versione preliminare 'Insieme di credenziali Recovery services' creata.</span><span class="sxs-lookup"><span data-stu-id="1535d-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="1535d-109">È consigliabile creare hello 'Insieme di credenziali Recovery services' nel percorso di hello in cui si desidera tooreplicate le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1535d-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="1535d-110">Ad esempio, se la posizione di destinazione è "Stati Uniti centrali", creare l'insieme di credenziali in "Stati Uniti centrali".</span><span class="sxs-lookup"><span data-stu-id="1535d-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="1535d-111">Se si utilizzano le regole di sicurezza gruppi (rete) o la connettività internet di firewall proxy toocontrol accesso toooutbound hello macchine virtuali di Azure, verificare che hello di whitelist è richiesta la URL o gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="1535d-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="1535d-112">Fare riferimento troppo[rete fornite nel documento](./site-recovery-azure-to-azure-networking-guidance.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="1535d-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="1535d-113">Se si dispone di ExpressRoute o una connessione VPN tra sedi locali e hello in Azure percorso di origine, seguire [considerazioni sul ripristino del sito per locale tooon Azure ExpressRoute o configurazione VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) documento.</span><span class="sxs-lookup"><span data-stu-id="1535d-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="1535d-114">L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica della macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1535d-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="1535d-115">La sottoscrizione di Azure deve essere abilitato toocreate VM nel percorso di destinazione hello desiderato toouse come area di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="1535d-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="1535d-116">Contattare il supporto tooenable hello obbligatorio quota.</span><span class="sxs-lookup"><span data-stu-id="1535d-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="1535d-117">Abilitare la replica dall'insieme di credenziali di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1535d-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="1535d-118">Per questa illustrazione, si eseguirà la replica di macchine virtuali in esecuzione in toohello di località di Azure "Asia orientale" hello ' sud-est asiatico ' percorso.</span><span class="sxs-lookup"><span data-stu-id="1535d-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="1535d-119">come indicato di seguito sono riportati i passaggi di Hello:</span><span class="sxs-lookup"><span data-stu-id="1535d-119">hello steps are as follows:</span></span>

 <span data-ttu-id="1535d-120">Fare clic su **+ replicare** nella replica di tooenable hello insieme di credenziali per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="1535d-121">**Origine:** fa toohello punto di origine delle macchine di hello, che in questo caso è **Azure**.</span><span class="sxs-lookup"><span data-stu-id="1535d-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="1535d-122">**Percorso di origine:** è hello area in cui si desidera tooprotect le macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="1535d-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="1535d-123">Per questa figura, il percorso di origine hello sarà "Asia orientale"</span><span class="sxs-lookup"><span data-stu-id="1535d-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="1535d-124">**Modello di distribuzione:** fa riferimento al modello di distribuzione di Azure toohello dei computer di origine hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="1535d-125">È possibile selezionare entrambi classica o Gestione risorse di computer appartenenti a modello specifico toohello viene elencato per la protezione nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="1535d-126">È possibile eseguire la replica di una macchina virtuale classica e ripristinarla solo come macchina virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="1535d-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="1535d-127">Non è possibile ripristinarla come macchina virtuale di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1535d-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="1535d-128">**Gruppo di risorse:** del toowhich gruppo di risorse hello appartengono le macchine virtuali di origine.</span><span class="sxs-lookup"><span data-stu-id="1535d-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="1535d-129">Verrà elencati per la protezione nel passaggio successivo hello hello tutte le macchine virtuali nel gruppo di risorse selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="1535d-131">In **macchine virtuali > macchine virtuali selezionare**, fare clic su e selezionare ciascuna macchina da tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="1535d-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="1535d-132">È possibile selezionare solo i computer per cui è possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="1535d-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="1535d-133">Fare quindi clic su OK.</span><span class="sxs-lookup"><span data-stu-id="1535d-133">Then click OK.</span></span>
    <span data-ttu-id="1535d-134">![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="1535d-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="1535d-135">Nella sezione Impostazioni è possibile configurare le proprietà del sito di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1535d-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="1535d-136">**Percorso di destinazione:** hello posizione in cui verranno replicati i dati di macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="1535d-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="1535d-137">In base al percorso di macchine virtuali selezionate, il ripristino del sito verrà fornito che Hello elenco delle aree di destinazione appropriato.</span><span class="sxs-lookup"><span data-stu-id="1535d-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="1535d-138">È consigliabile il percorso di destinazione tookeep stesso al momento del ripristino dell'insieme di credenziali dei servizi.</span><span class="sxs-lookup"><span data-stu-id="1535d-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="1535d-139">**Il gruppo di risorse di destinazione:** è hello toowhich di gruppo di risorse al quale apparterrà tutte le macchine virtuali replicate. Per impostazione predefinita ASR creerà un nuovo gruppo di risorse nell'area di destinazione hello con nome con il suffisso "asr".</span><span class="sxs-lookup"><span data-stu-id="1535d-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="1535d-140">Nel caso in cui il gruppo di risorse creato da ASR già esiste, verrà riutilizzata. È anche possibile scegliere toocustomize, come illustrato nella sezione hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="1535d-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="1535d-141">**Rete virtuale di destinazione:** per impostazione predefinita, ripristino automatico di sistema creerà una nuova rete virtuale nell'area di destinazione hello con nome con il suffisso "asr".</span><span class="sxs-lookup"><span data-stu-id="1535d-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="1535d-142">Questa sarà la rete di origine mappata tooyour e verrà utilizzata per alcuna protezione future.</span><span class="sxs-lookup"><span data-stu-id="1535d-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1535d-143">[Controllare i dettagli rete](site-recovery-network-mapping-azure-to-azure.md) tooknow ulteriori informazioni sul mapping di rete.</span><span class="sxs-lookup"><span data-stu-id="1535d-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="1535d-144">**Gli account di archiviazione di destinazione:** per impostazione predefinita, creerà hello nuova destinazione account di archiviazione che rispecchia la configurazione di archiviazione macchina virtuale di origine ripristino automatico di sistema.</span><span class="sxs-lookup"><span data-stu-id="1535d-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="1535d-145">Nel caso in cui l'account di archiviazione creato da Azure Site Recovery esista già, verrà riutilizzato.</span><span class="sxs-lookup"><span data-stu-id="1535d-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="1535d-146">**Memorizzare nella cache gli account di archiviazione:** ASR richiede account di archiviazione aggiuntiva denominata archiviazione cache nell'area di origine hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="1535d-147">Tutti hello modifiche che si verifichi hello macchine virtuali di origine vengono monitorate e inviate toocache account di archiviazione prima di replicare questi percorso di destinazione toohello.</span><span class="sxs-lookup"><span data-stu-id="1535d-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="1535d-148">**Set di disponibilità:** per impostazione predefinita, creerà un nuovo set di disponibilità nell'area di destinazione hello con nome con il suffisso "asr" Ripristino automatico di sistema.</span><span class="sxs-lookup"><span data-stu-id="1535d-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="1535d-149">Nel caso in cui il set di disponibilità creato da Azure Site Recovery esista già, verrà riutilizzato.</span><span class="sxs-lookup"><span data-stu-id="1535d-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="1535d-150">**Criteri di replica:** definisce le impostazioni per ripristino punto di memorizzazione della cronologia e app snapshot coerente con la frequenza di hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="1535d-151">Per impostazione predefinita, Azure Site Recovery creerà un nuovo criterio di replica con impostazioni predefiniti di "24 ore" per la conservazione del punto di ripristino e di "60 minuti" per la frequenza snapshot coerenti con l'app.</span><span class="sxs-lookup"><span data-stu-id="1535d-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="1535d-153">Personalizzare le risorse di destinazione</span><span class="sxs-lookup"><span data-stu-id="1535d-153">Customize target resources</span></span>

<span data-ttu-id="1535d-154">Nel caso in cui si desidera impostazioni predefinite di hello toochange utilizzate da Ripristino automatico di sistema, è possibile modificare le impostazioni di hello in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="1535d-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="1535d-155">**Personalizzare:** selezionarlo toochange hello predefinite utilizzate da Ripristino automatico di sistema.</span><span class="sxs-lookup"><span data-stu-id="1535d-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="1535d-156">**Il gruppo di risorse di destinazione:** è possibile selezionare il gruppo di risorse hello elenco hello di tutti i gruppi di risorse hello esistente nella posizione di destinazione hello sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="1535d-157">**Rete virtuale di destinazione:** è possibile trovare l'elenco di hello della rete virtuale di hello tutte nel percorso di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="1535d-158">**Set di disponibilità:** è possibile aggiungere solo disponibilità set di impostazioni toohello macchine virtuali che fanno parte di disponibilità nell'area di origine.</span><span class="sxs-lookup"><span data-stu-id="1535d-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="1535d-159">**Target Storage accounts (Account di archiviazione di destinazione):**</span><span class="sxs-lookup"><span data-stu-id="1535d-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="1535d-160">![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Fare clic su **Create target resources** (Crea risorse di destinazione) e quindi su Abilita replica.</span><span class="sxs-lookup"><span data-stu-id="1535d-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="1535d-161">Una volta macchine virtuali sono protetti, è possibile controllare lo stato di hello di integrità di macchine virtuali in **gli elementi replicati**</span><span class="sxs-lookup"><span data-stu-id="1535d-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="1535d-162">Durante hello momento della replica iniziale esiste Impossibile la possibilità che lo stato accetta ora toorefresh e non viene visualizzato lo stato di avanzamento per un certo tempo.</span><span class="sxs-lookup"><span data-stu-id="1535d-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="1535d-163">È possibile scegliere il pulsante Aggiorna hello in primo piano hello di stato più recente di hello pannello tooget hello.</span><span class="sxs-lookup"><span data-stu-id="1535d-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="1535d-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1535d-165">Next steps</span></span>
- <span data-ttu-id="1535d-166">[Altre informazioni](site-recovery-test-failover-to-azure.md) sull'esecuzione di un failover di test.</span><span class="sxs-lookup"><span data-stu-id="1535d-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="1535d-167">[Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e come toorun li.</span><span class="sxs-lookup"><span data-stu-id="1535d-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="1535d-168">Altre informazioni, vedere [utilizzando i piani di ripristino](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="1535d-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="1535d-169">Altre informazioni sulla [riprotezione delle VM di Azure](site-recovery-how-to-reprotect.md) dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="1535d-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
