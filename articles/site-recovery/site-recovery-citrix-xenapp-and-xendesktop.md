---
title: Eseguire la replica di una distribuzione Citrix XenDesktop e XenApp con Azure Site Recovery | Microsoft Docs
description: Questo articolo illustra come proteggere e ripristinare le distribuzioni Citrix XenDesktop e XenApp con Azure Site Recovery.
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
ms.openlocfilehash: dc064352b1841ff346b705dc63186b12d79350b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="163dd-103">Eseguire la replica di una distribuzione Citrix XenApp e XenDesktop multilivello con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="163dd-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="163dd-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="163dd-104">Overview</span></span>

<span data-ttu-id="163dd-105">Citrix XenDesktop è una soluzione di virtualizzazione del desktop che fornisce desktop e applicazioni come servizi su richiesta a qualsiasi utente, ovunque si trovi.</span><span class="sxs-lookup"><span data-stu-id="163dd-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service to any user, anywhere.</span></span> <span data-ttu-id="163dd-106">Con la tecnologia di distribuzione FlexCast, XenDesktop può distribuire in modo rapido e sicuro applicazioni e desktop agli utenti.</span><span class="sxs-lookup"><span data-stu-id="163dd-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops to users.</span></span>
<span data-ttu-id="163dd-107">Citrix XenApp non fornisce attualmente funzionalità di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="163dd-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="163dd-108">Una soluzione di ripristino di emergenza valida deve consentire la modellazione dei piani di ripristino per le architetture di applicazioni complesse descritte in precedenza e consentire anche l'aggiunta di passaggi personalizzati per gestire i mapping delle applicazioni tra i vari livelli, fornendo una soluzione rapida e sicura in caso di emergenza, con un RTO inferiore.</span><span class="sxs-lookup"><span data-stu-id="163dd-108">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>

<span data-ttu-id="163dd-109">Questo documento fornisce indicazioni dettagliate per la creazione di una soluzione di ripristino di emergenza per le distribuzioni Citrix XenApp locali in piattaforme Hyper-V e VMware vSphere.</span><span class="sxs-lookup"><span data-stu-id="163dd-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="163dd-110">Questo documento illustra anche come eseguire un failover di test (esercitazione per il ripristino di emergenza) e un failover non pianificato in Azure usando piani di ripristino, configurazioni supportate e prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="163dd-110">This document also describes how to perform a test failover(disaster recovery drill) and unplanned failover to Azure using recovery plans, the supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="163dd-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="163dd-111">Prerequisites</span></span>

