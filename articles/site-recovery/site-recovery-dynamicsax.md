---
title: una distribuzione di Dynamics AX multilivello usando Azure Site Recovery aaaReplicate | Documenti Microsoft
description: Questo articolo viene descritto come tooreplicate e proteggere con Azure Site Recovery di Dynamics AX
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="626d6-103">Eseguire la replica di un'applicazione Dynamics AX multilivello usando Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="626d6-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="626d6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="626d6-104">Overview</span></span>


<span data-ttu-id="626d6-105">Microsoft Dynamics AX è una delle soluzioni ERP più diffusi di hello tra processo toostandardized aziende luoghi, gestire le risorse e semplificando la conformità.</span><span class="sxs-lookup"><span data-stu-id="626d6-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="626d6-106">In considerazione un'applicazione hello è organizzazione tooan critici di business è molto importante toobe assicurarsi che se ripristino di emergenza, applicazione deve essere in esecuzione nel tempo minimo.</span><span class="sxs-lookup"><span data-stu-id="626d6-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="626d6-107">Attualmente Microsoft Dynamics AX non include funzionalità di ripristino di emergenza predefinite.</span><span class="sxs-lookup"><span data-stu-id="626d6-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="626d6-108">Microsoft Dynamics AX è costituito da molti componenti server come applicazione oggetto Server, Active Directory (AD), Server di Database SQL, i SharePoint Server, Reporting e così via Server toomanage hello il ripristino di emergenza di ciascuno di questi componenti è manualmente non solo dispendiosa ma anche soggetto a errori.</span><span class="sxs-lookup"><span data-stu-id="626d6-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="626d6-109">Questo articolo descrive dettagliatamente come creare una soluzione di ripristino di emergenza per l'applicazione Dynamics AX usando [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="626d6-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="626d6-110">Vengono anche descritti i failover pianificati/non pianificati/di test tramite il piano di ripristino con un solo clic, le configurazioni supportate e i prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="626d6-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="626d6-111">La soluzione di ripristino di emergenza basata su Azure Site Recovery è completamente testata, certificata e consigliata da Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="626d6-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="626d6-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="626d6-112">Prerequisites</span></span>

<span data-ttu-id="626d6-113">L'implementazione di ripristino di emergenza per l'applicazione di Dynamics AX usando Azure Site Recovery richiede hello seguenti prerequisiti completati.</span><span class="sxs-lookup"><span data-stu-id="626d6-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="626d6-114">•   Configurare una distribuzione di Dynamics AX locale</span><span class="sxs-lookup"><span data-stu-id="626d6-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="626d6-115">•   Creare un insieme di credenziali dei servizi di Azure Site Recovery nella sottoscrizione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="626d6-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="626d6-116">• Se Azure è il sito di ripristino, eseguire lo strumento di valutazione della macchina virtuale Azure hello in tooensure macchine virtuali che sono compatibili con le macchine virtuali di Azure e servizi di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="626d6-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="626d6-117">Supporto di Site Recovery</span><span class="sxs-lookup"><span data-stu-id="626d6-117">Site Recovery support</span></span>

<span data-ttu-id="626d6-118">Ai fini di hello della creazione di questo articolo, macchine virtuali VMware con 2012R3 Dynamics AX in Windows Server 2012 R2 Enterprise sono state utilizzate.</span><span class="sxs-lookup"><span data-stu-id="626d6-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="626d6-119">Replica di ripristino del sito è indipendente dall'applicazione, indicazioni di hello forniti sono toohold previsto negli scenari seguenti.</span><span class="sxs-lookup"><span data-stu-id="626d6-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="626d6-120">Origine e destinazione</span><span class="sxs-lookup"><span data-stu-id="626d6-120">Source and target</span></span>

<span data-ttu-id="626d6-121">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="626d6-121">**Scenario**</span></span> | <span data-ttu-id="626d6-122">**sito secondario tooa**</span><span class="sxs-lookup"><span data-stu-id="626d6-122">**tooa secondary site**</span></span> | <span data-ttu-id="626d6-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="626d6-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="626d6-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="626d6-124">**Hyper-V**</span></span> | <span data-ttu-id="626d6-125">Sì</span><span class="sxs-lookup"><span data-stu-id="626d6-125">Yes</span></span> | <span data-ttu-id="626d6-126">Sì</span><span class="sxs-lookup"><span data-stu-id="626d6-126">Yes</span></span>
<span data-ttu-id="626d6-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="626d6-127">**VMware**</span></span> | <span data-ttu-id="626d6-128">Sì</span><span class="sxs-lookup"><span data-stu-id="626d6-128">Yes</span></span> | <span data-ttu-id="626d6-129">Sì</span><span class="sxs-lookup"><span data-stu-id="626d6-129">Yes</span></span>
<span data-ttu-id="626d6-130">**Server fisico**</span><span class="sxs-lookup"><span data-stu-id="626d6-130">**Physical server**</span></span> | <span data-ttu-id="626d6-131">Sì</span><span class="sxs-lookup"><span data-stu-id="626d6-131">Yes</span></span> | <span data-ttu-id="626d6-132">Sì</span><span class="sxs-lookup"><span data-stu-id="626d6-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="626d6-133">Abilitare il ripristino di emergenza dell'applicazione Dynamics AX con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="626d6-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="626d6-134">Proteggere l'applicazione Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="626d6-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="626d6-135">Ogni componente di hello Dynamics AX esigenze toobe protetti tooenable hello applicazione completa replica e il ripristino.</span><span class="sxs-lookup"><span data-stu-id="626d6-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="626d6-136">Questa sezione descrive queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="626d6-136">This section covers:</span></span>

