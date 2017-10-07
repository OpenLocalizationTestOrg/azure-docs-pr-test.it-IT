---
title: servizi di rete per la replica VMware tooAzure aaaPlan | Documenti Microsoft
description: In questo articolo vengono illustrati pianificazione necessaria per la replica delle macchine virtuali VMware tooAzure di rete
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5578a0b4-0352-41c3-9cce-56beb17a4d97
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 2b4f385c768cc7f5e98abae0afb8258b00f3724f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-vmware-tooazure-replication"></a><span data-ttu-id="16a50-103">Passaggio 4: Pianificare la rete per la replica tooAzure VMware</span><span class="sxs-lookup"><span data-stu-id="16a50-103">Step 4: Plan networking for VMware tooAzure replication</span></span>

<span data-ttu-id="16a50-104">Questo articolo riepiloga le considerazioni sulla pianificazione quando la replica locale tooAzure le macchine virtuali VMware tramite hello rete [Azure Site Recovery](site-recovery-overview.md) servizio.</span><span class="sxs-lookup"><span data-stu-id="16a50-104">This article summarizes network planning considerations when replicating on-premises VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="16a50-105">Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="16a50-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connect-tooreplica-vms"></a><span data-ttu-id="16a50-106">Connettere le macchine virtuali tooreplica</span><span class="sxs-lookup"><span data-stu-id="16a50-106">Connect tooreplica VMs</span></span>

<span data-ttu-id="16a50-107">Quando si pianifica la replica e la strategia di failover, una delle domande chiave hello è come tooconnect toohello macchina virtuale di Azure dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="16a50-108">Quando si progetta la strategia di rete per la replica di VM di Azure, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="16a50-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="16a50-109">**Utilizzare l'indirizzo IP diverso**: È possibile selezionare toouse un intervallo di indirizzi IP diversi per hello replicati rete VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="16a50-109">**Use different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="16a50-110">In questo hello scenario VM Ottiene un nuovo indirizzo IP dopo il failover ed è richiesto un aggiornamento DNS.</span><span class="sxs-lookup"><span data-stu-id="16a50-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="16a50-111">**Mantenere stesso indirizzo IP**: potrebbe essere necessario toouse hello stesso intervallo di indirizzi IP a quella del sito primario locale, per hello Azure rete dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-111">**Retain same IP address**: You might want toouse hello same IP address range as that in your primary on-premises site, for hello Azure network after failover.</span></span> <span data-ttu-id="16a50-112">Conservazione hello stessi indirizzi IP semplifica il ripristino di hello riducendo i problemi di rete dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-112">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="16a50-113">Tuttavia, quando si esegue la replica tooAzure, sarà necessario route tooupdate con nuovo percorso di hello di indirizzi IP hello dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-113">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span> 


## <a name="retain-ip-addresses"></a><span data-ttu-id="16a50-114">Mantenere gli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="16a50-114">Retain IP addresses</span></span>

<span data-ttu-id="16a50-115">Site Recovery fornisce gli indirizzi IP di hello funzionalità tooretain predefinito quando si esegue il failover tooAzure, con un failover su subnet.</span><span class="sxs-lookup"><span data-stu-id="16a50-115">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="16a50-116">Con il failover sulla subnet è presente una subnet specifica nel sito 1 o nel sito 2, ma mai in entrambi i siti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="16a50-116">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="16a50-117">In ordine toomaintain hello spazio degli indirizzi IP nell'evento hello di un failover, provvederà a livello di codice per le subnet hello router infrastruttura toomove hello da un sito tooanother.</span><span class="sxs-lookup"><span data-stu-id="16a50-117">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="16a50-118">Durante il failover, spostamento di subnet hello con hello associate macchine virtuali protette.</span><span class="sxs-lookup"><span data-stu-id="16a50-118">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="16a50-119">svantaggio Hello è che in caso di hello di un errore, si dispone di toomove hello intera subnet.</span><span class="sxs-lookup"><span data-stu-id="16a50-119">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="16a50-120">Esempio di failover</span><span class="sxs-lookup"><span data-stu-id="16a50-120">Failover example</span></span>

