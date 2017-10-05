---
title: Eseguire la replica di macchine virtuali Hyper-V in un sito VMM secondario con Azure Site Recovery | Microsoft Docs
description: Fornisce una panoramica della replica di VM Hyper-V in un sito VMM secondario tramite il portale di Azure.
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
ms.openlocfilehash: b422dd2cf23426de2f154a553b38509082536309
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a><span data-ttu-id="e62d8-103">Eseguire la replica di macchine virtuali Hyper-V in cloud VMM in un sito VMM secondario</span><span class="sxs-lookup"><span data-stu-id="e62d8-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e62d8-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e62d8-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="e62d8-105">Portale classico</span><span class="sxs-lookup"><span data-stu-id="e62d8-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="e62d8-106">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="e62d8-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="e62d8-107">Questo articolo fornisce una panoramica della procedura necessaria per la replica di macchine virtuali Hyper-V locali gestite in cloud System Center Virtual Machine Manager (VMM) in un sito VMM secondario tramite [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e62d8-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span>

<span data-ttu-id="e62d8-108">È possibile inviare commenti nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e62d8-108">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="e62d8-109">Passaggio 1: Esaminare l'architettura dello scenario</span><span class="sxs-lookup"><span data-stu-id="e62d8-109">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="e62d8-110">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario e assicurarsi di comprendere quali componenti è necessario distribuire.</span><span class="sxs-lookup"><span data-stu-id="e62d8-110">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="e62d8-111">Andare al [Passaggio 1: Esaminare l'architettura](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-111">Go to [Step 1: Review the architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="e62d8-112">Passaggio 2: Esaminare i prerequisiti e le limitazioni</span><span class="sxs-lookup"><span data-stu-id="e62d8-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="e62d8-113">Assicurarsi di comprendere i prerequisiti e le limitazioni della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e62d8-113">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="e62d8-114">**Prerequisiti di Azure**: per orchestrare e gestire la replica sono necessari una sottoscrizione di Microsoft Azure e un insieme di credenziali di Servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="e62d8-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, to orchestrate and manage replication.</span></span>
<span data-ttu-id="e62d8-115">**Server VMM locali e host Hyper-V**: assicurarsi che i server VMM e gli host Hyper-V siano conformi e preparati per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e62d8-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="e62d8-116">Andare al [Passaggio 2: Esaminare i prerequisiti e le limitazioni](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-116">Go to [Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="e62d8-117">Passaggio 3: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="e62d8-117">Step 3: Plan networking</span></span>

<span data-ttu-id="e62d8-118">È necessario pianificare le risorse di rete, in modo da assicurare che sia possibile configurare il mapping di rete tra reti di macchine virtuali VMM durante la distribuzione dello scenario.</span><span class="sxs-lookup"><span data-stu-id="e62d8-118">You need to do some network planning to ensure that you can configure network mapping between VMM VM networks when you deploy the scenario.</span></span>

<span data-ttu-id="e62d8-119">Andare al [Passaggio 3: Pianificare la rete](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-119">Go to [Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="e62d8-120">Passaggio 4: Preparare VMM e Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e62d8-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="e62d8-121">Preparare i server VMM e gli host Hyper-V per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e62d8-121">Prepare the VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="e62d8-122">Andare al [Passaggio 4: Preparare VMM e Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-122">Go to [Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="e62d8-123">Passaggio 5: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="e62d8-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="e62d8-124">Configurare un insieme di credenziali dei Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e62d8-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="e62d8-125">L'insieme di credenziali contiene le impostazioni di configurazione e orchestra la replica.</span><span class="sxs-lookup"><span data-stu-id="e62d8-125">The vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="e62d8-126">[Passaggio 5: Configurare un insieme di credenziali](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="e62d8-127">Passaggio 6: Configurare le impostazioni di origine e destinazione</span><span class="sxs-lookup"><span data-stu-id="e62d8-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="e62d8-128">Configurare le posizioni VMM di replica di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e62d8-128">Set up the source and target replication VMM locations.</span></span> <span data-ttu-id="e62d8-129">Aggiungere i server VMM all'insieme di credenziali e scaricare i file di installazione per i componenti di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e62d8-129">Add the VMM servers to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="e62d8-130">Eseguire il programma di installazione del provider di Azure Site Recovery nel server VMM.</span><span class="sxs-lookup"><span data-stu-id="e62d8-130">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="e62d8-131">Il provider viene installato nel server VMM e il server viene registrato nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="e62d8-131">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="e62d8-132">Installare l'agente di Servizi di ripristino di Azure in ogni host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="e62d8-132">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="e62d8-133">Andare al [Passaggio 6: Configurare le impostazioni di origine e destinazione](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-133">Go to [Step 6: Set up the source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="e62d8-134">Passaggio 7: Configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="e62d8-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="e62d8-135">Mappare le reti di macchine virtuali VMM nelle posizioni di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e62d8-135">Map VMM VM networks in the source and target locations.</span></span> <span data-ttu-id="e62d8-136">Dopo il failover, le VM vengono create nella rete di destinazione mappata alla rete di VM di origine in cui si trova la macchina virtuale Hyper-V di origine.</span><span class="sxs-lookup"><span data-stu-id="e62d8-136">After failover, VMs are created in the target network that maps to the source VM network in which the source Hyper-V VM is located.</span></span>

<span data-ttu-id="e62d8-137">Andare al [Passaggio 7: Configurare il mapping di rete](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-137">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="e62d8-138">Passaggio 8: Configurare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="e62d8-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="e62d8-139">Specificare in che modo le macchine virtuali verranno replicate tra posizioni di VMM.</span><span class="sxs-lookup"><span data-stu-id="e62d8-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="e62d8-140">Andare al [Passaggio 8: Configurare un criterio di replica](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-140">Go to [Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="e62d8-141">Passaggio 9: Abilitare la replica per le VM</span><span class="sxs-lookup"><span data-stu-id="e62d8-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="e62d8-142">Selezionare le VM da replicare.</span><span class="sxs-lookup"><span data-stu-id="e62d8-142">Select the VMs you want to replicate.</span></span> <span data-ttu-id="e62d8-143">L'abilitazione di una VM per la replica attiva la replica iniziale nel sito secondario, seguita dalla replica differenziale in corso.</span><span class="sxs-lookup"><span data-stu-id="e62d8-143">Enabling a VM for replication triggers the initial replication to the secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="e62d8-144">Andare al [Passaggio 9: Abilitare la replica](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-144">Go to [Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="e62d8-145">Passaggio 10: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="e62d8-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="e62d8-146">Eseguire un failover di test per verificare che tutti gli elementi funzionino come previsto.</span><span class="sxs-lookup"><span data-stu-id="e62d8-146">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="e62d8-147">Andare al [Passaggio 10: Eseguire un failover di test](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="e62d8-147">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
