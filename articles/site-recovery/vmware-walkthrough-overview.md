---
title: Eseguire la replica di VM VMware in Azure con Azure Site Recovery | Microsoft Docs
description: Viene fornita una panoramica dei passaggi per la replica in Azure di carichi di lavoro in esecuzione in VM VMware
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: db6f5f95929503e82a529dba26b56af1edb0767f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-vms-to-azure-with-site-recovery"></a><span data-ttu-id="cdbe5-103">Replicare VM VMware in Azure con Site Recovery</span><span class="sxs-lookup"><span data-stu-id="cdbe5-103">Replicate VMware VMs to Azure with Site Recovery</span></span>

<span data-ttu-id="cdbe5-104">Questo articolo fornisce una panoramica dei passaggi necessari per eseguire la replica di macchine virtuali VMware locali in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-104">This article provides an overview of the steps required to replicate on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


![Processo di distribuzione](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="cdbe5-106">**Figura 1: Riepilogo del processo di distribuzione**</span><span class="sxs-lookup"><span data-stu-id="cdbe5-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="cdbe5-107">Passaggio 1: Esaminare l'architettura e i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cdbe5-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="cdbe5-108">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario e assicurarsi di comprendere quali componenti è necessario distribuire</span><span class="sxs-lookup"><span data-stu-id="cdbe5-108">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="cdbe5-109">Andare a [Passaggio 1: Esaminare l'architettura](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-109">Go to [Step 1: Review the architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="cdbe5-110">Passaggio 2: Esaminare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cdbe5-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="cdbe5-111">Assicurarsi che siano rispettati i prerequisiti per ogni componente della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="cdbe5-111">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="cdbe5-112">**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="cdbe5-113">**Componenti locali di Site Recovery**: è necessario un computer che esegue i componenti locali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="cdbe5-114">**Prerequisiti di VMware locale**: è necessario configurare gli account in modo che Site Recovery possa accedere ai server VMware e alle VM.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-114">**On-premises VMware prerequisites**: You need to set up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="cdbe5-115">**VM replicate**: le VM da replicare devono essere conformi ai requisiti di Azure e avere il componente servizio Mobility installato.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-115">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements, and have the Mobility service component installed.</span></span>

<span data-ttu-id="cdbe5-116">Andare a [Passaggio 2: Esaminare i prerequisiti e le limitazioni](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-116">Go to [Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="cdbe5-117">Passaggio 3: Pianificare la capacità</span><span class="sxs-lookup"><span data-stu-id="cdbe5-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="cdbe5-118">Se si sta eseguendo una distribuzione completa, è necessario individuare le risorse di replica richieste.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-118">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="cdbe5-119">A tale scopo, sono disponibili due strumenti.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-119">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="cdbe5-120">Andare al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-120">Go to Step 2.</span></span> <span data-ttu-id="cdbe5-121">Se si sta eseguendo una configurazione rapida per testare l'ambiente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-121">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="cdbe5-122">Andare a [Passaggio 3: Pianificare la capacità](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-122">Go to [Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="cdbe5-123">Passaggio 4: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="cdbe5-123">Step 4: Plan networking</span></span>

<span data-ttu-id="cdbe5-124">È necessario eseguire alcune attività di pianificazione per garantire che le VM di Azure siano connesse alle reti dopo il failover e che abbiano gli indirizzi IP appropriati.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-124">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="cdbe5-125">Andare a [Passaggio 4: Pianificare la rete](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-125">Go to [Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="cdbe5-126">Passaggio 5: Preparare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="cdbe5-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="cdbe5-127">Configurare le reti e le risorse di archiviazione di Azure prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="cdbe5-128">È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="cdbe5-129">Andare a [Passaggio 5: Preparare Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-129">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="cdbe5-130">Passaggio 6: Preparare VMware</span><span class="sxs-lookup"><span data-stu-id="cdbe5-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="cdbe5-131">È necessario configurare gli account che verranno usati da Site Recovery per:</span><span class="sxs-lookup"><span data-stu-id="cdbe5-131">You need to set up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="cdbe5-132">Accedere ai server di virtualizzazione VMware per rilevare automaticamente le VM.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-132">Access VMware virtualization servers to automatically detect VMs.</span></span>
- <span data-ttu-id="cdbe5-133">Accedere alle VM per installare il servizio Mobility.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-133">Access VMs to install the Mobility service.</span></span> <span data-ttu-id="cdbe5-134">Ogni VM che si vuole replicare deve avere l'agente del servizio Mobility installato affinché sia possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-134">Each VM you want to replicate must have the Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="cdbe5-135">Andare a [Passaggio 6: Preparare VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-135">Go to [Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="cdbe5-136">Passaggio 7: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="cdbe5-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="cdbe5-137">È necessario configurare un insieme di credenziali di Servizi di ripristino per orchestrare e gestire la replica.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-137">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="cdbe5-138">Quando si configura l'insieme di credenziali, specificare gli elementi da replicare e la posizione in cui eseguire la replica.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-138">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="cdbe5-139">Andare a [Passaggio 7: Configurare un insieme di credenziali](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-139">Go to [Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="cdbe5-140">Passaggio 8: Configurare le impostazioni di origine e di destinazione</span><span class="sxs-lookup"><span data-stu-id="cdbe5-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="cdbe5-141">Configurare l'origine e la destinazione usate per la replica.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-141">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="cdbe5-142">La configurazione delle impostazioni di origine include l'esecuzione dell'installazione unificata per installare i componenti di Site Recovery locali.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-142">Setting up source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="cdbe5-143">Andare a [Passaggio 8: Configurare l'origine e la destinazione](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-143">Go to [Step 8: Set up the source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="cdbe5-144">Passaggio 9: Configurare i criteri di replica</span><span class="sxs-lookup"><span data-stu-id="cdbe5-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="cdbe5-145">I criteri di replica vengono configurati per specificare le impostazioni di replica per le VM VMware nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-145">You set up a policy to specify replication settings for VMware VMs in the vault.</span></span>

<span data-ttu-id="cdbe5-146">Andare a [Passaggio 9: Configurare i criteri di replica](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-146">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="cdbe5-147">Passaggio 10: Installare il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="cdbe5-147">Step 10: Install the Mobility service</span></span>

<span data-ttu-id="cdbe5-148">Il servizio Mobility deve essere installato in ogni VM da replicare.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-148">The Mobility service must be installed on each VM you want to replicate.</span></span> <span data-ttu-id="cdbe5-149">È possibile configurare il servizio con l'installazione push o pull.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-149">There are a few ways to set up the service with push or pull installation.</span></span>

<span data-ttu-id="cdbe5-150">Andare a [Passaggio 10: Installare il servizio Mobility](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-150">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="cdbe5-151">Passaggio 11: Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="cdbe5-151">Step 11: Enable replication</span></span>

<span data-ttu-id="cdbe5-152">Quando il servizio Mobility è in esecuzione in una VM, è possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-152">After the Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="cdbe5-153">Dopo l'abilitazione, viene eseguita la replica iniziale delle VM.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-153">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="cdbe5-154">Andare a [Passaggio 11: Abilitare la replica](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-154">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="cdbe5-155">Passaggio 12: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="cdbe5-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="cdbe5-156">Dopo il completamento della replica iniziale e con la replica differenziale in esecuzione, è possibile eseguire un failover di test per verificare che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="cdbe5-156">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="cdbe5-157">Andare a [Passaggio 12: Eseguire un failover di test](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="cdbe5-157">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
