---
title: Eseguire la replica di una distribuzione di Dynamics AX multilivello con Azure Site Recovery | Microsoft Docs
description: Questo articolo descrive come eseguire la replica e proteggere Dynamics AX usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="a5d21-103">Eseguire la replica di un'applicazione Dynamics AX multilivello usando Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a5d21-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="a5d21-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a5d21-104">Overview</span></span>


<span data-ttu-id="a5d21-105">Microsoft Dynamics AX è una delle soluzioni ERP più diffuse tra le aziende per standardizzare i processi tra località, gestire le risorse e semplificare la conformità.</span><span class="sxs-lookup"><span data-stu-id="a5d21-105">Microsoft Dynamics AX is one of the most popular ERP solution among enterprises to standardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="a5d21-106">Poiché si tratta di un'applicazione aziendale critica per un'organizzazione, è molto importante fare in modo che l'applicazione sia operativa in tempi minimi nel caso di un evento di emergenza.</span><span class="sxs-lookup"><span data-stu-id="a5d21-106">Considering the application is business critical to an organization it is very important to be sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="a5d21-107">Attualmente Microsoft Dynamics AX non include funzionalità di ripristino di emergenza predefinite.</span><span class="sxs-lookup"><span data-stu-id="a5d21-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="a5d21-108">Microsoft Dynamics AX include molti componenti server come Application Object Server (AOS), Active Directory, il server di database SQL, SharePoint Server, Reporting Server e così via. La gestione manuale del ripristino di emergenza di ognuno di questi componenti non solo è costosa, ma è anche soggetta a errori.</span><span class="sxs-lookup"><span data-stu-id="a5d21-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. To manage the disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="a5d21-109">Questo articolo descrive dettagliatamente come creare una soluzione di ripristino di emergenza per l'applicazione Dynamics AX usando [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5d21-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="a5d21-110">Vengono anche descritti i failover pianificati/non pianificati/di test tramite il piano di ripristino con un solo clic, le configurazioni supportate e i prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="a5d21-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="a5d21-111">La soluzione di ripristino di emergenza basata su Azure Site Recovery è completamente testata, certificata e consigliata da Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="a5d21-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="a5d21-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5d21-112">Prerequisites</span></span>

<span data-ttu-id="a5d21-113">Per l'implementazione del ripristino di emergenza per l'applicazione Dynamics AX con Azure Site Recovery, è necessario soddisfare i prerequisiti seguenti.</span><span class="sxs-lookup"><span data-stu-id="a5d21-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires the following pre-requisites completed.</span></span>

<span data-ttu-id="a5d21-114">•   Configurare una distribuzione di Dynamics AX locale</span><span class="sxs-lookup"><span data-stu-id="a5d21-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="a5d21-115">•   Creare un insieme di credenziali dei servizi di Azure Site Recovery nella sottoscrizione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a5d21-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="a5d21-116">•   Se Azure è il sito di ripristino, eseguire lo strumento di valutazione della conformità delle macchine virtuali di Azure nelle VM per garantire che siano compatibili con le VM di Azure e i servizi di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a5d21-116">•   If Azure is your recovery site, run the Azure Virtual Machine Readiness Assessment tool  on VMs to ensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="a5d21-117">Supporto di Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a5d21-117">Site Recovery support</span></span>

<span data-ttu-id="a5d21-118">Ai fini di questo articolo sono state usate macchine virtuali VMware con Dynamics AX 2012R3 su Windows Server 2012 R2 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a5d21-118">For the purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="a5d21-119">Poiché la replica di Site Recovery è indipendente dall'applicazione, i consigli inclusi in questo articolo saranno validi anche per gli scenari seguenti.</span><span class="sxs-lookup"><span data-stu-id="a5d21-119">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="a5d21-120">Origine e destinazione</span><span class="sxs-lookup"><span data-stu-id="a5d21-120">Source and target</span></span>

<span data-ttu-id="a5d21-121">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="a5d21-121">**Scenario**</span></span> | <span data-ttu-id="a5d21-122">**In un sito secondario**</span><span class="sxs-lookup"><span data-stu-id="a5d21-122">**To a secondary site**</span></span> | <span data-ttu-id="a5d21-123">**In Azure**</span><span class="sxs-lookup"><span data-stu-id="a5d21-123">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="a5d21-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="a5d21-124">**Hyper-V**</span></span> | <span data-ttu-id="a5d21-125">Sì</span><span class="sxs-lookup"><span data-stu-id="a5d21-125">Yes</span></span> | <span data-ttu-id="a5d21-126">Sì</span><span class="sxs-lookup"><span data-stu-id="a5d21-126">Yes</span></span>
<span data-ttu-id="a5d21-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="a5d21-127">**VMware**</span></span> | <span data-ttu-id="a5d21-128">Sì</span><span class="sxs-lookup"><span data-stu-id="a5d21-128">Yes</span></span> | <span data-ttu-id="a5d21-129">Sì</span><span class="sxs-lookup"><span data-stu-id="a5d21-129">Yes</span></span>
<span data-ttu-id="a5d21-130">**Server fisico**</span><span class="sxs-lookup"><span data-stu-id="a5d21-130">**Physical server**</span></span> | <span data-ttu-id="a5d21-131">Sì</span><span class="sxs-lookup"><span data-stu-id="a5d21-131">Yes</span></span> | <span data-ttu-id="a5d21-132">Sì</span><span class="sxs-lookup"><span data-stu-id="a5d21-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="a5d21-133">Abilitare il ripristino di emergenza dell'applicazione Dynamics AX con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a5d21-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="a5d21-134">Proteggere l'applicazione Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="a5d21-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="a5d21-135">Ogni componente di Dynamics AX deve essere protetto per consentire la replica e il ripristino completi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a5d21-135">Each component of the Dynamics AX needs to be protected to enable the complete application replication and recovery.</span></span> <span data-ttu-id="a5d21-136">Questa sezione descrive queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="a5d21-136">This section covers:</span></span>

<span data-ttu-id="a5d21-137">**1. Protezione di Active Directory**</span><span class="sxs-lookup"><span data-stu-id="a5d21-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="a5d21-138">**2. Protezione del livello SQL**</span><span class="sxs-lookup"><span data-stu-id="a5d21-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="a5d21-139">**3. Protezione dei livelli app e Web**</span><span class="sxs-lookup"><span data-stu-id="a5d21-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="a5d21-140">**4. Configurazione delle impostazioni di rete**</span><span class="sxs-lookup"><span data-stu-id="a5d21-140">**4. Networking configuration**</span></span>

<span data-ttu-id="a5d21-141">**5. Piano di ripristino**</span><span class="sxs-lookup"><span data-stu-id="a5d21-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="a5d21-142">1. Configurare la replica di Active Directory e DNS</span><span class="sxs-lookup"><span data-stu-id="a5d21-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="a5d21-143">Ai fini del funzionamento dell'applicazione Dynamics AX, nel sito di ripristino di emergenza deve essere presente Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a5d21-143">Active Directory is required on the DR site for Dynamics AX application to function.</span></span> <span data-ttu-id="a5d21-144">Le scelte consigliate sono due, a seconda della complessità dell'ambiente locale del cliente.</span><span class="sxs-lookup"><span data-stu-id="a5d21-144">There are two recommended choices based on the complexity of the customer’s on-premises environment.</span></span>

<span data-ttu-id="a5d21-145">**Opzione 1**</span><span class="sxs-lookup"><span data-stu-id="a5d21-145">**Option 1**</span></span>

<span data-ttu-id="a5d21-146">Se il cliente ha un numero limitato di applicazioni e un singolo controller di dominio per l'intero sito locale ed eseguirà il failover dell'intero sito, è consigliabile usare ASR-Replication per la replica del computer del controller di dominio nel sito secondario (applicabile sia per l'operazione da sito a sito sia per l'operazione da sito ad Azure).</span><span class="sxs-lookup"><span data-stu-id="a5d21-146">If the customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over the entire site together, then we recommend using ASR-Replication to replicate the DC machine to secondary site (applicable for both Site to Site and Site to Azure).</span></span>

<span data-ttu-id="a5d21-147">**Opzione 2**</span><span class="sxs-lookup"><span data-stu-id="a5d21-147">**Option 2**</span></span>

<span data-ttu-id="a5d21-148">Se il cliente ha un numero elevato di applicazioni, esegue una foresta Active Directory ed eseguirà il failover di poche applicazioni per volta, è consigliabile configurare un controller di dominio aggiuntivo nel sito di ripristino di emergenza (sito secondario in Azure).</span><span class="sxs-lookup"><span data-stu-id="a5d21-148">If the customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on the DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="a5d21-149">Fare riferimento alla [guida complementare su come rendere disponibile un controller di dominio nel sito di ripristino di emergenza](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a5d21-149">Please refer to [companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="a5d21-150">Nella parte restante di questo documento si presuppone che nel sito di ripristino di emergenza sia disponibile un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="a5d21-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="a5d21-151">2. Configurare la replica di SQL Server</span><span class="sxs-lookup"><span data-stu-id="a5d21-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="a5d21-152">Per indicazioni tecniche dettagliate sulle opzioni consigliate per la protezione del [livello SQL](site-recovery-sql.md), fare riferimento alla guida complementare.</span><span class="sxs-lookup"><span data-stu-id="a5d21-152">Please refer to companion guide  for detailed technical guidance on the recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="a5d21-153">3. Abilitare la protezione per le VM AOS e client Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="a5d21-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="a5d21-154">Eseguire la configurazione di Azure Site Recovery pertinente a seconda che le VM vengano distribuite in [Hyper-V](site-recovery-hyper-v-site-to-azure.md) o [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a5d21-154">Perform relevant Azure Site Recovery configuration based on whether the VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="a5d21-155">La frequenza consigliata per la coerenza in caso di arresto anomalo è 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="a5d21-155">Recommended Crash consistent frequency to configure is 15 minutes.</span></span>
>

<span data-ttu-id="a5d21-156">Lo snapshot seguente mostra lo stato di protezione delle VM del componente Dynamics in uno scenario di protezione "Da sito VMware ad Azure".</span><span class="sxs-lookup"><span data-stu-id="a5d21-156">The below snapshot shows the protection status of Dynamics component VMs in ‘VMware site to Azure’ protection scenario.</span></span>
<span data-ttu-id="a5d21-157">![Elementi protetti ](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="a5d21-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="a5d21-158">4. Configurare le impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="a5d21-158">4. Configure Networking</span></span>
<span data-ttu-id="a5d21-159">Configurare le impostazioni di calcolo e di rete delle VM</span><span class="sxs-lookup"><span data-stu-id="a5d21-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="a5d21-160">Per le macchine virtuali AOS e il client AX, configurare le impostazioni di rete in Azure Site Recovery in modo che le reti delle macchine virtuali siano collegate alla rete di ripristino di emergenza corretta dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="a5d21-160">For the AX client and AOS VMs configure network settings in Azure Site Recovery so that the VM networks get attached to the right DR network after failover.</span></span> <span data-ttu-id="a5d21-161">Assicurarsi che la rete di ripristino di emergenza per questi livelli possa essere instradata al livello SQL.</span><span class="sxs-lookup"><span data-stu-id="a5d21-161">Ensure the DR network for these tiers is routable to the SQL tier.</span></span>

<span data-ttu-id="a5d21-162">È possibile selezionare la VM negli elementi replicati per configurare le impostazioni di rete come mostrato nello snapshot seguente.</span><span class="sxs-lookup"><span data-stu-id="a5d21-162">You can select the VM in the replicated items to configure the network settings as shown in the snapshot below.</span></span>

* <span data-ttu-id="a5d21-163">Per i server AOS, selezionare il set di disponibilità corretto.</span><span class="sxs-lookup"><span data-stu-id="a5d21-163">For AOS servers select the correct availability set.</span></span>

* <span data-ttu-id="a5d21-164">Se si usa un indirizzo IP statico, specificare l'indirizzo IP che dovrà essere usato dalla macchina virtuale nel campo **IP di destinazione** ![Impostazioni di rete ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="a5d21-164">If you are using a static IP then specify the IP that you want the virtual machine to take in the **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="a5d21-165">5. Creazione di un piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="a5d21-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="a5d21-166">È possibile creare un piano di ripristino in Azure Site Recovery per automatizzare il processo di failover.</span><span class="sxs-lookup"><span data-stu-id="a5d21-166">You can create a recovery plan in Azure Site Recovery to automate the failover process.</span></span> <span data-ttu-id="a5d21-167">Aggiungere il livello app e il livello Web nel piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="a5d21-167">Add app tier and web tier in the Recovery Plan.</span></span> <span data-ttu-id="a5d21-168">Ordinare i livelli in gruppi diversi in modo che il front-end si arresti prima del livello app.</span><span class="sxs-lookup"><span data-stu-id="a5d21-168">Order them in different groups so that the front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="a5d21-169">Selezionare l'insieme di credenziali di Azure Site Recovery nella sottoscrizione e fare clic sul riquadro "Piani di ripristino".</span><span class="sxs-lookup"><span data-stu-id="a5d21-169">Select the Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="a5d21-170">Fare clic su "Crea piano di ripristino" e specificare un nome.</span><span class="sxs-lookup"><span data-stu-id="a5d21-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="a5d21-171">Selezionare i valori desiderati per "Origine" e "Destinazione".</span><span class="sxs-lookup"><span data-stu-id="a5d21-171">Select the ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="a5d21-172">La destinazione può essere Azure o il sito secondario.</span><span class="sxs-lookup"><span data-stu-id="a5d21-172">The target can be Azure or secondary site.</span></span> <span data-ttu-id="a5d21-173">Se si sceglie Azure, è necessario specificare il modello di distribuzione</span><span class="sxs-lookup"><span data-stu-id="a5d21-173">In case you choose Azure, you must specify the deployment model</span></span>

![Crea piano di ripristino](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="a5d21-175">Selezionare le VM AOS e client nel piano di ripristino e fare clic su ✓.</span><span class="sxs-lookup"><span data-stu-id="a5d21-175">Select the AOS and client VMs to the recovery plan and click ✓.</span></span>
<span data-ttu-id="a5d21-176">![Crea piano di ripristino](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="a5d21-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Piano di ripristino](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="a5d21-178">È possibile personalizzare il piano di ripristino per l'applicazione Dynamics AX aggiungendo diversi passaggi, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="a5d21-178">You can customize the recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="a5d21-179">Lo snapshot precedente mostra il piano di ripristino completo dopo aver aggiunto tutti i passaggi.</span><span class="sxs-lookup"><span data-stu-id="a5d21-179">The above snapshot shows the complete recovery plan after adding all the steps.</span></span>

<span data-ttu-id="a5d21-180">*Passaggi:*</span><span class="sxs-lookup"><span data-stu-id="a5d21-180">*Steps:*</span></span>

<span data-ttu-id="a5d21-181">*1. Passaggi di failover di SQL Server*</span><span class="sxs-lookup"><span data-stu-id="a5d21-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="a5d21-182">Fare riferimento alla guida complementare [Soluzione di ripristino di emergenza di SQL Server](site-recovery-sql.md) per informazioni sui passaggi di ripristino specifici per SQL server.</span><span class="sxs-lookup"><span data-stu-id="a5d21-182">Refer to [‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific to SQL server.</span></span>

<span data-ttu-id="a5d21-183">*2. Gruppo di failover 1: eseguire il failover delle macchine virtuali AOS*</span><span class="sxs-lookup"><span data-stu-id="a5d21-183">*2. Failover Group 1: Fail over the AOS VMs*</span></span>

<span data-ttu-id="a5d21-184">Assicurarsi che il punto di recupero selezionato sia quanto più vicino al ripristino temporizzato del database, ma che non sia in anticipo.</span><span class="sxs-lookup"><span data-stu-id="a5d21-184">Make sure that the recovery point selected is as close as possible to the database PIT but not ahead.</span></span>

<span data-ttu-id="a5d21-185">*3. Script: aggiungere il bilanciamento del carico (solo E-A)*. Aggiungere uno script (tramite l'automazione di Azure) dopo la visualizzazione del gruppo di VM AOS per aggiungere il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="a5d21-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up to add a load balancer to it.</span></span> <span data-ttu-id="a5d21-186">A questo scopo, è possibile usare uno script.</span><span class="sxs-lookup"><span data-stu-id="a5d21-186">You can use a script to do this task.</span></span> <span data-ttu-id="a5d21-187">Fare riferimento all'articolo [How to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/) (Come aggiungere il bilanciamento del carico per il ripristino di emergenza di applicazioni multilivello)</span><span class="sxs-lookup"><span data-stu-id="a5d21-187">Refer article [how to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="a5d21-188">*4. Gruppo di failover 2: eseguire il failover delle macchine virtuali client AX.*</span><span class="sxs-lookup"><span data-stu-id="a5d21-188">*4. Failover Group 2: Fail over the AX client VMs.*</span></span>
<span data-ttu-id="a5d21-189">Eseguire il failover delle macchine virtuali di livello Web come parte del piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="a5d21-189">Fail over the web tier VMs as part of the recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="a5d21-190">Esecuzione di un failover di test</span><span class="sxs-lookup"><span data-stu-id="a5d21-190">Doing a test failover</span></span>

<span data-ttu-id="a5d21-191">Fare riferimento alle guide complementari "Soluzione di ripristino di emergenza di Active Directory" e "Soluzione di ripristino di emergenza di SQL Server" per le considerazioni specifiche rispettivamente di Active Directory e SQL Server durante il failover di test.</span><span class="sxs-lookup"><span data-stu-id="a5d21-191">Refer to ‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific to AD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="a5d21-192">Accedere al portale di Azure e selezionare l'insieme di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a5d21-192">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="a5d21-193">Fare clic sul piano di ripristino creato per Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="a5d21-193">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="a5d21-194">Fare clic su "Failover di test".</span><span class="sxs-lookup"><span data-stu-id="a5d21-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="a5d21-195">Selezionare la rete virtuale per avviare il processo di failover di test.</span><span class="sxs-lookup"><span data-stu-id="a5d21-195">Select the virtual network to start the test fail-over process.</span></span>
5.  <span data-ttu-id="a5d21-196">Quando l'ambiente secondario è disponibile, è possibile eseguire le convalide.</span><span class="sxs-lookup"><span data-stu-id="a5d21-196">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="a5d21-197">Al termine delle convalide è possibile selezionare 'Convalide complete' per pulire l'ambiente di failover di test.</span><span class="sxs-lookup"><span data-stu-id="a5d21-197">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

<span data-ttu-id="a5d21-198">Seguire [queste linee guida](site-recovery-test-failover-to-azure.md) per eseguire un failover di test.</span><span class="sxs-lookup"><span data-stu-id="a5d21-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="a5d21-199">Esecuzione di un failover</span><span class="sxs-lookup"><span data-stu-id="a5d21-199">Doing a failover</span></span>

1.  <span data-ttu-id="a5d21-200">Accedere al portale di Azure e selezionare l'insieme di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a5d21-200">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="a5d21-201">Fare clic sul piano di ripristino creato per Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="a5d21-201">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="a5d21-202">Fare clic su "Failover" e selezionare "Failover".</span><span class="sxs-lookup"><span data-stu-id="a5d21-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="a5d21-203">Selezionare la rete di destinazione e quindi fare clic su ✓ per avviare il processo di failover.</span><span class="sxs-lookup"><span data-stu-id="a5d21-203">Select the target network and click ✓ to start the failover process.</span></span>

<span data-ttu-id="a5d21-204">Seguire [queste linee guida](site-recovery-failover.md) quando si esegue un failover.</span><span class="sxs-lookup"><span data-stu-id="a5d21-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="a5d21-205">Eseguire un failback</span><span class="sxs-lookup"><span data-stu-id="a5d21-205">Perform a Failback</span></span>

<span data-ttu-id="a5d21-206">Fare riferimento alla guida complementare "Soluzione di ripristino di emergenza di SQL Server" per le considerazioni specifiche di SQL Server durante il failback.</span><span class="sxs-lookup"><span data-stu-id="a5d21-206">Refer to ‘SQL Server DR Solution ’ companion guide for considerations specific to SQL server during Failback.</span></span>

1.  <span data-ttu-id="a5d21-207">Accedere al portale di Azure e selezionare l'insieme di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a5d21-207">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="a5d21-208">Fare clic sul piano di ripristino creato per Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="a5d21-208">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="a5d21-209">Fare clic su "Failover" e selezionare il failover.</span><span class="sxs-lookup"><span data-stu-id="a5d21-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="a5d21-210">Fare clic su "Cambia direzione".</span><span class="sxs-lookup"><span data-stu-id="a5d21-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="a5d21-211">Selezionare le opzioni di sincronizzazione dei dati e di creazione delle VM appropriate</span><span class="sxs-lookup"><span data-stu-id="a5d21-211">Select the appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="a5d21-212">Fare clic su ✓ per avviare il processo di failback.</span><span class="sxs-lookup"><span data-stu-id="a5d21-212">Click ✓ to start the ‘Failback’ process.</span></span>


<span data-ttu-id="a5d21-213">Seguire [queste linee guida](site-recovery-failback-azure-to-vmware.md) quando si esegue un failback.</span><span class="sxs-lookup"><span data-stu-id="a5d21-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="a5d21-214">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="a5d21-214">Summary</span></span>
<span data-ttu-id="a5d21-215">Con Azure Site Recovery è possibile creare un piano di ripristino di emergenza completamente automatico per l'applicazione Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="a5d21-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="a5d21-216">È possibile avviare il failover in pochi secondi da qualsiasi luogo in caso di un'interruzione, perché l'applicazione sia operativa in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a5d21-216">You can initiate the failover within seconds from anywhere in the event of a disruption and get the application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5d21-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5d21-217">Next steps</span></span>
<span data-ttu-id="a5d21-218">Per altre informazioni sulla protezione dei carichi di lavoro aziendali con Azure Site Recovery, leggere [Quali carichi di lavoro è possibile proteggere?](site-recovery-workload.md).</span><span class="sxs-lookup"><span data-stu-id="a5d21-218">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
