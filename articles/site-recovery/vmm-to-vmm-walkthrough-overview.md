---
title: aaaReplicate macchine virtuali Hyper-V tooa VMM del sito secondario con Azure Site Recovery | Documenti Microsoft
description: Fornisce una panoramica per la replica delle macchine virtuali Hyper-V tooa sito VMM secondario tramite hello portale di Azure.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="0d19b-103">Replicare le macchine virtuali Hyper-V in VMM cloud tooa VMM del sito secondario</span><span class="sxs-lookup"><span data-stu-id="0d19b-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d19b-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0d19b-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="0d19b-105">Portale classico</span><span class="sxs-lookup"><span data-stu-id="0d19b-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="0d19b-106">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="0d19b-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="0d19b-107">In questo articolo viene fornita una panoramica dei passaggi necessari tooreplicate locale macchine virtuali di Hyper-V (VM) gestite nei cloud di System Center Virtual Machine Manager (VMM), tooa percorso secondario di VMM, hello utilizzando [Azure Site Recovery](site-recovery-overview.md)in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d19b-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="0d19b-108">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0d19b-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="0d19b-109">Passaggio 1: Esaminare l'architettura dello scenario hello</span><span class="sxs-lookup"><span data-stu-id="0d19b-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="0d19b-110">Prima di avviare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di aver compreso tutti i componenti di hello è necessario toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0d19b-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="0d19b-111">Andare troppo[passaggio 1: esaminare l'architettura di hello](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="0d19b-112">Passaggio 2: Esaminare i prerequisiti e le limitazioni</span><span class="sxs-lookup"><span data-stu-id="0d19b-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="0d19b-113">Assicurarsi di comprendere le limitazioni e prerequisiti di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="0d19b-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="0d19b-114">**Prerequisiti di Azure**: È necessaria una sottoscrizione di Microsoft Azure e servizi di ripristino di Azure dell'insieme di credenziali, tooorchestrate e gestire la replica.</span><span class="sxs-lookup"><span data-stu-id="0d19b-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="0d19b-115">**Server VMM locali e host Hyper-V**: assicurarsi che i server VMM e gli host Hyper-V siano conformi e preparati per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0d19b-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="0d19b-116">Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="0d19b-117">Passaggio 3: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="0d19b-117">Step 3: Plan networking</span></span>

<span data-ttu-id="0d19b-118">È necessario toodo alcuni pianificazione che è possibile configurare i mapping di rete tra le reti VM di VMM quando si distribuisce uno scenario di hello tooensure della rete.</span><span class="sxs-lookup"><span data-stu-id="0d19b-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="0d19b-119">Andare troppo[passaggio 3: pianificare la rete](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="0d19b-120">Passaggio 4: Preparare VMM e Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0d19b-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="0d19b-121">Preparare i server VMM hello e host Hyper-V per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0d19b-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="0d19b-122">Andare troppo[passaggio 4: preparare i server locali](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="0d19b-123">Passaggio 5: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="0d19b-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="0d19b-124">Configurare un insieme di credenziali dei Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0d19b-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="0d19b-125">insieme di credenziali Hello contiene impostazioni di configurazione e Orchestra la replica.</span><span class="sxs-lookup"><span data-stu-id="0d19b-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="0d19b-126">[Passaggio 5: Configurare un insieme di credenziali](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="0d19b-127">Passaggio 6: Configurare le impostazioni di origine e destinazione</span><span class="sxs-lookup"><span data-stu-id="0d19b-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="0d19b-128">Impostare hello ubicazioni VMM replica origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0d19b-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="0d19b-129">Aggiungi insieme di credenziali toohello server VMM hello e scaricare i file di installazione hello per i componenti di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0d19b-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="0d19b-130">Eseguire l'installazione di Provider di Azure Site Recovery nel server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="0d19b-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="0d19b-131">Il programma di installazione installa hello Provider nel server VMM hello e registra il server hello nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="0d19b-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="0d19b-132">Installare l'agente di servizi di ripristino di Microsoft hello in ogni host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0d19b-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="0d19b-133">Andare troppo[passaggio 6: configurare le impostazioni di origine e destinazione hello](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="0d19b-134">Passaggio 7: Configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="0d19b-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="0d19b-135">Mapping delle reti VM di VMM nei percorsi di origine e destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="0d19b-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="0d19b-136">Dopo il failover, le macchine virtuali vengono create nella rete di destinazione hello tale rete VM di mappe toohello origine in cui hello si trova la macchina virtuale Hyper-V di origine.</span><span class="sxs-lookup"><span data-stu-id="0d19b-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="0d19b-137">Andare troppo[passaggio 7: configurare il mapping di rete](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="0d19b-138">Passaggio 8: Configurare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="0d19b-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="0d19b-139">Specificare in che modo le macchine virtuali verranno replicate tra posizioni di VMM.</span><span class="sxs-lookup"><span data-stu-id="0d19b-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="0d19b-140">Andare troppo[passaggio 8: impostare un criterio di replica](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="0d19b-141">Passaggio 9: Abilitare la replica per le VM</span><span class="sxs-lookup"><span data-stu-id="0d19b-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="0d19b-142">Selezionare le macchine virtuali hello desiderato tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="0d19b-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="0d19b-143">Abilitazione di una macchina virtuale per il sito secondario di replica i trigger hello la replica iniziale toohello, seguito dalla replica differenziale in corso.</span><span class="sxs-lookup"><span data-stu-id="0d19b-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="0d19b-144">Andare troppo[passaggio 9: abilitare la replica](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="0d19b-145">Passaggio 10: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="0d19b-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="0d19b-146">Eseguire un toomake di failover di test che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="0d19b-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="0d19b-147">Andare troppo[passaggio 10: eseguire un failover di test](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="0d19b-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
