---
title: Eseguire la replica di server fisici locali in Azure con Azure Site Recovery | Microsoft Docs
description: Offre una panoramica della procedura di replica in Azure dei carichi di lavoro in esecuzione in server fisici Windows/Linux locali con il servizio Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 0a09b35e98dc0b2f5283c2a707a3a2b8ac9a39f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-physical-servers-to-azure-with-site-recovery"></a><span data-ttu-id="6fd88-103">Replicare server fisici in Azure con Site Recovery</span><span class="sxs-lookup"><span data-stu-id="6fd88-103">Replicate physical servers to Azure with Site Recovery</span></span>

<span data-ttu-id="6fd88-104">Questo articolo fornisce una panoramica dei passaggi necessari per eseguire la replica di server fisici Windows/Linux locali in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd88-104">This article provides an overview of the steps required to replicate on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="6fd88-105">Passaggio 1: Esaminare l'architettura e i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6fd88-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="6fd88-106">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario e assicurarsi di comprendere quali componenti sono necessari per configurare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6fd88-106">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to set up the deployment.</span></span>

<span data-ttu-id="6fd88-107">Andare a [Passaggio 1: Esaminare l'architettura](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-107">Go to [Step 1: Review the architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="6fd88-108">Passaggio 2: Esaminare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6fd88-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="6fd88-109">Assicurarsi che siano rispettati i prerequisiti per ogni componente della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="6fd88-109">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="6fd88-110">**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6fd88-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="6fd88-111">**Componenti locali di Site Recovery**: è necessario un computer che esegue i componenti locali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6fd88-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="6fd88-112">**Computer replicati**: i server di cui si vuole eseguire la replica devono essere conformi ai requisiti locali e di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd88-112">**Replicated machines**: Servers you want to replicate need to comply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="6fd88-113">Andare a [Passaggio 2: Esaminare i prerequisiti e le limitazioni](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-113">Go to [Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="6fd88-114">Passaggio 3: Pianificare la capacità</span><span class="sxs-lookup"><span data-stu-id="6fd88-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="6fd88-115">Se si sta eseguendo una distribuzione completa, è necessario individuare le risorse di replica richieste.</span><span class="sxs-lookup"><span data-stu-id="6fd88-115">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="6fd88-116">Se si sta eseguendo una configurazione rapida per testare l'ambiente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="6fd88-116">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="6fd88-117">Andare a [Passaggio 3: Pianificare la capacità](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-117">Go to [Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="6fd88-118">Passaggio 4: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="6fd88-118">Step 4: Plan networking</span></span>

<span data-ttu-id="6fd88-119">È necessario eseguire alcune attività di pianificazione per garantire che le VM di Azure siano connesse alle reti dopo il failover e che abbiano gli indirizzi IP appropriati.</span><span class="sxs-lookup"><span data-stu-id="6fd88-119">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="6fd88-120">Andare a [Passaggio 4: Pianificare la rete](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-120">Go to [Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="6fd88-121">Passaggio 5: Preparare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="6fd88-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="6fd88-122">Configurare le reti e le risorse di archiviazione di Azure prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="6fd88-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="6fd88-123">Andare a [Passaggio 5: Preparare Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-123">Go to [Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="6fd88-124">Passaggio 6: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="6fd88-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="6fd88-125">Si configura un insieme di credenziali di Servizi di ripristino per orchestrare e gestire la replica.</span><span class="sxs-lookup"><span data-stu-id="6fd88-125">You set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="6fd88-126">Quando si configura l'insieme di credenziali, specificare gli elementi da replicare e la posizione in cui eseguire la replica.</span><span class="sxs-lookup"><span data-stu-id="6fd88-126">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="6fd88-127">Andare a [Passaggio 6: Configurare un insieme di credenziali](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-127">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="6fd88-128">Passaggio 7: Configurare le impostazioni di origine e di destinazione</span><span class="sxs-lookup"><span data-stu-id="6fd88-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="6fd88-129">Configurare le impostazioni per il sito di origine e di destinazione (Azure).</span><span class="sxs-lookup"><span data-stu-id="6fd88-129">Configure settings for the source and target (Azure) site.</span></span> <span data-ttu-id="6fd88-130">Le impostazioni di origine includono l'esecuzione dell'installazione unificata per installare i componenti di Site Recovery locali.</span><span class="sxs-lookup"><span data-stu-id="6fd88-130">Source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="6fd88-131">Andare a [Passaggio 7: Configurare l'origine e la destinazione](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-131">Go to [Step 7: Set up the source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="6fd88-132">Passaggio 8: Configurare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="6fd88-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="6fd88-133">Si configura un criterio per specificare come replicare i server fisici.</span><span class="sxs-lookup"><span data-stu-id="6fd88-133">You set up a policy to specify how physical servers should replicate.</span></span>

<span data-ttu-id="6fd88-134">Andare a [Passaggio 8: Configurare i criteri di replica](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="6fd88-135">Passaggio 9: Installare il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="6fd88-135">Step 9: Install the Mobility service</span></span>

<span data-ttu-id="6fd88-136">Il servizio Mobility deve essere installato in ogni server da replicare.</span><span class="sxs-lookup"><span data-stu-id="6fd88-136">The Mobility service must be installed on each server you want to replicate.</span></span> <span data-ttu-id="6fd88-137">È possibile configurare il servizio con l'installazione push o pull.</span><span class="sxs-lookup"><span data-stu-id="6fd88-137">There are a few ways to set up the service, with push or pull installation.</span></span>

<span data-ttu-id="6fd88-138">Andare a [Passaggio 9: Installare il servizio Mobility](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-138">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="6fd88-139">Passaggio 10: Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="6fd88-139">Step 10: Enable replication</span></span>

<span data-ttu-id="6fd88-140">Quando il servizio Mobility è in esecuzione in un server, è possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="6fd88-140">After the Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="6fd88-141">Dopo l'abilitazione, viene eseguita la replica iniziale delle VM.</span><span class="sxs-lookup"><span data-stu-id="6fd88-141">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="6fd88-142">Andare a [Passaggio 10: Abilitare la replica](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-142">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="6fd88-143">Passaggio 11: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="6fd88-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="6fd88-144">Dopo il completamento della replica iniziale e con la replica differenziale in esecuzione, è possibile eseguire un failover di test per verificare che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="6fd88-144">After initial replication finishes and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="6fd88-145">Andare a [Passaggio 11: Eseguire un failover di test](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="6fd88-145">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

