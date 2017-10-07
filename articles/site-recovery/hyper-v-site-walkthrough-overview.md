---
title: aaaReplicate tooAzure di macchine virtuali Hyper-V con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come replica tooorchestrate, failover e il ripristino di locale Hyper-V VM tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="10a8f-103">La replica Hyper-V le macchine virtuali (senza VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="10a8f-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="10a8f-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="10a8f-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="10a8f-105">Azure classico</span><span class="sxs-lookup"><span data-stu-id="10a8f-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="10a8f-106">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="10a8f-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="10a8f-107">In questo articolo viene fornita una panoramica di hello passaggi necessari tooreplicate locale Hyper-V le macchine virtuali tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="10a8f-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="10a8f-108">In questa distribuzione le macchine virtuali Hyper-V non vengono gestite tramite la soluzione Virtual Machine Manager (VMM) di System Center.</span><span class="sxs-lookup"><span data-stu-id="10a8f-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="10a8f-109">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="10a8f-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="10a8f-110">Passaggio 1: Esaminare l'architettura e i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="10a8f-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="10a8f-111">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di che aver compreso tutti i componenti di hello necessari toodeploy</span><span class="sxs-lookup"><span data-stu-id="10a8f-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="10a8f-112">Andare troppo[passaggio 1: esaminare l'architettura di hello](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="10a8f-113">Passaggio 2: Esaminare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="10a8f-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="10a8f-114">Assicurarsi di avere i prerequisiti di hello sul posto per ogni componente di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="10a8f-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="10a8f-115">**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="10a8f-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="10a8f-116">**Prerequisiti di Hyper-V in locale**: assicurarsi che gli host Hyper-V siano pronti per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="10a8f-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="10a8f-117">**Macchine virtuali replicate**: macchine virtuali che si desidera tooreplicate necessario toocomply ai requisiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="10a8f-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="10a8f-118">Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="10a8f-119">Passaggio 3: Pianificare la capacità</span><span class="sxs-lookup"><span data-stu-id="10a8f-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="10a8f-120">Se si sta eseguendo una distribuzione completa, è necessario toofigure risorse quali la replica è necessario.</span><span class="sxs-lookup"><span data-stu-id="10a8f-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="10a8f-121">Esistono un paio di strumenti disponibili toohelp si esegue questa operazione.</span><span class="sxs-lookup"><span data-stu-id="10a8f-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="10a8f-122">Passare tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="10a8f-122">Go tooStep 2.</span></span> <span data-ttu-id="10a8f-123">Se si sta eseguendo una rapida Configura tootest hello ambiente è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="10a8f-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="10a8f-124">Andare troppo[passaggio 3: pianificare la capacità](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="10a8f-125">Passaggio 4: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="10a8f-125">Step 4: Plan networking</span></span>

<span data-ttu-id="10a8f-126">È necessario toodo alcuni pianificazione tooensure che macchine virtuali di Azure siano connessi toonetworks dopo che si verifica il failover e che dispongano di hello destra indirizzi IP della rete.</span><span class="sxs-lookup"><span data-stu-id="10a8f-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="10a8f-127">Andare troppo[passaggio 4: pianificare la rete](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="10a8f-128">Passaggio 5: Preparare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="10a8f-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="10a8f-129">Configurare le reti e le risorse di archiviazione di Azure prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="10a8f-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="10a8f-130">È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="10a8f-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="10a8f-131">Andare troppo[passaggio 5: preparare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="10a8f-132">Passaggio 6: Preparare Hyper-V</span><span class="sxs-lookup"><span data-stu-id="10a8f-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="10a8f-133">Assicurarsi che i server Hyper-V soddisfino i requisiti di distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="10a8f-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="10a8f-134">Andare troppo[passaggio 6: preparazione Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="10a8f-135">Passaggio 7: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="10a8f-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="10a8f-136">È necessario tooset backup un tooorchestrate insieme di credenziali di servizi di ripristino e gestire la replica.</span><span class="sxs-lookup"><span data-stu-id="10a8f-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="10a8f-137">Quando si imposta l'insieme di credenziali hello, specificare gli elementi da tooreplicate, e in cui si desidera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="10a8f-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="10a8f-138">Andare troppo[passaggio 7: creare un insieme di credenziali](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="10a8f-139">Passaggio 8: Configurare le impostazioni di origine e di destinazione</span><span class="sxs-lookup"><span data-stu-id="10a8f-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="10a8f-140">Consente di impostare hello origine e di destinazione che viene utilizzato per la replica.</span><span class="sxs-lookup"><span data-stu-id="10a8f-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="10a8f-141">Configurare le impostazioni dell'origine include l'aggiunta di host Hyper-V tooa sito di Hyper-V, l'installazione di hello Provider di Site Recovery e l'agente di servizi di ripristino in ogni host Hyper-V e la registrazione del sito hello in hello che insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="10a8f-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="10a8f-142">Andare troppo[passaggio 8: impostare hello origine e di destinazione](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="10a8f-143">Passaggio 9: Configurare i criteri di replica</span><span class="sxs-lookup"><span data-stu-id="10a8f-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="10a8f-144">Impostare le impostazioni di replica toospecify un criterio per le macchine virtuali Hyper-V nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="10a8f-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="10a8f-145">Andare troppo[passaggio 9: configurare un criterio di replica](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="10a8f-146">Passaggio 10: Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="10a8f-146">Step 10: Enable replication</span></span>

<span data-ttu-id="10a8f-147">Dopo aver creato un criterio di replica sul posto, dopo aver abilitato, viene eseguita la replica iniziale di VM hello.</span><span class="sxs-lookup"><span data-stu-id="10a8f-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="10a8f-148">Andare troppo[passaggio 10: abilitare la replica](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="10a8f-149">Passaggio 11: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="10a8f-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="10a8f-150">Dopo il completamento della replica iniziale e la replica differenziale è in esecuzione, è possibile eseguire un toomake di failover di test che tutto funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="10a8f-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="10a8f-151">Andare troppo[passaggio 11: eseguire un failover di test](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="10a8f-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