<span data-ttu-id="163dd-112">Prima di iniziare, è necessario comprendere i concetti illustrati di seguito:</span><span class="sxs-lookup"><span data-stu-id="163dd-112">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="163dd-113">Replica di una macchina virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="163dd-113">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="163dd-114">Come [progettare una rete di ripristino](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="163dd-114">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="163dd-115">Esecuzione di un failover di test in Azure</span><span class="sxs-lookup"><span data-stu-id="163dd-115">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="163dd-116">Esecuzione di un failover in Azure</span><span class="sxs-lookup"><span data-stu-id="163dd-116">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="163dd-117">Come [replicare un controller di dominio](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="163dd-117">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="163dd-118">Come [replicare SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="163dd-118">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="163dd-119">Modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="163dd-119">Deployment patterns</span></span>

<span data-ttu-id="163dd-120">Una farm Citrix XenApp e XenDesktop presenta in genere questo modello di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="163dd-120">A Citrix XenApp and XenDesktop farm typically has the following deployment pattern:</span></span>

<span data-ttu-id="163dd-121">**Modello di distribuzione**</span><span class="sxs-lookup"><span data-stu-id="163dd-121">**Deployment pattern**</span></span>

<span data-ttu-id="163dd-122">Distribuzione Citrix XenApp e XenDesktop con server DNS di AD, server di database SQL, Citrix Delivery Controller, server StoreFront, XenApp Master (VDA), server licenze di Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="163dd-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Modello di distribuzione 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="163dd-124">Supporto di Site Recovery</span><span class="sxs-lookup"><span data-stu-id="163dd-124">Site Recovery support</span></span>

<span data-ttu-id="163dd-125">Per le finalità di questo articolo, sono state usate distribuzioni Citrix in macchine virtuali VMware gestite da vSphere 6.0 / System Center VMM 2012 R2 per configurare il ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="163dd-125">For the purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used to setup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="163dd-126">Origine e destinazione</span><span class="sxs-lookup"><span data-stu-id="163dd-126">Source and target</span></span>

<span data-ttu-id="163dd-127">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="163dd-127">**Scenario**</span></span> | <span data-ttu-id="163dd-128">**In un sito secondario**</span><span class="sxs-lookup"><span data-stu-id="163dd-128">**To a secondary site**</span></span> | <span data-ttu-id="163dd-129">**In Azure**</span><span class="sxs-lookup"><span data-stu-id="163dd-129">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="163dd-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="163dd-130">**Hyper-V**</span></span> | <span data-ttu-id="163dd-131">Non nell'ambito</span><span class="sxs-lookup"><span data-stu-id="163dd-131">Not in scope</span></span> | <span data-ttu-id="163dd-132">Sì</span><span class="sxs-lookup"><span data-stu-id="163dd-132">Yes</span></span>
<span data-ttu-id="163dd-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="163dd-133">**VMware**</span></span> | <span data-ttu-id="163dd-134">Non nell'ambito</span><span class="sxs-lookup"><span data-stu-id="163dd-134">Not in scope</span></span> | <span data-ttu-id="163dd-135">Sì</span><span class="sxs-lookup"><span data-stu-id="163dd-135">Yes</span></span>
<span data-ttu-id="163dd-136">**Server fisico**</span><span class="sxs-lookup"><span data-stu-id="163dd-136">**Physical server**</span></span> | <span data-ttu-id="163dd-137">Non nell'ambito</span><span class="sxs-lookup"><span data-stu-id="163dd-137">Not in scope</span></span> | <span data-ttu-id="163dd-138">Sì</span><span class="sxs-lookup"><span data-stu-id="163dd-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="163dd-139">Versioni</span><span class="sxs-lookup"><span data-stu-id="163dd-139">Versions</span></span>
<span data-ttu-id="163dd-140">I clienti possono distribuire componenti di XenApp come macchine virtuali in esecuzione su Hyper-V o VMware oppure come server fisici.</span><span class="sxs-lookup"><span data-stu-id="163dd-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="163dd-141">Azure Site Recovery può proteggere le distribuzioni fisiche e virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-141">Azure Site Recovery can protect both physical and virtual deployments to Azure.</span></span>
<span data-ttu-id="163dd-142">Poiché XenApp 7.7 è supportato in Azure, è possibile eseguire il failover in Azure solo delle distribuzioni con queste versioni per il ripristino di emergenza o la migrazione.</span><span class="sxs-lookup"><span data-stu-id="163dd-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over to Azure for Disaster Recovery or migration.</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="163dd-143">Aspetti da considerare</span><span class="sxs-lookup"><span data-stu-id="163dd-143">Things to keep in mind</span></span>

1. <span data-ttu-id="163dd-144">Sono supportati la protezione e il ripristino delle distribuzioni locali con computer con sistema operativo Server per fornire app XenApp pubblicate e desktop XenApp pubblicati.</span><span class="sxs-lookup"><span data-stu-id="163dd-144">Protection and recovery of on-premises deployments using Server OS machines to deliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="163dd-145">Non sono supportati la protezione e il ripristino di distribuzioni locali con computer con sistema operativo Desktop per fornire VDI desktop per desktop virtuali client, incluso Windows 10.</span><span class="sxs-lookup"><span data-stu-id="163dd-145">Protection and recovery of on-premises deployments using desktop OS machines to deliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="163dd-146">Azure Site Recovery non supporta infatti il ripristino di computer con sistemi operativi Desktop.</span><span class="sxs-lookup"><span data-stu-id="163dd-146">This is because ASR does not support the recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="163dd-147">Alcuni tipi di desktop virtuale client, ad esempio</span><span class="sxs-lookup"><span data-stu-id="163dd-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="163dd-148">Windows 7, non sono inoltre ancora supportati per le licenze in Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="163dd-149">[Altre informazioni](https://azure.microsoft.com/pricing/licensing-faq/) sulle licenze per computer desktop client/server in Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="163dd-150">Azure Site Recovery non può replicare e proteggere cloni MCS o PVS locali esistenti.</span><span class="sxs-lookup"><span data-stu-id="163dd-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="163dd-151">È necessario ricreare questi cloni usando il provisioning di Azure RM dal controller di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="163dd-151">You need to recreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="163dd-152">NetScaler non può essere protetto tramite Azure Site Recovery perché NetScaler è basato su FreeBSD e Azure Site Recovery non supporta la protezione del sistema operativo FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="163dd-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="163dd-153">Sarebbe necessario distribuire e configurare una nuova appliance NetScaler da Azure Market dopo il failover in Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-153">You would need to deploy and configure a new NetScaler appliance from Azure Market place after failover to Azure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="163dd-154">Replica di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="163dd-154">Replicating virtual machines</span></span>

<span data-ttu-id="163dd-155">I componenti seguenti della distribuzione Citrix XenApp devono essere protetti per consentire la replica e il ripristino.</span><span class="sxs-lookup"><span data-stu-id="163dd-155">The following components of the Citrix XenApp deployment need to be protected to enable replication and recovery.</span></span>

* <span data-ttu-id="163dd-156">Protezione del server DNS di AD</span><span class="sxs-lookup"><span data-stu-id="163dd-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="163dd-157">Protezione del server di database SQL</span><span class="sxs-lookup"><span data-stu-id="163dd-157">Protection of SQL database server</span></span>
* <span data-ttu-id="163dd-158">Protezione di Citrix Delivery Controller</span><span class="sxs-lookup"><span data-stu-id="163dd-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="163dd-159">Protezione del server StoreFront</span><span class="sxs-lookup"><span data-stu-id="163dd-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="163dd-160">Protezione di XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="163dd-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="163dd-161">Protezione del server licenze di Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="163dd-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="163dd-162">**Replica del server DNS di AD**</span><span class="sxs-lookup"><span data-stu-id="163dd-162">**AD DNS server replication**</span></span>

<span data-ttu-id="163dd-163">Per indicazioni sulla replica e sulla configurazione di un controller di dominio in Azure, vedere [Proteggere Active Directory e DNS con Azure Site Recovery](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="163dd-163">Please refer to [Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="163dd-164">**Replica del server di database SQL**</span><span class="sxs-lookup"><span data-stu-id="163dd-164">**SQL database Server replication**</span></span>

<span data-ttu-id="163dd-165">Per informazioni tecniche dettagliate sulle opzioni consigliate per la protezione dei server SQL, vedere [Proteggere SQL Server con il ripristino di emergenza di SQL Server e Azure Site Recovery](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="163dd-165">Please refer to [Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on the recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="163dd-166">Per avviare la replica delle macchine virtuali degli altri componenti in Azure, vedere [queste indicazioni](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="163dd-166">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the other component virtual machines to Azure.</span></span>

![Protezione dei componenti di XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="163dd-168">**Impostazioni di Calcolo e rete**</span><span class="sxs-lookup"><span data-stu-id="163dd-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="163dd-169">Dopo avere completato la protezione dei computer (stato "Protetto" in Elementi replicati), è necessario configurare le impostazioni di Calcolo e rete.</span><span class="sxs-lookup"><span data-stu-id="163dd-169">After the machines are protected (status shows as “Protected” under Replicated Items), the Compute and Network settings need to be configured.</span></span>
<span data-ttu-id="163dd-170">In Calcolo e rete > Proprietà di calcolo è possibile specificare il nome e le dimensioni di destinazione della VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-170">In Compute and Network > Compute properties, you can specify the Azure VM name and target size.</span></span>
<span data-ttu-id="163dd-171">Se necessario, modificare il nome in modo che sia conforme ai requisiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-171">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="163dd-172">È anche possibile visualizzare e aggiungere le informazioni sulla rete di destinazione, la subnet e l'indirizzo IP che verranno assegnati alla macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-172">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span>

<span data-ttu-id="163dd-173">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="163dd-173">Note the following:</span></span>

* <span data-ttu-id="163dd-174">È possibile impostare l'indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="163dd-174">You can set the target IP address.</span></span> <span data-ttu-id="163dd-175">Se non si specifica un indirizzo, il computer di cui è stato eseguito il failover usa DHCP.</span><span class="sxs-lookup"><span data-stu-id="163dd-175">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="163dd-176">Se si imposta un indirizzo che non è disponibile al momento del failover, il failover non riesce.</span><span class="sxs-lookup"><span data-stu-id="163dd-176">If you set an address that isn't available at failover, the failover won't work.</span></span> <span data-ttu-id="163dd-177">Se l'indirizzo è disponibile nella rete di failover di test, è possibile usare lo stesso indirizzo IP di destinazione per il failover di test.</span><span class="sxs-lookup"><span data-stu-id="163dd-177">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

* <span data-ttu-id="163dd-178">Per il server di AD/DNS il mantenimento dell'indirizzo locale consente di specificare lo stesso indirizzo del server DNS per la rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-178">For the AD/DNS server, retaining the on-premises address lets you specify the same address as the DNS server for the Azure Virtual network.</span></span>

<span data-ttu-id="163dd-179">Il numero di schede di rete dipende dalle dimensioni specificate per la macchina virtuale di destinazione, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="163dd-179">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

*   <span data-ttu-id="163dd-180">Se il numero di schede di rete nella macchina di origine è minore o uguale al numero di schede consentite per la macchina di destinazione, la destinazione avrà lo stesso numero di schede dell’origine.</span><span class="sxs-lookup"><span data-stu-id="163dd-180">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
*   <span data-ttu-id="163dd-181">Se il numero di schede per la macchina virtuale di origine supera il numero consentito per le dimensioni di destinazione, verrà utilizzata la dimensione di destinazione massima.</span><span class="sxs-lookup"><span data-stu-id="163dd-181">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
* <span data-ttu-id="163dd-182">Ad esempio, se una macchina di origine ha due schede di rete e le dimensioni della macchina di destinazione ne supportano quattro, la macchina di destinazione avrà due schede.</span><span class="sxs-lookup"><span data-stu-id="163dd-182">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="163dd-183">Se la macchina di origine dispone di due schede ma le dimensioni di destinazione supportate ne consentono solo una, la macchina di destinazione avrà una sola scheda.</span><span class="sxs-lookup"><span data-stu-id="163dd-183">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>
*   <span data-ttu-id="163dd-184">Se la macchina virtuale ha più schede di rete, si connetteranno tutte alla stessa rete.</span><span class="sxs-lookup"><span data-stu-id="163dd-184">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
*   <span data-ttu-id="163dd-185">Se la macchina virtuale ha più schede di rete, la prima nell'elenco diventa la scheda di rete predefinita nella macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-185">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the Default network adapter in the Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="163dd-186">Creazione di un piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="163dd-186">Creating a recovery plan</span></span>

<span data-ttu-id="163dd-187">Dopo l'abilitazione della replica per le VM del componente XenApp, il passaggio successivo consiste nella creazione di un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="163dd-187">After replication is enabled for the XenApp component VMs, the next step is to create a recovery plan.</span></span>
<span data-ttu-id="163dd-188">Un piano di ripristino raggruppa le macchine virtuali con requisiti simili per il failover e il ripristino.</span><span class="sxs-lookup"><span data-stu-id="163dd-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="163dd-189">**Procedura per la creazione di un piano di ripristino**</span><span class="sxs-lookup"><span data-stu-id="163dd-189">**Steps to create a recovery plan**</span></span>

1. <span data-ttu-id="163dd-190">Aggiungere le macchine virtuali del componente XenApp nel piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="163dd-190">Add the XenApp component virtual machines in the Recovery Plan.</span></span>
2. <span data-ttu-id="163dd-191">Fare clic su Piani di ripristino -> + Piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="163dd-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="163dd-192">Specificare un nome intuitivo per il piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="163dd-192">Provide an intuitive name for the recovery plan.</span></span>
3. <span data-ttu-id="163dd-193">Per macchine virtuali VMware: selezionare il server di elaborazione VMware come origine, Microsoft Azure come destinazione e Resource Manager come modello di distribuzione, quindi fare clic su Seleziona elementi.</span><span class="sxs-lookup"><span data-stu-id="163dd-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="163dd-194">Per macchine virtuali Hyper-V: selezionare il server VMM come origine, Microsoft Azure come destinazione e Resource Manager come modello di distribuzione, quindi fare clic su Seleziona elementi e selezionare le VM della distribuzione XenApp.</span><span class="sxs-lookup"><span data-stu-id="163dd-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select the XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="163dd-195">Aggiunta di macchine virtuali a gruppi di failover</span><span class="sxs-lookup"><span data-stu-id="163dd-195">Adding virtual machines to failover groups</span></span>

<span data-ttu-id="163dd-196">I piani di ripristino possono essere personalizzati per aggiungere gruppi di failover per specificare determinati ordini di avvio, script o azioni manuali.</span><span class="sxs-lookup"><span data-stu-id="163dd-196">Recovery plans can be customized to add failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="163dd-197">I gruppi seguenti devono essere aggiunti al piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="163dd-197">The following groups need to be added to the recovery plan.</span></span>

1. <span data-ttu-id="163dd-198">Gruppo di failover 1: DNS di AD</span><span class="sxs-lookup"><span data-stu-id="163dd-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="163dd-199">Gruppo di failover 2: VM SQL Server</span><span class="sxs-lookup"><span data-stu-id="163dd-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="163dd-200">Gruppo di failover 3: VM di immagine master VDA</span><span class="sxs-lookup"><span data-stu-id="163dd-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="163dd-201">Gruppo di failover 4: controller di distribuzione e VM del server StoreFront</span><span class="sxs-lookup"><span data-stu-id="163dd-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="163dd-202">Aggiunta di script al piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="163dd-202">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="163dd-203">Gli script possono essere eseguiti prima o dopo un gruppo specifico in un piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="163dd-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="163dd-204">È anche possibile includere azioni manuali ed eseguirle durante il failover.</span><span class="sxs-lookup"><span data-stu-id="163dd-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="163dd-205">Il piano di ripristino personalizzato ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="163dd-205">The customized recovery plan looks like the below:</span></span>

1. <span data-ttu-id="163dd-206">Gruppo di failover 1: DNS di AD</span><span class="sxs-lookup"><span data-stu-id="163dd-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="163dd-207">Gruppo di failover 2: VM SQL Server</span><span class="sxs-lookup"><span data-stu-id="163dd-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="163dd-208">Gruppo di failover 3: VM di immagine master VDA</span><span class="sxs-lookup"><span data-stu-id="163dd-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="163dd-209">I passaggi 4, 6 e 7 contenenti le azioni manuali o di script sono applicabili solo a un ambiente XenApp locale con cataloghi MCS/PVS.</span><span class="sxs-lookup"><span data-stu-id="163dd-209">Steps 4, 6 and 7 containing manual or script actions are applicable to only an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="163dd-210">Gruppo 3 - Azione manuale o di script: arresto della VM VDA master. Quando viene eseguito il failover della VM VDA master in Azure, lo stato della VM sarà In esecuzione.</span><span class="sxs-lookup"><span data-stu-id="163dd-210">Group 3 Manual or script action: Shutdown master VDA VM The Master VDA VM when failed over to Azure will be in a running state.</span></span> <span data-ttu-id="163dd-211">Per creare nuovi cataloghi MCS usando l'hosting di Azure ARM, è necessario che lo stato della VM VDA master sia Arrestato (deallocato).</span><span class="sxs-lookup"><span data-stu-id="163dd-211">To create new MCS catalogs using Azure ARM hosting, the master VDA VM is required to be in Stopped (de allocated) state.</span></span> <span data-ttu-id="163dd-212">Arrestare la VM dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-212">Shutdown the VM from Azure Portal.</span></span>

5. <span data-ttu-id="163dd-213">Gruppo di failover 4: controller di distribuzione e VM del server StoreFront</span><span class="sxs-lookup"><span data-stu-id="163dd-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="163dd-214">Gruppo 3 - Azione manuale o di script 1:</span><span class="sxs-lookup"><span data-stu-id="163dd-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="163dd-215">***Aggiungere una connessione host di Azure RM***</span><span class="sxs-lookup"><span data-stu-id="163dd-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="163dd-216">Creare una connessione host di Azure ARM nel computer del controller di distribuzione per effettuare il provisioning di nuovi cataloghi MCS in Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-216">Create Azure ARM host connection in Delivery Controller machine to provision new MCS catalogs in Azure.</span></span> <span data-ttu-id="163dd-217">Seguire la procedura illustrata in questo [articolo](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="163dd-217">Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="163dd-218">Gruppo 3 - Azione manuale o di script 2:</span><span class="sxs-lookup"><span data-stu-id="163dd-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="163dd-219">***Ricreare i cataloghi MCS in Azure***</span><span class="sxs-lookup"><span data-stu-id="163dd-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="163dd-220">I cloni MCS o PVS esistenti nel sito primario non verranno replicati in Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-220">The existing MCS or PVS clones on the primary site will not be replicated to Azure.</span></span> <span data-ttu-id="163dd-221">È necessario ricreare questi cloni usando VDA master sottoposto a replica e il provisioning di Azure ARM dal controller di distribuzione. Seguire la procedura illustrata in questo [articolo](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) per creare cataloghi MCS in Azure.</span><span class="sxs-lookup"><span data-stu-id="163dd-221">You need to recreate these clones using the replicated master VDA and Azure ARM provisioning from Delivery controller.Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) to create MCS catalogs in Azure.</span></span>

![Piano di ripristino per i componenti XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="163dd-223">È possibile usare gli script disponibili in questa [pagina](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) per aggiornare DNS con i nuovi indirizzi IP delle macchine virtuali sottoposte a failover oppure per collegare un servizio di bilanciamento del carico alle macchine virtuali sottoposte a failover, se necessario.</span><span class="sxs-lookup"><span data-stu-id="163dd-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) to update the DNS with the new IPs of the failed over >virtual machines or to attach a load balancer on the failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="163dd-224">Esecuzione di un failover di test</span><span class="sxs-lookup"><span data-stu-id="163dd-224">Doing a test failover</span></span>

<span data-ttu-id="163dd-225">Seguire [queste linee guida](site-recovery-test-failover-to-azure.md) per eseguire un failover di test.</span><span class="sxs-lookup"><span data-stu-id="163dd-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

![Piano di ripristino](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="163dd-227">Esecuzione di un failover</span><span class="sxs-lookup"><span data-stu-id="163dd-227">Doing a failover</span></span>

<span data-ttu-id="163dd-228">Seguire [queste linee guida](site-recovery-failover.md) quando si esegue un failover.</span><span class="sxs-lookup"><span data-stu-id="163dd-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="163dd-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="163dd-229">Next steps</span></span>

<span data-ttu-id="163dd-230">Per [altre informazioni](https://aka.ms/citrix-xenapp-xendesktop-with-asr) sulla replica di distribuzioni Citrix XenApp e XenDesktop, vedere questo white paper.</span><span class="sxs-lookup"><span data-stu-id="163dd-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="163dd-231">Sono disponibili indicazioni sulla [replica di altre applicazioni](site-recovery-workload.md) con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="163dd-231">Look at the guidance to [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
