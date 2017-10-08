---
title: cloud di macchine virtuali Hyper-V in VMM aaaReplicate tooAzure con Azure Site Recovery | Documenti Microsoft
description: Viene fornita una panoramica per la replica delle macchine virtuali Hyper-V in VMM cloud tooAzure utilizzando il servizio di Azure Site Recovery hello
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="8b0ea-103">Replicare le macchine virtuali Hyper-V in VMM cloud tooAzure usando Site Recovery nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="8b0ea-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b0ea-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8b0ea-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="8b0ea-105">Azure classico</span><span class="sxs-lookup"><span data-stu-id="8b0ea-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="8b0ea-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8b0ea-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="8b0ea-107">PowerShell - Classica</span><span class="sxs-lookup"><span data-stu-id="8b0ea-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="8b0ea-108">In questo articolo fornisce una panoramica di hello passaggi necessari tooreplicate locale macchine virtuali di Hyper-V (VM) gestite in tooAzure cloud di System Center Virtual Machine Manager (VMM), utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio Hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="8b0ea-109">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8b0ea-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="8b0ea-110">Passaggio 1: Esaminare l'architettura dello scenario hello</span><span class="sxs-lookup"><span data-stu-id="8b0ea-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="8b0ea-111">Prima di avviare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di aver compreso tutti i componenti di hello è necessario toodeploy.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="8b0ea-112">Andare troppo[passaggio 1: esaminare l'architettura di hello](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="8b0ea-113">Passaggio 2: Esaminare i prerequisiti e le limitazioni</span><span class="sxs-lookup"><span data-stu-id="8b0ea-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="8b0ea-114">Assicurarsi di comprendere le limitazioni e prerequisiti di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="8b0ea-115">**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="8b0ea-116">**Server VMM locali e host Hyper-V**: assicurarsi che i server VMM e gli host Hyper-V siano conformi e preparati per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="8b0ea-117">**Macchine virtuali replicate**: verificare che le macchine virtuali desiderate tooreplicate conformi ai requisiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="8b0ea-118">Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="8b0ea-119">Passaggio 3: Pianificare la capacità</span><span class="sxs-lookup"><span data-stu-id="8b0ea-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="8b0ea-120">Se si sta eseguendo una distribuzione completa, è necessario toofigure risorse quali la replica è necessario.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="8b0ea-121">Esistono un paio di strumenti disponibili toohelp si esegue questa operazione.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="8b0ea-122">Se si sta eseguendo una rapida Configura tootest hello ambiente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="8b0ea-123">Andare troppo[passaggio 3: pianificare la capacità](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="8b0ea-124">Passaggio 4: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="8b0ea-124">Step 4: Plan networking</span></span>

<span data-ttu-id="8b0ea-125">È necessario toodo alcuni pianificazione tooensure che è possibile configurare il mapping di rete quando si distribuisce uno scenario di hello, della rete che macchine virtuali di Azure saranno le reti virtuali connesse tooAzure dopo che si verifica il failover e indirizzi che che sono state assegnate IP appropriato.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="8b0ea-126">Andare troppo[passaggio 4: pianificare la rete](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="8b0ea-127">Passaggio 5: Preparare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="8b0ea-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="8b0ea-128">Configurare un account Azure, reti e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="8b0ea-129">È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="8b0ea-130">Andare troppo[passaggio 5: preparare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="8b0ea-131">Passaggio 6: Preparare VMM e Hyper-V</span><span class="sxs-lookup"><span data-stu-id="8b0ea-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="8b0ea-132">Preparare i server VMM locale di hello e host Hyper-V per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="8b0ea-133">Andare troppo[passaggio 6: preparare i server locali](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="8b0ea-134">Passaggio 7: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="8b0ea-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="8b0ea-135">Configurare un insieme di credenziali dei Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="8b0ea-136">insieme di credenziali Hello contiene impostazioni di configurazione e Orchestra la replica.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="8b0ea-137">Passaggio 7: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="8b0ea-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="8b0ea-138">Passaggio 8: Configurare le impostazioni di origine e di destinazione</span><span class="sxs-lookup"><span data-stu-id="8b0ea-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="8b0ea-139">Impostare il percorso di replica di origine e destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="8b0ea-140">Aggiungi insieme di credenziali toohello server VMM hello e scaricare i file di installazione hello per i componenti di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="8b0ea-141">Eseguire l'installazione di Provider di Azure Site Recovery nel server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="8b0ea-142">Il programma di installazione installa hello Provider nel server VMM hello e registra il server hello nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="8b0ea-143">Installare l'agente di servizi di ripristino di Microsoft hello in ogni host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="8b0ea-144">Andare troppo[passaggio 8: configurare le impostazioni di origine e di destinazione](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="8b0ea-145">Passaggio 9: Configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="8b0ea-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="8b0ea-146">Mappa reti virtuali tooAzure di reti VM di VMM in locale.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="8b0ea-147">Dopo il failover, macchine virtuali di Azure vengono create in hello rete di Azure che esegue il mapping di rete VM toohello locale in cui hello Hyper-V di origine si trova.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="8b0ea-148">Andare troppo[passaggio 9: configurare il mapping di rete](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="8b0ea-149">Passaggio 10: Configurare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="8b0ea-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="8b0ea-150">Specificare la modalità di macchine virtuali in locale verranno replicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="8b0ea-151">Andare troppo[passaggio 10: configurare un criterio di replica](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="8b0ea-152">Passaggio 11: Abilitare la replica per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="8b0ea-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="8b0ea-153">Selezionare le macchine virtuali hello desiderato tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="8b0ea-154">Abilitazione di una macchina virtuale per tooAzure la replica iniziale hello trigger di replica, seguito dalla replica differenziale in corso.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="8b0ea-155">Andare troppo[passaggio 11: abilitare la replica](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="8b0ea-156">Passaggio 12: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="8b0ea-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="8b0ea-157">Eseguire un toomake di failover di test che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="8b0ea-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="8b0ea-158">Andare troppo[passaggio 12: eseguire un failover di test](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="8b0ea-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