<span data-ttu-id="16a50-121">Esaminiamo un esempio di tooAzure di failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-121">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="16a50-122">Una società fittizia, Woodgrove Bank, dispone di un'infrastruttura locale che ospita le app aziendali.</span><span class="sxs-lookup"><span data-stu-id="16a50-122">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="16a50-123">Le applicazioni per dispositivi mobili sono ospitate in Azure.</span><span class="sxs-lookup"><span data-stu-id="16a50-123">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="16a50-124">La connettività tra macchine virtuali di Woodgrove Bank server locali e Azure viene fornita da una connessione (VPN) da sito a sito tra una rete perimetrale locale di hello e hello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="16a50-124">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="16a50-125">Ciò significa VPN che hello virtuale rete aziendale in Azure viene visualizzato come un'estensione della rete locale.</span><span class="sxs-lookup"><span data-stu-id="16a50-125">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="16a50-126">Woodgrove vuole toouse Site Recovery tooreplicate locale i carichi di lavoro tooAzure.</span><span class="sxs-lookup"><span data-stu-id="16a50-126">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="16a50-127">Woodgrove ha toodeal con applicazioni e le configurazioni che dipendono dal livello di codice gli indirizzi IP e pertanto richiede indirizzi IP tooretain per le applicazioni dopo il failover tooAzure.</span><span class="sxs-lookup"><span data-stu-id="16a50-127">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="16a50-128">Woodgrove dispone di indirizzi IP assegnati dall'intervallo 172.16.1.0/24, 172.16.2.0/24 tooits risorse in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="16a50-128">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="16a50-129">Per Woodgrove toobe in grado di tooreplicate tooAzure relative macchine Virtuali mentre mantenendo hello IP indirizzi, ecco le società hello deve toodo:</span><span class="sxs-lookup"><span data-stu-id="16a50-129">For Woodgrove toobe able tooreplicate its VMS tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="16a50-130">Creare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="16a50-130">Create an Azure virtual network.</span></span> <span data-ttu-id="16a50-131">Deve essere un'estensione di hello locale rete, in modo che le applicazioni possono eseguire facilmente il failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-131">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="16a50-132">Azure consente di tooadd site-to-site VPN connettività inoltre connettività da sito a toopoint toohello le reti virtuali create in Azure.</span><span class="sxs-lookup"><span data-stu-id="16a50-132">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="16a50-133">Quando si configura una connessione site-to-site hello, in Azure hello di rete, è possibile indirizzare percorso locale di traffico toohello (rete locale) solo se l'intervallo di indirizzi IP hello è diverso dall'intervallo di indirizzi IP locale hello.</span><span class="sxs-lookup"><span data-stu-id="16a50-133">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="16a50-134">Ciò è dovuto al fatto che Azure non supporta le subnet estese.</span><span class="sxs-lookup"><span data-stu-id="16a50-134">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="16a50-135">Pertanto, se si dispone di subnet 192.168.1.0/24 locale, è possibile aggiungere 192.168.1.0/24 una rete locale in hello rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="16a50-135">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="16a50-136">È previsto poiché Azure non riconosce che non esistono attivi sono macchine virtuali nella subnet hello e subnet hello viene creato per solo il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="16a50-136">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="16a50-137">toobe toocorrectly in grado di routing del traffico da una subnet hello rete di Azure in rete hello e hello rete locale non deve entrare in conflitto.</span><span class="sxs-lookup"><span data-stu-id="16a50-137">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![Prima del failover sulla subnet](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="16a50-139">Prima del failover</span><span class="sxs-lookup"><span data-stu-id="16a50-139">Before failover</span></span>

1. <span data-ttu-id="16a50-140">Creare una rete aggiuntiva (ad esempio una rete di ripristino).</span><span class="sxs-lookup"><span data-stu-id="16a50-140">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="16a50-141">Rete hello in cui eseguire il failover le macchine virtuali vengono creati.</span><span class="sxs-lookup"><span data-stu-id="16a50-141">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="16a50-142">tooensure che hello indirizzo IP per una macchina virtuale viene mantenuta dopo un failover, nella proprietà della macchina virtuale hello > **configura**, specificare tale hello e macchina virtuale locale, scegliere l'indirizzo IP stesso hello **salvare**.</span><span class="sxs-lookup"><span data-stu-id="16a50-142">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="16a50-143">Quando hello VM è stato eseguito il failover, Azure Site Recovery assegnerà hello fornito tooit indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="16a50-143">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![Proprietà di rete](./media/site-recovery-network-design/network-design8.png)

4. <span data-ttu-id="16a50-145">Al termine del failover trigger viene attivato e le macchine virtuali hello vengono create in Azure con l'indirizzo IP hello necessario, è possibile connettersi tramite rete toohello un [connessione di rete virtuale tooVnet](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="16a50-145">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet connection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="16a50-146">Questa azione può essere eseguita tramite script.</span><span class="sxs-lookup"><span data-stu-id="16a50-146">This action can be scripted.</span></span>
5. <span data-ttu-id="16a50-147">Le route necessarie toobe modificate in modo appropriato, tooreflect che 192.168.1.0/24 ha spostato tooAzure.</span><span class="sxs-lookup"><span data-stu-id="16a50-147">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![Dopo il failover sulla subnet](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="16a50-149">Dopo il failover</span><span class="sxs-lookup"><span data-stu-id="16a50-149">After failover</span></span>

<span data-ttu-id="16a50-150">Se non si dispone di una rete di Azure come illustrato in precedenza, è possibile creare una connessione VPN da sito a sito tra il sito primario e Azure, dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-150">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failover.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="16a50-151">Modificare gli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="16a50-151">Change IP addresses</span></span>

<span data-ttu-id="16a50-152">Questo [post di blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) spiega come tooset backup hello Azure infrastruttura di rete quando non è necessario tooretain IP indirizzi dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-152">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="16a50-153">Inizia con una descrizione dell'applicazione, è in modalità tooset di rete locale e in Azure e si conclude con informazioni sull'esecuzione di failover.</span><span class="sxs-lookup"><span data-stu-id="16a50-153">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="16a50-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16a50-154">Next steps</span></span>

<span data-ttu-id="16a50-155">Andare troppo[passaggio 5: preparare Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="16a50-155">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>