<span data-ttu-id="626d6-137">**1. Protezione di Active Directory**</span><span class="sxs-lookup"><span data-stu-id="626d6-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="626d6-138">**2. Protezione del livello SQL**</span><span class="sxs-lookup"><span data-stu-id="626d6-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="626d6-139">**3. Protezione dei livelli app e Web**</span><span class="sxs-lookup"><span data-stu-id="626d6-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="626d6-140">**4. Configurazione delle impostazioni di rete**</span><span class="sxs-lookup"><span data-stu-id="626d6-140">**4. Networking configuration**</span></span>

<span data-ttu-id="626d6-141">**5. Piano di ripristino**</span><span class="sxs-lookup"><span data-stu-id="626d6-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="626d6-142">1. Configurare la replica di Active Directory e DNS</span><span class="sxs-lookup"><span data-stu-id="626d6-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="626d6-143">Active Directory è necessaria nel sito di ripristino di emergenza hello per toofunction applicazione Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="626d6-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="626d6-144">Esistono due opzioni consigliate in base hello complessità dell'ambiente locale del cliente hello.</span><span class="sxs-lookup"><span data-stu-id="626d6-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="626d6-145">**Opzione 1**</span><span class="sxs-lookup"><span data-stu-id="626d6-145">**Option 1**</span></span>

<span data-ttu-id="626d6-146">Se il cliente hello dispone di un numero ridotto di applicazioni e un singolo controller di dominio per il suo intero sito locale e verrà essersi verificato un errore sull'intero sito hello insieme, quindi è consigliabile utilizzare la replica di ripristino automatico di sistema tooreplicate hello controller di dominio computer toosecondary sito ( applicabile per sito tooSite e tooAzure sito).</span><span class="sxs-lookup"><span data-stu-id="626d6-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="626d6-147">**Opzione 2**</span><span class="sxs-lookup"><span data-stu-id="626d6-147">**Option 2**</span></span>

