---
title: Eseguire la replica delle macchine virtuali Hyper-V nei cloud VMM in Azure con Azure Site Recovery | Microsoft Docs
description: Viene fornita una panoramica su come replicare le macchine virtuali Hyper-V nei cloud VMM in Azure tramite il servizio Azure Site Recovery
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
ms.openlocfilehash: af68d21184c137b2b0f1bb4c1afb9bf507e8332d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a><span data-ttu-id="3afaa-103">Eseguire la replica di macchine virtuali Hyper-V nei cloud VMM in Azure tramite Site Recovery nel Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3afaa-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3afaa-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3afaa-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="3afaa-105">Azure classico</span><span class="sxs-lookup"><span data-stu-id="3afaa-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="3afaa-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3afaa-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="3afaa-107">PowerShell - Classica</span><span class="sxs-lookup"><span data-stu-id="3afaa-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="3afaa-108">Questo articolo fornisce una panoramica della procedura necessaria per la replica di macchine virtuali Hyper-V locali gestite in cloud System Center Virtual Machine Manager (VMM) in Azure tramite il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3afaa-108">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="3afaa-109">È possibile inviare commenti nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3afaa-109">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="3afaa-110">Passaggio 1: Esaminare l'architettura dello scenario</span><span class="sxs-lookup"><span data-stu-id="3afaa-110">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="3afaa-111">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario e assicurarsi di comprendere quali componenti è necessario distribuire.</span><span class="sxs-lookup"><span data-stu-id="3afaa-111">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="3afaa-112">Andare a [Passaggio 1: Esaminare l'architettura](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-112">Go to [Step 1: Review the architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="3afaa-113">Passaggio 2: Esaminare i prerequisiti e le limitazioni</span><span class="sxs-lookup"><span data-stu-id="3afaa-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="3afaa-114">Assicurarsi di comprendere i prerequisiti e le limitazioni della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3afaa-114">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="3afaa-115">**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3afaa-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="3afaa-116">**Server VMM locali e host Hyper-V**: assicurarsi che i server VMM e gli host Hyper-V siano conformi e preparati per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3afaa-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="3afaa-117">**Macchine virtuali replicate**: assicurarsi che la macchine virtuali da replicare siano conformi ai requisiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="3afaa-117">**Replicated VMs**: Check that VMs you want to replicate comply with Azure requirements.</span></span>

<span data-ttu-id="3afaa-118">Andare a [Passaggio 2: Esaminare i prerequisiti e le limitazioni](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-118">Go to [Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="3afaa-119">Passaggio 3: Pianificare la capacità</span><span class="sxs-lookup"><span data-stu-id="3afaa-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="3afaa-120">Se si sta eseguendo una distribuzione completa, è necessario individuare le risorse di replica richieste.</span><span class="sxs-lookup"><span data-stu-id="3afaa-120">If you're doing a full deployment, you need to figure out what replication resources you need.</span></span> <span data-ttu-id="3afaa-121">A tale scopo, sono disponibili due strumenti.</span><span class="sxs-lookup"><span data-stu-id="3afaa-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="3afaa-122">Se si sta eseguendo una configurazione rapida per testare l'ambiente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="3afaa-122">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="3afaa-123">Andare a [Passaggio 3: Pianificare la capacità](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-123">Go to [Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="3afaa-124">Passaggio 4: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="3afaa-124">Step 4: Plan networking</span></span>

<span data-ttu-id="3afaa-125">È necessario eseguire una pianificazione della rete per garantire la configurazione del mapping di rete quando si distribuisce lo scenario, la connessione delle macchine virtuali di Azure alle reti virtuali di Azure dopo il failover e la relativa assegnazione di indirizzi IP idonei.</span><span class="sxs-lookup"><span data-stu-id="3afaa-125">You need to do some network planning to ensure that you can configure network mapping when you deploy the scenario, that Azure VMs will be connected to Azure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="3afaa-126">Andare a [Passaggio 4: Pianificare la rete](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-126">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="3afaa-127">Passaggio 5: Preparare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="3afaa-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="3afaa-128">Configurare un account Azure, reti e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3afaa-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="3afaa-129">È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="3afaa-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="3afaa-130">Andare al [Passaggio 5: Preparare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-130">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="3afaa-131">Passaggio 6: Preparare VMM e Hyper-V</span><span class="sxs-lookup"><span data-stu-id="3afaa-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="3afaa-132">Preparare i server VMM locali e gli host Hyper-V per la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3afaa-132">Prepare the on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="3afaa-133">Andare al [Passaggio 6: Preparare server locali](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-133">Go to [Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="3afaa-134">Passaggio 7: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="3afaa-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="3afaa-135">Configurare un insieme di credenziali dei Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3afaa-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="3afaa-136">L'insieme di credenziali contiene le impostazioni di configurazione e orchestra la replica.</span><span class="sxs-lookup"><span data-stu-id="3afaa-136">The vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="3afaa-137">Passaggio 7: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="3afaa-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="3afaa-138">Passaggio 8: Configurare le impostazioni di origine e di destinazione</span><span class="sxs-lookup"><span data-stu-id="3afaa-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="3afaa-139">Configurare le località di replica di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3afaa-139">Set up the source and target replication locations.</span></span> <span data-ttu-id="3afaa-140">Aggiungere i server VMM all'insieme di credenziali e scaricare i file di installazione per i componenti di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3afaa-140">Add the VMM server to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="3afaa-141">Eseguire il programma di installazione del provider di Azure Site Recovery nel server VMM.</span><span class="sxs-lookup"><span data-stu-id="3afaa-141">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="3afaa-142">Il provider viene installato nel server VMM e il server viene registrato nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3afaa-142">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="3afaa-143">Installare l'agente di Servizi di ripristino di Azure in ogni host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="3afaa-143">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="3afaa-144">Andare al [Passaggio 8: Configurare le impostazioni di origine e di destinazione](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-144">Go to [Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="3afaa-145">Passaggio 9: Configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="3afaa-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="3afaa-146">Mappare le reti della macchina virtuale VMM locali a reti virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="3afaa-146">Map on-premises VMM VM networks to Azure virtual networks.</span></span> <span data-ttu-id="3afaa-147">Dopo il failover, le macchine virtuali di Azure vengono create nella rete di Azure mappata alla rete della macchina virtuale locale in cui si trova Hyper-V di origine.</span><span class="sxs-lookup"><span data-stu-id="3afaa-147">After failover, Azure VMs are created in the Azure network that maps to the on-premises VM network in which the source Hyper-V is located.</span></span>

<span data-ttu-id="3afaa-148">Andare al [Passaggio 9: Configurare il mapping di rete](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-148">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="3afaa-149">Passaggio 10: Configurare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="3afaa-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="3afaa-150">Specificare come verranno replicate le macchine virtuali locali in Azure.</span><span class="sxs-lookup"><span data-stu-id="3afaa-150">Specify how on-premises VMs will be replicated to Azure.</span></span>

<span data-ttu-id="3afaa-151">Andare al [Passaggio 10: Configurare un criterio di replica](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-151">Go to [Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="3afaa-152">Passaggio 11: Abilitare la replica per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="3afaa-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="3afaa-153">Selezionare le macchine virtuali da replicare.</span><span class="sxs-lookup"><span data-stu-id="3afaa-153">Select the VMs you want to replicate.</span></span> <span data-ttu-id="3afaa-154">L'abilitazione di una macchina virtuale per la replica attiva la replica iniziale in Azure, seguita dalla replica differenziale in corso.</span><span class="sxs-lookup"><span data-stu-id="3afaa-154">ENabling a VM for replication triggers the initial replication to Azure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="3afaa-155">Andare a [Passaggio 11: Abilitare la replica](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-155">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="3afaa-156">Passaggio 12: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="3afaa-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="3afaa-157">Eseguire un failover di test per verificare che tutti gli elementi funzionino come previsto.</span><span class="sxs-lookup"><span data-stu-id="3afaa-157">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="3afaa-158">Andare a [Passaggio 12: Eseguire un failover di test](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="3afaa-158">Go to [Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


