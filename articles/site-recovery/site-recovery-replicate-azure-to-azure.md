---
title: Eseguire la replica di applicazioni (da Azure ad Azure) | Microsoft Docs
description: Questo articolo descrive come configurare la replica di macchine virtuali in esecuzione in un'area di Azure verso un'altra area di Azure.
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
ms.openlocfilehash: f9f97cf840b722c8cfee169dd1640e0682f287ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-virtual-machines-to-another-azure-region"></a><span data-ttu-id="28877-103">Eseguire la replica di macchine virtuali di Azure in un'altra area di Azure</span><span class="sxs-lookup"><span data-stu-id="28877-103">Replicate Azure virtual machines to another Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="28877-104">La replica di Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="28877-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="28877-105">Questo articolo descrive come configurare la replica di macchine virtuali in esecuzione in un'area di Azure verso un'altra area di Azure.</span><span class="sxs-lookup"><span data-stu-id="28877-105">This article describes how to set up replication of virtual machines running in one Azure region to another Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28877-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="28877-106">Prerequisites</span></span>

* <span data-ttu-id="28877-107">L'articolo presuppone una conoscenza di Site Recovery e dell'insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="28877-107">The article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="28877-108">È necessario che sia già stato creato un "insieme di credenziali dei servizi di ripristino".</span><span class="sxs-lookup"><span data-stu-id="28877-108">You need to have a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="28877-109">È consigliabile creare un "insieme di credenziali dei servizi di ripristino" nella posizione in cui si vuole che vengano replicate le VM.</span><span class="sxs-lookup"><span data-stu-id="28877-109">It is recommended that you create the 'Recovery services vault' in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="28877-110">Ad esempio, se la posizione di destinazione è "Stati Uniti centrali", creare l'insieme di credenziali in "Stati Uniti centrali".</span><span class="sxs-lookup"><span data-stu-id="28877-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="28877-111">Se si usano le regole dei gruppi di sicurezza di rete o un proxy firewall per controllare l'accesso alla connettività Internet in uscita nelle VM di Azure, assicurarsi di aggiungere all'elenco elementi consentiti gli URL o gli IP necessari.</span><span class="sxs-lookup"><span data-stu-id="28877-111">If you are using Network Security Groups (NSG) rules or firewall proxy to control access to outbound internet connectivity on the Azure VMs, ensure that you whitelist the required URLs or IPs.</span></span> <span data-ttu-id="28877-112">Per altri dettagli, vedere il [documento di indicazioni sulla rete](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="28877-112">Refer to [Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="28877-113">Se è presente una connessione ExpressRoute o VPN tra posizioni locali e di origine in Azure, vedere il documento [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) (Considerazioni su Site Recovery per la configurazione da Azure a ExpressRoute/VPN in locale).</span><span class="sxs-lookup"><span data-stu-id="28877-113">If you have an ExpressRoute or a VPN connection between on-premises and the source location in Azure, follow [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="28877-114">L'account utente di Azure deve avere determinate [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) per abilitare la replica di una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="28877-114">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="28877-115">È necessario che la sottoscrizione di Azure sia abilitata per la creazione di VM nella posizione di destinazione da usare come area per il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="28877-115">Your Azure subscription should be enabled to create VMs in the target location you want to use as DR region.</span></span> <span data-ttu-id="28877-116">È possibile contattare il supporto tecnico per abilitare la quota necessaria.</span><span class="sxs-lookup"><span data-stu-id="28877-116">You can contact support to enable the required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="28877-117">Abilitare la replica dall'insieme di credenziali di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="28877-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="28877-118">Per illustrare questo concetto, verrà eseguita la replica di VM in esecuzione nell'area "Asia orientale" di Azure verso l'area "Asia sud-orientale".</span><span class="sxs-lookup"><span data-stu-id="28877-118">For this illustration, we will replicate VMs running  in the ‘East Asia’ Azure location to the ‘South East Asia’ location.</span></span> <span data-ttu-id="28877-119">Attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="28877-119">The steps are as follows:</span></span>

 <span data-ttu-id="28877-120">Fare clic su **+Replica** nell'insieme di credenziali per abilitare la replica per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="28877-120">Click **+Replicate** in the vault to enable replication for the virtual machines.</span></span>

1. <span data-ttu-id="28877-121">**Origine:** indica il punto di origine delle macchine virtuali, in questo caso **Azure**.</span><span class="sxs-lookup"><span data-stu-id="28877-121">**Source:** It refers to the point of origin of the machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="28877-122">**Percorso di origine:** indica l'area di Azure da cui si vogliono proteggere le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="28877-122">**Source location:** It is the Azure region from where you want to protect your virtual machines.</span></span> <span data-ttu-id="28877-123">Per questo esempio, il percorso di origine sarà "Asia orientale".</span><span class="sxs-lookup"><span data-stu-id="28877-123">For this illustration, the source location will be 'East Asia'</span></span>