<span data-ttu-id="626d6-148">Se hello cliente ha un numero elevato di applicazioni e sia in esecuzione una foresta di Active Directory ed eseguirà il failover alcune applicazioni alla volta, quindi è consigliabile configurare un controller di dominio nel sito di ripristino di emergenza hello (sito secondario o in Azure).</span><span class="sxs-lookup"><span data-stu-id="626d6-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="626d6-149">Consultare troppo[guida complementare in rende disponibile un controller di dominio nel sito di ripristino di emergenza](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="626d6-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="626d6-150">Nella parte restante di questo documento si presuppone che nel sito di ripristino di emergenza sia disponibile un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="626d6-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="626d6-151">2. Configurare la replica di SQL Server</span><span class="sxs-lookup"><span data-stu-id="626d6-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="626d6-152">Per indicazioni tecniche dettagliate su hello consigliata l'opzione per la protezione, consultare Guida toocompanion [livello SQL](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="626d6-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="626d6-153">3. Abilitare la protezione per le VM AOS e client Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="626d6-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="626d6-154">Eseguire la configurazione di Azure Site Recovery pertinente in base alle macchine virtuali hello se distribuite in [Hyper-V](site-recovery-hyper-v-site-to-azure.md) oppure [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="626d6-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="626d6-155">Tooconfigure di frequenza coerente con l'arresto anomalo del sistema consigliata è di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="626d6-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="626d6-156">Hello seguito snapshot Mostra lo stato di protezione hello di macchine virtuali componente Dynamics in uno scenario di protezione 'TooAzure sito VMware'.</span><span class="sxs-lookup"><span data-stu-id="626d6-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="626d6-157">![Elementi protetti ](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="626d6-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="626d6-158">4. Configurare le impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="626d6-158">4. Configure Networking</span></span>
<span data-ttu-id="626d6-159">Configurare le impostazioni di calcolo e di rete delle VM</span><span class="sxs-lookup"><span data-stu-id="626d6-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="626d6-160">Per i client AX hello e le macchine virtuali AOS configurare le impostazioni di rete in Azure Site Recovery in modo che le reti VM hello ottenere toohello collegato corretto ripristino di emergenza rete dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="626d6-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="626d6-161">Verificare che sia di rete di ripristino di emergenza hello per questi livelli livello SQL toohello instradabile.</span><span class="sxs-lookup"><span data-stu-id="626d6-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="626d6-162">È possibile selezionare Ciao VM hello replicate le impostazioni di rete hello tooconfigure elementi come illustrato nello snapshot hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="626d6-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="626d6-163">Per i server AOS selezionare il set di disponibilità corretto hello.</span><span class="sxs-lookup"><span data-stu-id="626d6-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="626d6-164">Se si utilizza un indirizzo IP statico, specificare hello IP che si desidera hello tootake macchina virtuale in hello **indirizzo IP di destinazione** campo ![le impostazioni di rete](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="626d6-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="626d6-165">5. Creazione di un piano di ripristino</span><span class="sxs-lookup"><span data-stu-id="626d6-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="626d6-166">È possibile creare un piano di ripristino nel processo di failover di Azure Site Recovery tooautomate hello.</span><span class="sxs-lookup"><span data-stu-id="626d6-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="626d6-167">Aggiungere il livello di applicazione e web in hello il piano di ripristino.</span><span class="sxs-lookup"><span data-stu-id="626d6-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="626d6-168">Ordinarli in diversi gruppi in modo che hello front-end arresto prima di livello applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="626d6-169">Selezionare l'insieme di credenziali di Azure Site Recovery hello nella sottoscrizione e fare clic sul riquadro 'Piani di ripristino'.</span><span class="sxs-lookup"><span data-stu-id="626d6-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="626d6-170">Fare clic su "Crea piano di ripristino" e specificare un nome.</span><span class="sxs-lookup"><span data-stu-id="626d6-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="626d6-171">Selezionare hello 'Source' e 'Target'.</span><span class="sxs-lookup"><span data-stu-id="626d6-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="626d6-172">destinazione Hello può essere il sito secondario o di Azure.</span><span class="sxs-lookup"><span data-stu-id="626d6-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="626d6-173">Nel caso in cui si sceglie di Azure, è necessario specificare il modello di distribuzione hello</span><span class="sxs-lookup"><span data-stu-id="626d6-173">In case you choose Azure, you must specify hello deployment model</span></span>

![Crea piano di ripristino](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="626d6-175">Selezionare hello AOS e piano di ripristino toohello macchine virtuali di client e fare clic su ✓.</span><span class="sxs-lookup"><span data-stu-id="626d6-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="626d6-176">![Crea piano di ripristino](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="626d6-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Piano di ripristino](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="626d6-178">È possibile personalizzare il piano di ripristino hello per l'applicazione di Dynamics AX aggiungendo i vari passaggi come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="626d6-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="626d6-179">Hello sopra snapshot viene illustrato il piano di ripristino completo hello dopo l'aggiunta di tutti i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="626d6-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="626d6-180">*Passaggi:*</span><span class="sxs-lookup"><span data-stu-id="626d6-180">*Steps:*</span></span>

<span data-ttu-id="626d6-181">*1. Passaggi di failover di SQL Server*</span><span class="sxs-lookup"><span data-stu-id="626d6-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="626d6-182">Fare riferimento troppo['Soluzione di ripristino di emergenza di SQL Server'](site-recovery-sql.md) guida complementare per informazioni sul server tooSQL specifici passaggi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="626d6-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="626d6-183">*2. Failover gruppo 1: Eseguire il failover le macchine virtuali AOS hello*</span><span class="sxs-lookup"><span data-stu-id="626d6-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="626d6-184">Assicurarsi che il punto di ripristino hello selezionato sia il più vicino possibile toohello database PIT ma non-ahead.</span><span class="sxs-lookup"><span data-stu-id="626d6-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="626d6-185">*3. Script: Servizio di bilanciamento del carico Aggiungi (solo A E)* aggiungere uno script (tramite l'automazione di Azure) dopo il gruppo di VM AOS arriva tooadd un tooit di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="626d6-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="626d6-186">È possibile utilizzare un toodo script questa attività.</span><span class="sxs-lookup"><span data-stu-id="626d6-186">You can use a script toodo this task.</span></span> <span data-ttu-id="626d6-187">Vedere l'articolo [come tooadd bilanciamento del carico per applicazioni multilivello ripristino di emergenza](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="626d6-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="626d6-188">*4. Failover gruppo 2: Eseguire il failover client AX hello macchine virtuali.*</span><span class="sxs-lookup"><span data-stu-id="626d6-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="626d6-189">Il livello di web hello macchine virtuali come parte del piano di ripristino hello il failover.</span><span class="sxs-lookup"><span data-stu-id="626d6-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="626d6-190">Esecuzione di un failover di test</span><span class="sxs-lookup"><span data-stu-id="626d6-190">Doing a test failover</span></span>

<span data-ttu-id="626d6-191">Fare riferimento too'AD Solution ' e 'Soluzione di ripristino di emergenza di SQL Server' le guide complementari per considerazioni specifiche tooAD e SQL server rispettivamente durante il Failover di Test.</span><span class="sxs-lookup"><span data-stu-id="626d6-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="626d6-192">Passare tooAzure portale e selezionare l'insieme di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="626d6-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="626d6-193">Fare clic sul piano di ripristino hello creato per Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="626d6-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="626d6-194">Fare clic su "Failover di test".</span><span class="sxs-lookup"><span data-stu-id="626d6-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="626d6-195">Selezionare hello rete virtuale toostart hello il failover, il processo di test.</span><span class="sxs-lookup"><span data-stu-id="626d6-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="626d6-196">Una volta ambiente secondario hello è attivo, è possibile eseguire le convalide.</span><span class="sxs-lookup"><span data-stu-id="626d6-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="626d6-197">Dopo aver complete le convalide hello, è possibile selezionare 'Convalide completare' e ambiente di failover di test hello verrà pulita.</span><span class="sxs-lookup"><span data-stu-id="626d6-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="626d6-198">Seguire [questa Guida](site-recovery-test-failover-to-azure.md) toodo un failover di test.</span><span class="sxs-lookup"><span data-stu-id="626d6-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="626d6-199">Esecuzione di un failover</span><span class="sxs-lookup"><span data-stu-id="626d6-199">Doing a failover</span></span>

1.  <span data-ttu-id="626d6-200">Passare tooAzure portale e selezionare l'insieme di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="626d6-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="626d6-201">Fare clic sul piano di ripristino hello creato per Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="626d6-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="626d6-202">Fare clic su "Failover" e selezionare "Failover".</span><span class="sxs-lookup"><span data-stu-id="626d6-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="626d6-203">Selezionare la rete di destinazione hello e fare clic su processo di failover ✓ toostart hello.</span><span class="sxs-lookup"><span data-stu-id="626d6-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="626d6-204">Seguire [queste linee guida](site-recovery-failover.md) quando si esegue un failover.</span><span class="sxs-lookup"><span data-stu-id="626d6-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="626d6-205">Eseguire un failback</span><span class="sxs-lookup"><span data-stu-id="626d6-205">Perform a Failback</span></span>

<span data-ttu-id="626d6-206">Fare riferimento too'SQL soluzione di ripristino di emergenza Server "nella Guida complementare per server tooSQL specifiche considerazioni durante il Failback.</span><span class="sxs-lookup"><span data-stu-id="626d6-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="626d6-207">Passare tooAzure portale e selezionare l'insieme di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="626d6-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="626d6-208">Fare clic sul piano di ripristino hello creato per Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="626d6-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="626d6-209">Fare clic su "Failover" e selezionare il failover.</span><span class="sxs-lookup"><span data-stu-id="626d6-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="626d6-210">Fare clic su "Cambia direzione".</span><span class="sxs-lookup"><span data-stu-id="626d6-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="626d6-211">Selezionare le opzioni appropriate di hello - sincronizzazione dei dati e le opzioni di creazione di VM</span><span class="sxs-lookup"><span data-stu-id="626d6-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="626d6-212">Fare clic su ✓ toostart hello 'Failback' processo.</span><span class="sxs-lookup"><span data-stu-id="626d6-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="626d6-213">Seguire [queste linee guida](site-recovery-failback-azure-to-vmware.md) quando si esegue un failback.</span><span class="sxs-lookup"><span data-stu-id="626d6-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="626d6-214">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="626d6-214">Summary</span></span>
<span data-ttu-id="626d6-215">Con Azure Site Recovery è possibile creare un piano di ripristino di emergenza completamente automatico per l'applicazione Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="626d6-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="626d6-216">È possibile avviare il failover hello entro pochi secondi da qualsiasi posizione in hello evento di interruzione e ottenere un'applicazione hello attivo e in esecuzione in minuti.</span><span class="sxs-lookup"><span data-stu-id="626d6-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="626d6-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="626d6-217">Next steps</span></span>
<span data-ttu-id="626d6-218">Lettura [i carichi di lavoro è possibile proteggere?](site-recovery-workload.md) toolearn ulteriori informazioni sulla protezione di carichi di lavoro aziendali con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="626d6-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
