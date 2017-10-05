---
title: Pianificare la rete per la replica VMware in Azure | Microsoft Docs
description: Questo articolo illustra la pianificazione di rete necessaria per la replica di VM VMware in Azure
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
ms.openlocfilehash: f164ac68ba6ec650bb3996b4aa870e1b98533a23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-4-plan-networking-for-vmware-to-azure-replication"></a><span data-ttu-id="a6132-103">Passaggio 4: Pianificare la rete per la replica VMware in Azure</span><span class="sxs-lookup"><span data-stu-id="a6132-103">Step 4: Plan networking for VMware to Azure replication</span></span>

<span data-ttu-id="a6132-104">Questo articolo riepiloga le considerazioni relative alla pianificazione di rete quando si esegue la replica di VM VMware locali in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6132-104">This article summarizes network planning considerations when replicating on-premises VMware VMs to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="a6132-105">È possibile inserire commenti alla fine di questo articolo oppure porre domande nel [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a6132-105">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connect-to-replica-vms"></a><span data-ttu-id="a6132-106">Connettersi alle VM di replica</span><span class="sxs-lookup"><span data-stu-id="a6132-106">Connect to replica VMs</span></span>

<span data-ttu-id="a6132-107">Quando si pianifica la strategia di replica e failover, una delle domande principali riguarda la modalità di connessione alla VM di Azure dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a6132-107">When planning your replication and failover strategy, one of the key questions is how to connect to the Azure VM after failover.</span></span> <span data-ttu-id="a6132-108">Quando si progetta la strategia di rete per la replica di VM di Azure, ci sono due opzioni:</span><span class="sxs-lookup"><span data-stu-id="a6132-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="a6132-109">**Usare un indirizzo IP diverso**: è possibile scegliere di usare un intervallo di indirizzi IP diverso per la rete di VM di Azure di cui viene eseguita la replica.</span><span class="sxs-lookup"><span data-stu-id="a6132-109">**Use different IP address**: You can select to use a different IP address range for the replicated Azure VM network.</span></span> <span data-ttu-id="a6132-110">In questo scenario, la VM ottiene un nuovo indirizzo IP dopo il failover ed è necessario un aggiornamento del DNS.</span><span class="sxs-lookup"><span data-stu-id="a6132-110">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="a6132-111">**Mantenere lo stesso indirizzo IP**: si potrebbe voler usare lo stesso intervallo di indirizzi del sito primario locale per la rete di Azure dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a6132-111">**Retain same IP address**: You might want to use the same IP address range as that in your primary on-premises site, for the Azure network after failover.</span></span> <span data-ttu-id="a6132-112">Mantenere gli stessi indirizzi IP semplifica il ripristino riducendo i problemi di rete dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a6132-112">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="a6132-113">Quando si esegue la replica in Azure, è tuttavia necessario aggiornare le route con la nuova posizione degli indirizzi IP dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a6132-113">However, when you're replicating to Azure, you will need to update routes with the new location of the IP addresses after failover.</span></span> 


## <a name="retain-ip-addresses"></a><span data-ttu-id="a6132-114">Mantenere gli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="a6132-114">Retain IP addresses</span></span>

<span data-ttu-id="a6132-115">Site Recovery consente di mantenere gli indirizzi IP fissi durante il failover in Azure, con un failover sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="a6132-115">Site Recovery provides the capability to retain fixed IP addresses when failing over to Azure, with a subnet failover.</span></span>

<span data-ttu-id="a6132-116">Con il failover sulla subnet è presente una subnet specifica nel sito 1 o nel sito 2, ma mai in entrambi i siti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="a6132-116">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="a6132-117">Per mantenere lo spazio degli indirizzi IP in caso di failover, si programma l'infrastruttura del router per lo spostamento delle subnet da un sito a un altro.</span><span class="sxs-lookup"><span data-stu-id="a6132-117">In order to maintain the IP address space in the event of a failover, you programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="a6132-118">Durante il failover, le subnet vengono spostate con le VM protette associate.</span><span class="sxs-lookup"><span data-stu-id="a6132-118">During failover, the subnets move with the associated protected VMs.</span></span> <span data-ttu-id="a6132-119">Il principale svantaggio è che in caso di errore è necessario spostare l'intera subnet.</span><span class="sxs-lookup"><span data-stu-id="a6132-119">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="a6132-120">Esempio di failover</span><span class="sxs-lookup"><span data-stu-id="a6132-120">Failover example</span></span>

