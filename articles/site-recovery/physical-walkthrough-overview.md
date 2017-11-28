---
title: aaaReplicate fisico locale tooAzure server con Azure Site Recovery | Documenti Microsoft
description: Viene fornita una panoramica dei passaggi di hello per la replica dei carichi di lavoro in esecuzione in locale Windows/Linux server fisici tooAzure con hello servizio Azure Site Recovery.
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
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="d2067-103">Replicare tooAzure server fisici con il ripristino del sito</span><span class="sxs-lookup"><span data-stu-id="d2067-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="d2067-104">In questo articolo viene fornita una panoramica di hello passaggi necessari tooreplicate locale Windows/Linux server fisici tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2067-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="d2067-105">Passaggio 1: Esaminare l'architettura e i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d2067-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="d2067-106">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di che aver compreso tutti i componenti di hello necessari tooset distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="d2067-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="d2067-107">Andare troppo[passaggio 1: esaminare l'architettura di hello](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="d2067-108">Passaggio 2: Esaminare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d2067-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="d2067-109">Assicurarsi di avere i prerequisiti di hello sul posto per ogni componente di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="d2067-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="d2067-110">**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d2067-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="d2067-111">**Componenti locali di Site Recovery**: è necessario un computer che esegue i componenti locali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d2067-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="d2067-112">**Le macchine replicate**: server da tooreplicate necessario toocomply con requisiti di Azure e locali.</span><span class="sxs-lookup"><span data-stu-id="d2067-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="d2067-113">Andare troppo[passaggio 2: esaminare i prerequisiti e limitazioni](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="d2067-114">Passaggio 3: Pianificare la capacità</span><span class="sxs-lookup"><span data-stu-id="d2067-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="d2067-115">Se si sta eseguendo una distribuzione completa, è necessario toofigure risorse quali la replica è necessario.</span><span class="sxs-lookup"><span data-stu-id="d2067-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="d2067-116">Se si sta eseguendo una rapida Configura tootest hello ambiente, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="d2067-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="d2067-117">Andare troppo[passaggio 3: pianificare la capacità](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="d2067-118">Passaggio 4: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="d2067-118">Step 4: Plan networking</span></span>

<span data-ttu-id="d2067-119">È necessario toodo alcuni pianificazione tooensure che macchine virtuali di Azure siano connessi toonetworks dopo che si verifica il failover e che dispongano di hello destra indirizzi IP della rete.</span><span class="sxs-lookup"><span data-stu-id="d2067-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="d2067-120">Andare troppo[passaggio 4: pianificare la rete](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="d2067-121">Passaggio 5: Preparare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="d2067-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="d2067-122">Configurare le reti e le risorse di archiviazione di Azure prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="d2067-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="d2067-123">Andare troppo[passaggio 5: preparare Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="d2067-124">Passaggio 6: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="d2067-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="d2067-125">Per impostare un tooorchestrate insieme di credenziali di servizi di ripristino e gestire la replica.</span><span class="sxs-lookup"><span data-stu-id="d2067-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="d2067-126">Quando si imposta l'insieme di credenziali hello, specificare gli elementi da tooreplicate, e in cui si desidera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="d2067-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="d2067-127">Andare troppo[passaggio 6: configurare un insieme di credenziali](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="d2067-128">Passaggio 7: Configurare le impostazioni di origine e di destinazione</span><span class="sxs-lookup"><span data-stu-id="d2067-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="d2067-129">Configurare le impostazioni per l'origine hello e di destinazione del sito (Azure).</span><span class="sxs-lookup"><span data-stu-id="d2067-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="d2067-130">Le impostazioni dell'origine include l'esecuzione del programma di installazione unificata tooinstall componenti Site Recovery di hello locali.</span><span class="sxs-lookup"><span data-stu-id="d2067-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="d2067-131">Andare troppo[passaggio 7: configurare hello origine e di destinazione](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="d2067-132">Passaggio 8: Configurare un criterio di replica</span><span class="sxs-lookup"><span data-stu-id="d2067-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="d2067-133">Impostare un criterio toospecify fisico come i server devono essere replicati.</span><span class="sxs-lookup"><span data-stu-id="d2067-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="d2067-134">Andare troppo[passaggio 8: impostare un criterio di replica](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="d2067-135">Passaggio 9: Installare il servizio di mobilità hello</span><span class="sxs-lookup"><span data-stu-id="d2067-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="d2067-136">servizio di mobilità Hello deve essere installato in ogni server desiderate tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="d2067-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="d2067-137">Esistono alcuni modi tooset servizio hello, con l'installazione push o pull.</span><span class="sxs-lookup"><span data-stu-id="d2067-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="d2067-138">Andare troppo[passaggio 9: installare il servizio Mobility hello](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="d2067-139">Passaggio 10: Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="d2067-139">Step 10: Enable replication</span></span>

<span data-ttu-id="d2067-140">Dopo che il servizio di mobilità hello è in esecuzione in un server, è possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="d2067-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="d2067-141">Dopo aver abilitato, viene eseguita la replica iniziale di VM hello.</span><span class="sxs-lookup"><span data-stu-id="d2067-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="d2067-142">Andare troppo[passaggio 10: abilitare la replica](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="d2067-143">Passaggio 11: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="d2067-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="d2067-144">Al termine della replica iniziale e la replica differenziale è in esecuzione, è possibile eseguire un toomake di failover di test che tutto funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="d2067-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="d2067-145">Andare troppo[passaggio 11: eseguire un failover di test](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="d2067-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