3. <span data-ttu-id="28877-124">**Modello di distribuzione:** indica il modello di distribuzione di Azure per le macchine virtuali di origine.</span><span class="sxs-lookup"><span data-stu-id="28877-124">**Deployment model:** It refers to the Azure deployment model of the source machines.</span></span> <span data-ttu-id="28877-125">È possibile selezionare il modello di distribuzione classica o Resource Manager e le macchine virtuali appartenenti al modello specifico verranno elencate per la protezione nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="28877-125">You can select either classic or resource manager and machines belonging to the specific model will be listed for protection in the next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="28877-126">È solo possibile eseguire la replica di una macchina virtuale classica e ripristinarla come macchina virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="28877-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="28877-127">Non è possibile ripristinarla come macchina virtuale Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="28877-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="28877-128">**Gruppo di risorse:** indica il gruppo di risorse a cui appartengono le macchine virtuali di origine.</span><span class="sxs-lookup"><span data-stu-id="28877-128">**Resource Group:** It’s the resource group to which your source virtual machines belong.</span></span> <span data-ttu-id="28877-129">Tutte le VM nel gruppo di risorse selezionato verranno elencate per la protezione nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="28877-129">All the VMs under the selected resource group will be listed for protection in the next step.</span></span>

    ![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="28877-131">In **Macchine virtuali > Seleziona macchine virtuali** fare clic per selezionare tutte le macchine virtuali da replicare.</span><span class="sxs-lookup"><span data-stu-id="28877-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="28877-132">È possibile selezionare solo i computer per cui è possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="28877-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="28877-133">Fare quindi clic su OK.</span><span class="sxs-lookup"><span data-stu-id="28877-133">Then click OK.</span></span>
    <span data-ttu-id="28877-134">![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="28877-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="28877-135">Nella sezione Impostazioni è possibile configurare le proprietà del sito di destinazione.</span><span class="sxs-lookup"><span data-stu-id="28877-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="28877-136">**Percorso di destinazione:** indica la posizione in cui verrà eseguita la replica dei dati delle macchine virtuali di origine.</span><span class="sxs-lookup"><span data-stu-id="28877-136">**Target Location:**  This is the location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="28877-137">In base al percorso selezionato per le macchine virtuali, Site Recovery fornirà l'elenco di aree di destinazione idonee.</span><span class="sxs-lookup"><span data-stu-id="28877-137">Depending upon your selected machines location, Site Recovery will provide you the list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="28877-138">È consigliabile usare lo stesso percorso di destinazione dell'insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="28877-138">It is recommended to keep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="28877-139">**Gruppo di risorse di destinazione:** indica il gruppo di risorse a cui apparterranno tutte le macchine virtuali replicate. Per impostazione predefinita, Azure Site Recovery creerà un nuovo gruppo di risorse nell'area di destinazione, con un nome con suffisso "asr".</span><span class="sxs-lookup"><span data-stu-id="28877-139">**Target resource group :** It is the resource group to which all your replicated virtual machines will belong.By default ASR will create a new resource group in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="28877-140">Nel caso in cui il gruppo di risorse creato da Azure Site Recovery esista già, verrà riutilizzato. È anche possibile scegliere di personalizzarlo, come illustrato nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="28877-140">In case resource group created by ASR already exist, it will be reused.You can also choose to customize it as shown in the section below.</span></span>    
3. <span data-ttu-id="28877-141">**Target Virtual Network (Rete virtuale di destinazione):** per impostazione predefinita, Azure Site Recovery creerà una nuova rete virtuale nell'area di destinazione con un nome con suffisso "asr".</span><span class="sxs-lookup"><span data-stu-id="28877-141">**Target Virtual Network:** By default, ASR will create a new virtual network in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="28877-142">Questa rete verrà mappata alla rete di origine e verrà usata per la protezione futura.</span><span class="sxs-lookup"><span data-stu-id="28877-142">This will be mapped to your source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="28877-143">[Controllare i dettagli sulla rete](site-recovery-network-mapping-azure-to-azure.md) per ottenere altre informazioni sul mapping di rete.</span><span class="sxs-lookup"><span data-stu-id="28877-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) to know more about network mapping.</span></span>

4. <span data-ttu-id="28877-144">**Target Storage accounts (Account di archiviazione di destinazione):** per impostazione predefinita, Azure Site Recovery creerà un nuovo account di archiviazione di destinazione, che rispecchia la configurazione delle risorse di archiviazione della VM di origine.</span><span class="sxs-lookup"><span data-stu-id="28877-144">**Target Storage accounts:** By default, ASR will create the new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="28877-145">Nel caso in cui l'account di archiviazione creato da Azure Site Recovery esista già, verrà riutilizzato.</span><span class="sxs-lookup"><span data-stu-id="28877-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="28877-146">**Cache Storage accounts (Account di archiviazione della cache):** Azure Site Recovery necessita di un account di archiviazione aggiuntivo, definito account di archiviazione della cache, nell'area di origine.</span><span class="sxs-lookup"><span data-stu-id="28877-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in the source region.</span></span> <span data-ttu-id="28877-147">Tutte le modifiche apportate nelle VM di origine vengono registrate e inviate all'account di archiviazione della cache prima della replica nella posizione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="28877-147">All the changes happening on the source VMs are tracked and sent to cache storage account before replicating those to the target location.</span></span>

6. <span data-ttu-id="28877-148">**Set di disponibilità:** per impostazione predefinita, Azure Site Recovery creerà un nuovo set di disponibilità nell'area di destinazione, con un nome con suffisso "asr".</span><span class="sxs-lookup"><span data-stu-id="28877-148">**Availability set :** By default, ASR will create a new availability set in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="28877-149">Nel caso in cui il set di disponibilità creato da Azure Site Recovery esista già, verrà riutilizzato.</span><span class="sxs-lookup"><span data-stu-id="28877-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="28877-150">**Criteri di replica:** definisce le impostazioni per la cronologia della conservazione del punto di ripristino e per la frequenza snapshot coerenti con l'app.</span><span class="sxs-lookup"><span data-stu-id="28877-150">**Replication Policy:** It defines the settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="28877-151">Per impostazione predefinita, Azure Site Recovery creerà un nuovo criterio di replica con impostazioni predefiniti di "24 ore" per la conservazione del punto di ripristino e di "60 minuti" per la frequenza snapshot coerenti con l'app.</span><span class="sxs-lookup"><span data-stu-id="28877-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="28877-153">Personalizzare le risorse di destinazione</span><span class="sxs-lookup"><span data-stu-id="28877-153">Customize target resources</span></span>

<span data-ttu-id="28877-154">Se si vogliono modificare i valori predefiniti usati da Azure Site Recovery, è possibile modificare le impostazioni in base alle esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="28877-154">In case you want to change the defaults used by ASR, you can change the settings based on your needs.</span></span>

1. <span data-ttu-id="28877-155">**Personalizza:** fare clic sul pulsante per modificare le impostazioni predefinite usate da Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="28877-155">**Customize:** Click it to change the defaults used by ASR.</span></span>

2. <span data-ttu-id="28877-156">**Gruppo di risorse di destinazione:** è possibile selezionare il gruppo di risorse dall'elenco di tutti i gruppi di risorse esistenti nel percorso di destinazione all'interno della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="28877-156">**Target resource group :**  You can select the resource group from the list of all the resource groups existing in the target location within the subscription.</span></span>

3. <span data-ttu-id="28877-157">**Target Virtual Network (Rete virtuale di destinazione):** è possibile trovare l'elenco di tutte le reti virtuali nel percorso di destinazione.</span><span class="sxs-lookup"><span data-stu-id="28877-157">**Target Virtual Network:** You can find the list of all the virtual network in the target location.</span></span>

4. <span data-ttu-id="28877-158">**Set di disponibilità:** è possibile aggiungere impostazioni dei set di disponibilità solo alle macchine virtuali che appartengono a un set di disponibilità nell'area di origine.</span><span class="sxs-lookup"><span data-stu-id="28877-158">**Availability set :** You can only add availability sets settings to the virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="28877-159">**Target Storage accounts (Account di archiviazione di destinazione):**</span><span class="sxs-lookup"><span data-stu-id="28877-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="28877-160">![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Fare clic su **Create target resources** (Crea risorse di destinazione) e quindi su Abilita replica.</span><span class="sxs-lookup"><span data-stu-id="28877-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="28877-161">Dopo avere completato la protezione delle macchine virtuali, è possibile controllare lo stato dell'integrità delle VM in **Elementi replicati**.</span><span class="sxs-lookup"><span data-stu-id="28877-161">Once virtual machines are protected you can check the status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="28877-162">Durante la replica iniziale è possibile che sia necessario attendere qualche minuto per l'aggiornamento dello stato e per la visualizzazione dell'avanzamento.</span><span class="sxs-lookup"><span data-stu-id="28877-162">During the time of initial replication there could a possibility that status takes time to refresh and you don't see progress for some time.</span></span> <span data-ttu-id="28877-163">È possibile fare clic sul pulsante Aggiorna nella parte superiore del pannello per visualizzare lo stato più aggiornato.</span><span class="sxs-lookup"><span data-stu-id="28877-163">You can click the Refresh button on the top of the blade to get the latest status.</span></span>
>

![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="28877-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28877-165">Next steps</span></span>
- <span data-ttu-id="28877-166">[Altre informazioni](site-recovery-test-failover-to-azure.md) sull'esecuzione di un failover di test.</span><span class="sxs-lookup"><span data-stu-id="28877-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="28877-167">[Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e su come eseguirli.</span><span class="sxs-lookup"><span data-stu-id="28877-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="28877-168">Altre informazioni sull'[uso dei piani di ripristino](site-recovery-create-recovery-plans.md) per la riduzione di RTO.</span><span class="sxs-lookup"><span data-stu-id="28877-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
- <span data-ttu-id="28877-169">Altre informazioni sulla [riprotezione delle VM di Azure](site-recovery-how-to-reprotect.md) dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="28877-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