<span data-ttu-id="a6132-121">Esaminiamo ora un esempio di failover in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-121">Let's look at an example for failover to Azure.</span></span>

- <span data-ttu-id="a6132-122">Una società fittizia, Woodgrove Bank, dispone di un'infrastruttura locale che ospita le app aziendali.</span><span class="sxs-lookup"><span data-stu-id="a6132-122">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="a6132-123">Le applicazioni per dispositivi mobili sono ospitate in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-123">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="a6132-124">La connettività tra le VM di Woodgrove Bank in Azure e i server locali è fornita da una connessione (VPN) da sito a sito tra la rete perimetrale locale e la rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-124">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between the on-premises edge network and the Azure virtual network.</span></span>
- <span data-ttu-id="a6132-125">La presenza della VPN implica che la rete virtuale dell'azienda in Azure sia visualizzata come estensione della rete locale.</span><span class="sxs-lookup"><span data-stu-id="a6132-125">This VPN means that the company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="a6132-126">Woodgrove vuole usare Site Recovery per replicare i carichi di lavoro locali in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-126">Woodgrove wants to use Site Recovery to replicate on-premises workloads to Azure.</span></span>
 - <span data-ttu-id="a6132-127">Woodgrove deve tenere conto delle applicazioni e delle configurazioni che dipendono da indirizzi IP hardcoded, quindi deve mantenere gli indirizzi IP delle applicazioni dopo il failover in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-127">Woodgrove has to deal with applications and configurations which depend on hard-coded IP addresses, and thus need to retain IP addresses for their applications after failover to Azure.</span></span>
 - <span data-ttu-id="a6132-128">Woodgrove ha assegnato gli indirizzi IP dall'intervallo 172.16.1.0/24, 172.16.2.0/24 alle risorse in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-128">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 to its resources running in Azure.</span></span>


<span data-ttu-id="a6132-129">Ecco cosa deve fare Woodgrove per poter replicare le VM in Azure mantenendo gli indirizzi IP:</span><span class="sxs-lookup"><span data-stu-id="a6132-129">For Woodgrove to be able to replicate its VMS to Azure while retaining the IP addresses, here's what the company needs to do:</span></span>

1. <span data-ttu-id="a6132-130">Creare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="a6132-130">Create an Azure virtual network.</span></span> <span data-ttu-id="a6132-131">Deve trattarsi di un'estensione della rete locale, per agevolare il failover delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a6132-131">It should be an extension of the on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="a6132-132">Azure consente di aggiungere connettività VPN da sito a sito, oltre che connettività da punto a sito, alle reti virtuali create in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-132">Azure allows you to add site-to-site VPN connectivity, in addition to point-to-site connectivity to the virtual networks created in Azure.</span></span>
3. <span data-ttu-id="a6132-133">Quando si configura la connessione da sito a sito, nella rete di Azure è possibile instradare il traffico verso il percorso locale (rete locale) solo se l'intervallo di indirizzi IP è diverso da quello degli indirizzi IP locali.</span><span class="sxs-lookup"><span data-stu-id="a6132-133">When setting up the site-to-site connection, in the Azure network, you can route traffic to the on-premises location (local-network) only if the IP address range is different from the on-premises IP address range.</span></span>
    - <span data-ttu-id="a6132-134">Ciò è dovuto al fatto che Azure non supporta le subnet estese.</span><span class="sxs-lookup"><span data-stu-id="a6132-134">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="a6132-135">Se si ha quindi una subnet 192.168.1.0/24 locale, non è possibile aggiungere una rete locale 192.168.1.0/24 nella rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-135">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in the Azure network.</span></span>
    - <span data-ttu-id="a6132-136">Si tratta di un comportamento previsto, perché Azure non sa che non ci sono VM attive nella subnet e che la subnet viene creata solo per scopi di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="a6132-136">This is expected because Azure doesn’t know that there are no active VMs in the subnet, and that the subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="a6132-137">Per poter instradare correttamente il traffico di rete all'esterno di una rete di Azure, le subnet nella rete e nella rete locale non devono essere in conflitto.</span><span class="sxs-lookup"><span data-stu-id="a6132-137">To be able to correctly route network traffic out of an Azure network the subnets in the network and the local-network mustn't conflict.</span></span>

