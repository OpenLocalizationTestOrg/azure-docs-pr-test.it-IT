---
title: aaaReplicate macchine virtuali di Azure tra le aree di Azure | Microsoft documenti
description: Riepiloga tooreplicate necessari passaggi hello macchine virtuali di Azure tra le aree di Azure con il servizio Azure Site Recovery hello in hello portale di Azure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="7343a-103">Eseguire la replica delle VM di Azure tra le aree con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="7343a-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="7343a-104">Questo articolo fornisce una panoramica di hello passaggi necessari tooreplicate macchine virtuali di Azure (VM) in un'area di Azure tooAzure macchine virtuali in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="7343a-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="7343a-105">La replica di macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="7343a-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="7343a-106">Inviare commenti e domande nella parte inferiore di hello di questo articolo o di hello [forum di servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7343a-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="7343a-107">Passaggio 1: Esaminare l'architettura</span><span class="sxs-lookup"><span data-stu-id="7343a-107">Step 1: Review architecture</span></span>

<span data-ttu-id="7343a-108">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario hello e i componenti di hello è necessario toodeploy.</span><span class="sxs-lookup"><span data-stu-id="7343a-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="7343a-109">Andare troppo[passaggio 1: esaminare l'architettura di hello](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="7343a-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="7343a-110">Passaggio 2: Esaminare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7343a-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="7343a-111">Verificare che si sono hello Azure prerequisiti in posizioni, tra cui una sottoscrizione, le reti virtuali, gli account di archiviazione e i requisiti macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7343a-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="7343a-112">Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="7343a-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="7343a-113">Passaggio 3: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="7343a-113">Step 3: Plan networking</span></span>

<span data-ttu-id="7343a-114">Verificare che la connettività in uscita sia impostata su macchine virtuali di Azure, si desidera tooreplicate e che le connessioni da locale siano impostate.</span><span class="sxs-lookup"><span data-stu-id="7343a-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="7343a-115">Andare troppo[passaggio 4: pianificare la rete](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="7343a-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="7343a-116">Passaggio 4: Creare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="7343a-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="7343a-117">È necessario tooset backup un tooorchestrate insieme di credenziali di servizi di ripristino e gestire la replica e specificare l'area di origine hello.</span><span class="sxs-lookup"><span data-stu-id="7343a-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="7343a-118">Andare troppo[passaggio 4: creare un insieme di credenziali](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="7343a-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="7343a-119">Passaggio 5: Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="7343a-119">Step 5: Enable replication</span></span>


<span data-ttu-id="7343a-120">replica tooenable, configurare le impostazioni percorso di destinazione, impostare un criterio di replica e selezionare hello macchine virtuali di Azure che si desidera tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="7343a-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="7343a-121">Dopo aver abilitato, viene eseguita la replica iniziale di VM hello.</span><span class="sxs-lookup"><span data-stu-id="7343a-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="7343a-122">Andare troppo[passaggio 5: abilitare la replica](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="7343a-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="7343a-123">Passaggio 6: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="7343a-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="7343a-124">Dopo il completamento della replica iniziale e la replica differenziale è in esecuzione, è possibile eseguire un toomake di failover di test che tutto funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="7343a-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="7343a-125">Andare troppo[passaggio 6: eseguire un failover di test](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="7343a-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


