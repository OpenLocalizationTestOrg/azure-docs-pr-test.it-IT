---
title: "una distribuzione a più livelli di Citrix XenDesktop e informazioni usando Azure Site Recovery aaaReplicate | Documenti Microsoft"
description: Questo articolo viene descritto come tooprotect e ripristinare di distribuzioni di Citrix XenDesktop e informazioni tramite Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="57bda-103">Eseguire la replica di una distribuzione Citrix XenApp e XenDesktop multilivello con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="57bda-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="57bda-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="57bda-104">Overview</span></span>

<span data-ttu-id="57bda-105">Citrix XenDesktop è una soluzione di virtualizzazione desktop che consente di recapitare desktop e applicazioni come un ondemand tooany utente del servizio in qualsiasi punto.</span><span class="sxs-lookup"><span data-stu-id="57bda-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="57bda-106">Con la tecnologia di recapito, FlexCast XenDesktop rapido e sicuro consegnano toousers desktop e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="57bda-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="57bda-107">Citrix XenApp non fornisce attualmente funzionalità di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="57bda-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="57bda-108">Una soluzione di ripristino di emergenza valido, deve consentire di modellazione dei piani di ripristino intorno hello sopra architetture di applicazioni complesse e dispongano di hello possibilità tooadd personalizzato passaggi toohandle applicazione mapping tra i vari livelli fornendo un con clic singolo che cattura soluzione nell'evento hello un'emergenza iniziali tooa inferiore RTO.</span><span class="sxs-lookup"><span data-stu-id="57bda-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="57bda-109">Questo documento fornisce indicazioni dettagliate per la creazione di una soluzione di ripristino di emergenza per le distribuzioni Citrix XenApp locali in piattaforme Hyper-V e VMware vSphere.</span><span class="sxs-lookup"><span data-stu-id="57bda-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="57bda-110">Questo documento descrive inoltre come tooperform un failover di test (analisi di ripristino di emergenza) e con i piani di ripristino, le configurazioni supportata di hello e prerequisiti tooAzure di failover non pianificato.</span><span class="sxs-lookup"><span data-stu-id="57bda-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="57bda-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="57bda-111">Prerequisites</span></span>

