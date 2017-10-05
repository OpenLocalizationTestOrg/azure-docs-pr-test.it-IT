---
title: Eseguire la replica di VM Hyper-V in Azure con Azure Site Recovery | Microsoft Docs
description: Questo articolo descrive come orchestrare la replica, il failover e il ripristino di macchine virtuali locali Hyper-V in Azure.
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
ms.openlocfilehash: da10b213bc2543942b5ac77cf5c5d8547c00220c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure"></a><span data-ttu-id="0c604-103">Eseguire la replica di macchine virtuali Hyper-V (senza VMM) in Azure</span><span class="sxs-lookup"><span data-stu-id="0c604-103">Replicate Hyper-V virtual machines (without VMM) to Azure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c604-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0c604-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="0c604-105">Azure classico</span><span class="sxs-lookup"><span data-stu-id="0c604-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="0c604-106">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="0c604-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="0c604-107">Questo articolo fornisce una panoramica dei passaggi necessari per eseguire la replica di macchine virtuali Hyper-V locali in Azure usando [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c604-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="0c604-108">In questa distribuzione le macchine virtuali Hyper-V non vengono gestite tramite la soluzione Virtual Machine Manager (VMM) di System Center.</span><span class="sxs-lookup"><span data-stu-id="0c604-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="0c604-109">Dopo la lettura di questo articolo, è possibile inserire commenti nella parte inferiore oppure porre domande tecniche nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0c604-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="0c604-110">Passaggio 1: Esaminare l'architettura e i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0c604-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="0c604-111">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario e assicurarsi di comprendere quali componenti è necessario distribuire</span><span class="sxs-lookup"><span data-stu-id="0c604-111">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="0c604-112">Andare a [Passaggio 1: Esaminare l'architettura](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-112">Go to [Step 1: Review the architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="0c604-113">Passaggio 2: Esaminare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0c604-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="0c604-114">Assicurarsi che siano rispettati i prerequisiti per ogni componente della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="0c604-114">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="0c604-115">**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0c604-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="0c604-116">**Prerequisiti di Hyper-V in locale**: assicurarsi che gli host Hyper-V siano pronti per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0c604-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="0c604-117">**VM replicate**: le VM da replicare devono essere conformi ai requisiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c604-117">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements.</span></span>

<span data-ttu-id="0c604-118">Andare a [Passaggio 2: Esaminare i prerequisiti e le limitazioni](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-118">Go to [Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="0c604-119">Passaggio 3: Pianificare la capacità</span><span class="sxs-lookup"><span data-stu-id="0c604-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="0c604-120">Se si sta eseguendo una distribuzione completa, è necessario individuare le risorse di replica richieste.</span><span class="sxs-lookup"><span data-stu-id="0c604-120">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="0c604-121">A tale scopo, sono disponibili due strumenti.</span><span class="sxs-lookup"><span data-stu-id="0c604-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="0c604-122">Andare al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="0c604-122">Go to Step 2.</span></span> <span data-ttu-id="0c604-123">Se si sta eseguendo una configurazione rapida per testare l'ambiente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="0c604-123">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="0c604-124">Andare a [Passaggio 3: Pianificare la capacità](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-124">Go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="0c604-125">Passaggio 4: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="0c604-125">Step 4: Plan networking</span></span>

<span data-ttu-id="0c604-126">È necessario eseguire alcune attività di pianificazione per garantire che le VM di Azure siano connesse alle reti dopo il failover e che abbiano gli indirizzi IP appropriati.</span><span class="sxs-lookup"><span data-stu-id="0c604-126">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="0c604-127">Andare a [Passaggio 4: Pianificare la rete](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-127">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="0c604-128">Passaggio 5: Preparare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="0c604-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="0c604-129">Configurare le reti e le risorse di archiviazione di Azure prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="0c604-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="0c604-130">È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="0c604-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="0c604-131">Andare a [Passaggio 5: Preparare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-131">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="0c604-132">Passaggio 6: Preparare Hyper-V</span><span class="sxs-lookup"><span data-stu-id="0c604-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="0c604-133">Assicurarsi che i server Hyper-V soddisfino i requisiti di distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0c604-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="0c604-134">Andare a [Passaggio 6: Preparare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-134">Go to [Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="0c604-135">Passaggio 7: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="0c604-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="0c604-136">È necessario configurare un insieme di credenziali di Servizi di ripristino per orchestrare e gestire la replica.</span><span class="sxs-lookup"><span data-stu-id="0c604-136">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="0c604-137">Quando si configura l'insieme di credenziali, specificare gli elementi da replicare e la posizione in cui eseguire la replica.</span><span class="sxs-lookup"><span data-stu-id="0c604-137">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="0c604-138">Andare a [Passaggio 7: Creare un insieme di credenziali](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-138">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="0c604-139">Passaggio 8: Configurare le impostazioni di origine e di destinazione</span><span class="sxs-lookup"><span data-stu-id="0c604-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="0c604-140">Configurare l'origine e la destinazione usate per la replica.</span><span class="sxs-lookup"><span data-stu-id="0c604-140">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="0c604-141">La configurazione delle impostazioni di origine comprende l'aggiunta di host Hyper-V a un sito Hyper-V, l'installazione del provider di Site Recovery e dell'agente di Servizi di ripristino in ogni host Hyper-V e la registrazione del sito nell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0c604-141">Setting up source settings includes adding Hyper-V hosts to a Hyper-V site, installing the Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering the site in the Recovery Services vault.</span></span>

<span data-ttu-id="0c604-142">Andare a [Passaggio 8: Configurare l'origine e la destinazione](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-142">Go to [Step 8: Set up the source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="0c604-143">Passaggio 9: Configurare i criteri di replica</span><span class="sxs-lookup"><span data-stu-id="0c604-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="0c604-144">I criteri di replica vengono configurati per specificare le impostazioni di replica per le VM Hyper-V nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="0c604-144">You set up a policy to specify replication settings for Hyper-V VMs in the vault.</span></span>

<span data-ttu-id="0c604-145">Andare a [Passaggio 9: Configurare i criteri di replica](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-145">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="0c604-146">Passaggio 10: Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="0c604-146">Step 10: Enable replication</span></span>

<span data-ttu-id="0c604-147">Una volta creati i criteri di replica, dopo l'abilitazione viene eseguita la replica iniziale delle VM.</span><span class="sxs-lookup"><span data-stu-id="0c604-147">After you have a replication policy in place,  After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="0c604-148">Andare a [Passaggio 10: Abilitare la replica](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-148">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="0c604-149">Passaggio 11: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="0c604-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="0c604-150">Dopo il completamento della replica iniziale e con la replica differenziale in esecuzione, è possibile eseguire un failover di test per verificare che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="0c604-150">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="0c604-151">Andare a [Passaggio 11: Eseguire un failover di test](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="0c604-151">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
