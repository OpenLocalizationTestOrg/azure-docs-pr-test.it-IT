---
title: aaaReplicate tooAzure di macchine virtuali VMware con Azure Site Recovery | Documenti Microsoft
description: Viene fornita una panoramica dei passaggi di hello per la replica dei carichi di lavoro in esecuzione in macchine virtuali VMware tooAzure
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
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="68917-103">Replicare le macchine virtuali VMware tooAzure con il ripristino del sito</span><span class="sxs-lookup"><span data-stu-id="68917-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="68917-104">In questo articolo viene fornita una panoramica di hello passaggi necessari tooreplicate locale VMware le macchine virtuali tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="68917-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![Processo di distribuzione](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="68917-106">**Figura 1: Riepilogo del processo di distribuzione**</span><span class="sxs-lookup"><span data-stu-id="68917-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="68917-107">Passaggio 1: Esaminare l'architettura e i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="68917-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="68917-108">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di che aver compreso tutti i componenti di hello necessari toodeploy</span><span class="sxs-lookup"><span data-stu-id="68917-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="68917-109">Andare troppo[passaggio 1: esaminare l'architettura di hello](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="68917-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="68917-110">Passaggio 2: Esaminare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="68917-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="68917-111">Assicurarsi di avere i prerequisiti di hello sul posto per ogni componente di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="68917-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="68917-112">**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="68917-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="68917-113">**Componenti locali di Site Recovery**: è necessario un computer che esegue i componenti locali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="68917-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="68917-114">**Prerequisiti di VMware locale**: È necessario tooset gli account in modo che il ripristino del sito possono accedere al server VMware e le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="68917-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="68917-115">**Macchine virtuali replicate**: le macchine virtuali desiderate tooreplicate necessità toocomply ai requisiti di Azure e hanno installato il componente del servizio Mobility hello.</span><span class="sxs-lookup"><span data-stu-id="68917-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="68917-116">Andare troppo[passaggio 2: esaminare i prerequisiti e limitazioni](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="68917-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="68917-117">Passaggio 3: Pianificare la capacità</span><span class="sxs-lookup"><span data-stu-id="68917-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="68917-118">Se si sta eseguendo una distribuzione completa, è necessario toofigure risorse quali la replica è necessario.</span><span class="sxs-lookup"><span data-stu-id="68917-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="68917-119">Esistono un paio di strumenti disponibili toohelp si esegue questa operazione.</span><span class="sxs-lookup"><span data-stu-id="68917-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="68917-120">Passare tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="68917-120">Go tooStep 2.</span></span> <span data-ttu-id="68917-121">Se si sta eseguendo una rapida Configura tootest hello ambiente è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="68917-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="68917-122">Andare troppo[passaggio 3: pianificare la capacità](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="68917-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="68917-123">Passaggio 4: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="68917-123">Step 4: Plan networking</span></span>

<span data-ttu-id="68917-124">È necessario toodo alcuni pianificazione tooensure che macchine virtuali di Azure siano connessi toonetworks dopo che si verifica il failover e che dispongano di hello destra indirizzi IP della rete.</span><span class="sxs-lookup"><span data-stu-id="68917-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="68917-125">Andare troppo[passaggio 4: pianificare la rete](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="68917-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="68917-126">Passaggio 5: Preparare le risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="68917-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="68917-127">Configurare le reti e le risorse di archiviazione di Azure prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="68917-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="68917-128">È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="68917-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="68917-129">Andare troppo[passaggio 5: preparare Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="68917-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="68917-130">Passaggio 6: Preparare VMware</span><span class="sxs-lookup"><span data-stu-id="68917-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="68917-131">È necessario tooset gli account utilizzati per il ripristino del sito:</span><span class="sxs-lookup"><span data-stu-id="68917-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="68917-132">Accesso VMware virtualizzazione server tooautomatically rilevare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="68917-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="68917-133">Accedere a servizio di mobilità hello tooinstall macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="68917-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="68917-134">Ogni macchina virtuale si desidera tooreplicate deve avere l'agente di servizio di mobilità hello installato prima possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="68917-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="68917-135">Andare troppo[passaggio 6: preparazione VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="68917-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="68917-136">Passaggio 7: Configurare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="68917-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="68917-137">È necessario tooset backup un tooorchestrate insieme di credenziali di servizi di ripristino e gestire la replica.</span><span class="sxs-lookup"><span data-stu-id="68917-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="68917-138">Quando si imposta l'insieme di credenziali hello, specificare gli elementi da tooreplicate, e in cui si desidera tooreplicate a.</span><span class="sxs-lookup"><span data-stu-id="68917-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="68917-139">Andare troppo[passaggio 7: configurare un insieme di credenziali](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="68917-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="68917-140">Passaggio 8: Configurare le impostazioni di origine e di destinazione</span><span class="sxs-lookup"><span data-stu-id="68917-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="68917-141">Consente di impostare hello origine e di destinazione che viene utilizzato per la replica.</span><span class="sxs-lookup"><span data-stu-id="68917-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="68917-142">Configurare le impostazioni dell'origine include l'esecuzione del programma di installazione unificata tooinstall componenti Site Recovery di hello locali.</span><span class="sxs-lookup"><span data-stu-id="68917-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="68917-143">Andare troppo[passaggio 8: impostare hello origine e di destinazione](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="68917-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="68917-144">Passaggio 9: Configurare i criteri di replica</span><span class="sxs-lookup"><span data-stu-id="68917-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="68917-145">Impostare le impostazioni di replica toospecify un criterio per le macchine virtuali VMware nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="68917-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="68917-146">Andare troppo[passaggio 9: configurare un criterio di replica](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="68917-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="68917-147">Passaggio 10: Installare il servizio di mobilità hello</span><span class="sxs-lookup"><span data-stu-id="68917-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="68917-148">servizio di mobilità Hello deve essere installato in ogni macchina virtuale si desidera tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="68917-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="68917-149">Esistono alcuni modi tooset servizio hello con installazione push o pull.</span><span class="sxs-lookup"><span data-stu-id="68917-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="68917-150">Andare troppo[passaggio 10: installare il servizio Mobility hello](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="68917-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="68917-151">Passaggio 11: Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="68917-151">Step 11: Enable replication</span></span>

<span data-ttu-id="68917-152">Dopo che il servizio di mobilità hello è in esecuzione in una macchina virtuale è possibile abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="68917-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="68917-153">Dopo aver abilitato, viene eseguita la replica iniziale di VM hello.</span><span class="sxs-lookup"><span data-stu-id="68917-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="68917-154">Andare troppo[passaggio 11: abilitare la replica](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="68917-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="68917-155">Passaggio 12: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="68917-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="68917-156">Dopo il completamento della replica iniziale e la replica differenziale è in esecuzione, è possibile eseguire un toomake di failover di test che tutto funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="68917-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="68917-157">Andare troppo[passaggio 12: eseguire un failover di test](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="68917-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