<span data-ttu-id="57bda-112">Prima di iniziare, assicurarsi di che aver compreso l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="57bda-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="57bda-113">La replica tooAzure una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="57bda-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="57bda-114">Come troppo[progettare una rete di ripristino](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="57bda-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="57bda-115">Esegue un tooAzure di failover di test</span><span class="sxs-lookup"><span data-stu-id="57bda-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="57bda-116">Eseguire un failover tooAzure</span><span class="sxs-lookup"><span data-stu-id="57bda-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="57bda-117">Come troppo[replicare un controller di dominio](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="57bda-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="57bda-118">Come troppo[la replica di SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="57bda-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="57bda-119">Modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="57bda-119">Deployment patterns</span></span>

<span data-ttu-id="57bda-120">Una farm Citrix XenApp e XenDesktop include in genere hello seguente modello di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="57bda-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="57bda-121">**Modello di distribuzione**</span><span class="sxs-lookup"><span data-stu-id="57bda-121">**Deployment pattern**</span></span>

<span data-ttu-id="57bda-122">Distribuzione Citrix XenApp e XenDesktop con server DNS di AD, server di database SQL, Citrix Delivery Controller, server StoreFront, XenApp Master (VDA), server licenze di Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="57bda-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Modello di distribuzione 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="57bda-124">Supporto di Site Recovery</span><span class="sxs-lookup"><span data-stu-id="57bda-124">Site Recovery support</span></span>

<span data-ttu-id="57bda-125">A scopo di hello di questo articolo, Citrix le distribuzioni di macchine virtuali VMware è gestito da vSphere 6.0 o System Center VMM 2012 R2 sono stati utilizzati toosetup ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="57bda-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="57bda-126">Origine e destinazione</span><span class="sxs-lookup"><span data-stu-id="57bda-126">Source and target</span></span>

<span data-ttu-id="57bda-127">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="57bda-127">**Scenario**</span></span> | <span data-ttu-id="57bda-128">**sito secondario tooa**</span><span class="sxs-lookup"><span data-stu-id="57bda-128">**tooa secondary site**</span></span> | <span data-ttu-id="57bda-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="57bda-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="57bda-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="57bda-130">**Hyper-V**</span></span> | <span data-ttu-id="57bda-131">Non nell'ambito</span><span class="sxs-lookup"><span data-stu-id="57bda-131">Not in scope</span></span> | <span data-ttu-id="57bda-132">Sì</span><span class="sxs-lookup"><span data-stu-id="57bda-132">Yes</span></span>
<span data-ttu-id="57bda-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="57bda-133">**VMware**</span></span> | <span data-ttu-id="57bda-134">Non nell'ambito</span><span class="sxs-lookup"><span data-stu-id="57bda-134">Not in scope</span></span> | <span data-ttu-id="57bda-135">Sì</span><span class="sxs-lookup"><span data-stu-id="57bda-135">Yes</span></span>
<span data-ttu-id="57bda-136">**Server fisico**</span><span class="sxs-lookup"><span data-stu-id="57bda-136">**Physical server**</span></span> | <span data-ttu-id="57bda-137">Non nell'ambito</span><span class="sxs-lookup"><span data-stu-id="57bda-137">Not in scope</span></span> | <span data-ttu-id="57bda-138">Sì</span><span class="sxs-lookup"><span data-stu-id="57bda-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="57bda-139">Versioni</span><span class="sxs-lookup"><span data-stu-id="57bda-139">Versions</span></span>
<span data-ttu-id="57bda-140">I clienti possono distribuire componenti di XenApp come macchine virtuali in esecuzione su Hyper-V o VMware oppure come server fisici.</span><span class="sxs-lookup"><span data-stu-id="57bda-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="57bda-141">Azure Site Recovery può proteggere entrambi tooAzure distribuzioni fisici e virtuali.</span><span class="sxs-lookup"><span data-stu-id="57bda-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="57bda-142">Poiché informazioni 7.7 o versioni successive sono supportato in Azure, solo le distribuzioni con tali versioni non consente il failover tooAzure per il ripristino di emergenza o la migrazione.</span><span class="sxs-lookup"><span data-stu-id="57bda-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="57bda-143">Operazioni tookeep presente</span><span class="sxs-lookup"><span data-stu-id="57bda-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="57bda-144">Protezione e ripristino di on-premise le distribuzioni con sistema operativo Server macchine toodeliver informazioni App pubblicate e informazioni pubblicate desktop è supportata.</span><span class="sxs-lookup"><span data-stu-id="57bda-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="57bda-145">Protezione e il ripristino delle distribuzioni locali utilizzando desktop del sistema operativo macchine toodeliver Desktop VDI per i desktop virtuali client, incluso Windows 10, non è supportata.</span><span class="sxs-lookup"><span data-stu-id="57bda-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="57bda-146">Infatti, ripristino automatico di sistema non supporta il ripristino hello di computer con desktop OS'es.</span><span class="sxs-lookup"><span data-stu-id="57bda-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="57bda-147">Alcuni tipi di desktop virtuale client, ad esempio</span><span class="sxs-lookup"><span data-stu-id="57bda-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="57bda-148">Windows 7, non sono inoltre ancora supportati per le licenze in Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="57bda-149">[Altre informazioni](https://azure.microsoft.com/pricing/licensing-faq/) sulle licenze per computer desktop client/server in Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="57bda-150">Azure Site Recovery non può replicare e proteggere cloni MCS o PVS locali esistenti.</span><span class="sxs-lookup"><span data-stu-id="57bda-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="57bda-151">È necessario toorecreate i cloni utilizzando Azure RM provisioning dal controller di recapito.</span><span class="sxs-lookup"><span data-stu-id="57bda-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="57bda-152">NetScaler non può essere protetto tramite Azure Site Recovery perché NetScaler è basato su FreeBSD e Azure Site Recovery non supporta la protezione del sistema operativo FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="57bda-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="57bda-153">Si sarebbe necessario toodeploy e configurare un nuovo dispositivo NetScaler da Azure Marketplace dopo il failover tooAzure.</span><span class="sxs-lookup"><span data-stu-id="57bda-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="57bda-154">Replica di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="57bda-154">Replicating virtual machines</span></span>

<span data-ttu-id="57bda-155">Hello seguenti componenti di hello Citrix XenApp distribuzione necessario replica tooenable toobe protetto e il ripristino.</span><span class="sxs-lookup"><span data-stu-id="57bda-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="57bda-156">Protezione del server DNS di AD</span><span class="sxs-lookup"><span data-stu-id="57bda-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="57bda-157">Protezione del server di database SQL</span><span class="sxs-lookup"><span data-stu-id="57bda-157">Protection of SQL database server</span></span>
* <span data-ttu-id="57bda-158">Protezione di Citrix Delivery Controller</span><span class="sxs-lookup"><span data-stu-id="57bda-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="57bda-159">Protezione del server StoreFront</span><span class="sxs-lookup"><span data-stu-id="57bda-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="57bda-160">Protezione di XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="57bda-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="57bda-161">Protezione del server licenze di Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="57bda-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="57bda-162">**Replica del server DNS di AD**</span><span class="sxs-lookup"><span data-stu-id="57bda-162">**AD DNS server replication**</span></span>

<span data-ttu-id="57bda-163">Consultare troppo[proteggere Active Directory e DNS con Azure Site Recovery](site-recovery-active-directory.md) alle linee guida per la replica e la configurazione di un controller di dominio in Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="57bda-164">**Replica del server di database SQL**</span><span class="sxs-lookup"><span data-stu-id="57bda-164">**SQL database Server replication**</span></span>

<span data-ttu-id="57bda-165">Consultare troppo[proteggere SQL Server con il ripristino di emergenza di SQL Server e Azure Site Recovery](site-recovery-sql.md) per indicazioni tecniche dettagliate su hello consigliabile opzioni per la protezione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="57bda-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="57bda-166">Seguire [questa Guida](site-recovery-vmware-to-azure.md) toostart replica hello altri tooAzure di macchine virtuali del componente.</span><span class="sxs-lookup"><span data-stu-id="57bda-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![Protezione dei componenti di XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="57bda-168">**Impostazioni di Calcolo e rete**</span><span class="sxs-lookup"><span data-stu-id="57bda-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="57bda-169">Dopo che sono protetti macchine hello (stato viene visualizzato come "Protetto" in elementi replicati), hello calcolo e le impostazioni di rete necessario toobe configurato.</span><span class="sxs-lookup"><span data-stu-id="57bda-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="57bda-170">Nel calcolo e rete > calcolo proprietà, è possibile specificare dimensioni delle macchine Virtuali di Azure hello nome e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="57bda-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="57bda-171">Se si desidera, modificare toocomply nome hello ai requisiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="57bda-172">È inoltre possibile visualizzare e aggiungere le informazioni di rete di destinazione hello, subnet e indirizzi IP che verranno assegnato toohello macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="57bda-173">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="57bda-173">Note hello following:</span></span>

* <span data-ttu-id="57bda-174">È possibile impostare l'indirizzo IP di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="57bda-174">You can set hello target IP address.</span></span> <span data-ttu-id="57bda-175">Se non si fornisce un indirizzo, hello failover macchina utilizzerà DHCP.</span><span class="sxs-lookup"><span data-stu-id="57bda-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="57bda-176">Se si imposta un indirizzo che non è disponibile in caso di failover, failover hello non funzionerà.</span><span class="sxs-lookup"><span data-stu-id="57bda-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="57bda-177">Hello stesso indirizzo IP di destinazione è utilizzabile per il test failover se è disponibile in rete di failover di test hello hello indirizzo.</span><span class="sxs-lookup"><span data-stu-id="57bda-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="57bda-178">Per il server di Active Directory/DNS hello, mantenendo hello locale consente di indirizzo che specificare hello uguale indirizzo come server DNS hello per la rete virtuale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="57bda-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="57bda-179">numero di Hello di schede di rete dipende dalla dimensione hello specificata per la macchina virtuale di destinazione hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="57bda-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="57bda-180">Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale toohello numero di schede consentite per le dimensioni del computer di destinazione hello, quindi sarà necessario destinazione hello hello origine hello stesso numero di schede.</span><span class="sxs-lookup"><span data-stu-id="57bda-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="57bda-181">Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per la dimensione di destinazione hello quindi massimo di dimensioni di destinazione hello verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="57bda-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="57bda-182">Ad esempio, se un computer di origine dispone di due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, nel computer di destinazione hello avrà due schede.</span><span class="sxs-lookup"><span data-stu-id="57bda-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="57bda-183">Se il computer di origine hello dispone di due schede ma hello dimensioni di destinazione supportata supportano solo una macchina di destinazione hello avrà una sola scheda di.</span><span class="sxs-lookup"><span data-stu-id="57bda-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="57bda-184">Se più schede di rete nella macchina virtuale hello verranno tutti connettono toohello stessa rete.</span><span class="sxs-lookup"><span data-stu-id="57bda-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="57bda-185">Se macchina virtuale hello dispone di più schede di rete, hello primo quello riportato nell'elenco di hello diventa quindi scheda di rete predefinito hello in hello macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="57bda-186">Creazione di un piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="57bda-186">Creating a recovery plan</span></span>

<span data-ttu-id="57bda-187">Dopo la replica è abilitata per le macchine virtuali componente informazioni hello, hello è toocreate un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="57bda-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="57bda-188">Un piano di ripristino raggruppa le macchine virtuali con requisiti simili per il failover e il ripristino.</span><span class="sxs-lookup"><span data-stu-id="57bda-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="57bda-189">**Passaggi toocreate un piano di ripristino**</span><span class="sxs-lookup"><span data-stu-id="57bda-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="57bda-190">Aggiungi macchine virtuali di hello informazioni componente hello il piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="57bda-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="57bda-191">Fare clic su Piani di ripristino -> + Piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="57bda-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="57bda-192">Fornire un nome per il piano di ripristino hello intuitivo.</span><span class="sxs-lookup"><span data-stu-id="57bda-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="57bda-193">Per macchine virtuali VMware: selezionare il server di elaborazione VMware come origine, Microsoft Azure come destinazione e Resource Manager come modello di distribuzione, quindi fare clic su Seleziona elementi.</span><span class="sxs-lookup"><span data-stu-id="57bda-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="57bda-194">Per le macchine virtuali Hyper-V: selezionare l'origine come server VMM, come Microsoft Azure e il modello di distribuzione come Gestione risorse di destinazione e fare clic su selezionare gli elementi e quindi selezionare la distribuzione di informazioni di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="57bda-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="57bda-195">Aggiunta di gruppi toofailover macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="57bda-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="57bda-196">I piani di ripristino possono essere personalizzato tooadd failover gruppi per le azioni di avvio specifico ordine, script o manuale.</span><span class="sxs-lookup"><span data-stu-id="57bda-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="57bda-197">Hello seguenti gruppi necessario toobe toohello aggiunto piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="57bda-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="57bda-198">Gruppo di failover 1: DNS di AD</span><span class="sxs-lookup"><span data-stu-id="57bda-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="57bda-199">Gruppo di failover 2: VM SQL Server</span><span class="sxs-lookup"><span data-stu-id="57bda-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="57bda-200">Gruppo di failover 3: VM di immagine master VDA</span><span class="sxs-lookup"><span data-stu-id="57bda-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="57bda-201">Gruppo di failover 4: controller di distribuzione e VM del server StoreFront</span><span class="sxs-lookup"><span data-stu-id="57bda-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="57bda-202">Aggiunta di script toohello piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="57bda-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="57bda-203">Gli script possono essere eseguiti prima o dopo un gruppo specifico in un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="57bda-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="57bda-204">È anche possibile includere azioni manuali ed eseguirle durante il failover.</span><span class="sxs-lookup"><span data-stu-id="57bda-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="57bda-205">piano di ripristino personalizzata Hello è simile hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="57bda-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="57bda-206">Gruppo di failover 1: DNS di AD</span><span class="sxs-lookup"><span data-stu-id="57bda-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="57bda-207">Gruppo di failover 2: VM SQL Server</span><span class="sxs-lookup"><span data-stu-id="57bda-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="57bda-208">Gruppo di failover 3: VM di immagine master VDA</span><span class="sxs-lookup"><span data-stu-id="57bda-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="57bda-209">I passaggi 4, 6 e 7 contenente azioni manuali o uno script sono applicabili tooonly un informazioni locali > ambiente cataloghi MCS/PV.</span><span class="sxs-lookup"><span data-stu-id="57bda-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="57bda-210">Azione manuale o script di gruppo 3: hello VDA VM master di arresto Master VDA VM quando è stato eseguito il failover tooAzure sarà in uno stato di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="57bda-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="57bda-211">toocreate nuovo MCS cataloghi utilizzando Azure ARM hosting, master hello VDA VM è necessario toobe Stopped (de allocato) dello stato.</span><span class="sxs-lookup"><span data-stu-id="57bda-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="57bda-212">Hello arresto macchina virtuale dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="57bda-213">Gruppo di failover 4: controller di distribuzione e VM del server StoreFront</span><span class="sxs-lookup"><span data-stu-id="57bda-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="57bda-214">Gruppo 3 - Azione manuale o di script 1:</span><span class="sxs-lookup"><span data-stu-id="57bda-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="57bda-215">***Aggiungere una connessione host di Azure RM***</span><span class="sxs-lookup"><span data-stu-id="57bda-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="57bda-216">Crea connessione all'host di Azure ARM tooprovision computer Controller di recapito nuovi cataloghi MCS in Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="57bda-217">Seguire i passaggi di hello, come illustrato in questo [articolo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="57bda-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="57bda-218">Gruppo 3 - Azione manuale o di script 2:</span><span class="sxs-lookup"><span data-stu-id="57bda-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="57bda-219">***Ricreare i cataloghi MCS in Azure***</span><span class="sxs-lookup"><span data-stu-id="57bda-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="57bda-220">Hello esistente MCS o PV cloni nel sito primario di hello non saranno replicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="57bda-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="57bda-221">È necessario toorecreate i cloni utilizzando hello replicati VDA master e ARM Azure provisioning dal controller di recapito. Seguire i passaggi di hello, come illustrato in questo [articolo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS cataloghi in Azure.</span><span class="sxs-lookup"><span data-stu-id="57bda-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![Piano di ripristino per i componenti XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="57bda-223">È possibile utilizzare script in [percorso](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS con i nuovi indirizzi IP di hello failover hello > macchine virtuali o tooattach hello un bilanciamento del carico failover macchina virtuale, se necessario.</span><span class="sxs-lookup"><span data-stu-id="57bda-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="57bda-224">Esecuzione di un failover di test</span><span class="sxs-lookup"><span data-stu-id="57bda-224">Doing a test failover</span></span>

<span data-ttu-id="57bda-225">Seguire [questa Guida](site-recovery-test-failover-to-azure.md) toodo un failover di test.</span><span class="sxs-lookup"><span data-stu-id="57bda-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![Piano di ripristino](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="57bda-227">Esecuzione di un failover</span><span class="sxs-lookup"><span data-stu-id="57bda-227">Doing a failover</span></span>

<span data-ttu-id="57bda-228">Seguire [queste linee guida](site-recovery-failover.md) quando si esegue un failover.</span><span class="sxs-lookup"><span data-stu-id="57bda-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57bda-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57bda-229">Next steps</span></span>

<span data-ttu-id="57bda-230">Per [altre informazioni](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sulla replica di distribuzioni Citrix XenApp e XenDesktop, vedere questo white paper.</span><span class="sxs-lookup"><span data-stu-id="57bda-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="57bda-231">Esaminare indicazioni hello troppo[replicare altre applicazioni](site-recovery-workload.md) utilizzando il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="57bda-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