![Prima del failover sulla subnet](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="a6132-139">Prima del failover</span><span class="sxs-lookup"><span data-stu-id="a6132-139">Before failover</span></span>

1. <span data-ttu-id="a6132-140">Creare una rete aggiuntiva (ad esempio una rete di ripristino).</span><span class="sxs-lookup"><span data-stu-id="a6132-140">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="a6132-141">Si tratta della rete in cui vengono create le VM di cui viene eseguito il failover.</span><span class="sxs-lookup"><span data-stu-id="a6132-141">This is the network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="a6132-142">Per assicurarsi che l'indirizzo IP per una VM venga mantenuto dopo un failover, nelle proprietà della VM selezionare **Configura**, specificare lo stesso indirizzo IP locale della VM e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a6132-142">To ensure that the IP address for a VM is retained after a failover, in the VM properties > **Configure**, specify the same IP address that the VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="a6132-143">Quando viene eseguito il failover della VM, Azure Site Recovery assegna l'indirizzo IP specificato alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6132-143">When the VM is failed over, Azure Site Recovery will assign the provided IP address to it.</span></span>

    ![Proprietà di rete](./media/site-recovery-network-design/network-design8.png)

4. <span data-ttu-id="a6132-145">Dopo l'attivazione del failover e la creazione delle VM in Azure con l'indirizzo IP richiesto, è possibile connettersi alla rete tramite una [connessione da rete virtuale a rete virtuale](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="a6132-145">After failover is trigger is triggered, and the VMs are created in Azure with the required IP address, you can connect to the network using a [Vnet to Vnet connection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="a6132-146">Questa azione può essere eseguita tramite script.</span><span class="sxs-lookup"><span data-stu-id="a6132-146">This action can be scripted.</span></span>
5. <span data-ttu-id="a6132-147">Le route devono essere modificate adeguatamente in modo da indicare lo spostamento di 192.168.1.0/24 ad Azure.</span><span class="sxs-lookup"><span data-stu-id="a6132-147">Routes need to be appropriately modified, to reflect that 192.168.1.0/24 has now moved to Azure.</span></span>

    ![Dopo il failover sulla subnet](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="a6132-149">Dopo il failover</span><span class="sxs-lookup"><span data-stu-id="a6132-149">After failover</span></span>

<span data-ttu-id="a6132-150">Se non si dispone di una rete di Azure come illustrato in precedenza, è possibile creare una connessione VPN da sito a sito tra il sito primario e Azure, dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a6132-150">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failover.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="a6132-151">Modificare gli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="a6132-151">Change IP addresses</span></span>

<span data-ttu-id="a6132-152">Questo [post di blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) spiega come configurare l'infrastruttura di rete di Azure quando non è necessario mantenere gli indirizzi IP dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a6132-152">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how to set up the Azure networking infrastructure when you don't need to retain IP addresses after failover.</span></span> <span data-ttu-id="a6132-153">Inizia con una descrizione dell'applicazione, analizza come impostare la rete locale e in Azure e conclude con informazioni sull'esecuzione dei failover.</span><span class="sxs-lookup"><span data-stu-id="a6132-153">It starts with an application description, looks at how to set up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a6132-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6132-154">Next steps</span></span>

<span data-ttu-id="a6132-155">Andare al [Passaggio 5: Preparare Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="a6132-155">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>
