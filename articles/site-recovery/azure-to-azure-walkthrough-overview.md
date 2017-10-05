---
title: Eseguire la replica di macchine virtuali di Azure tra aree di Azure | Microsoft Docs
description: Offre un riepilogo sulla procedura necessaria per eseguire la replica delle macchine virtuali di Azure tra aree di Azure mediante il servizio Azure Site Recovery nel portale di Azure
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
ms.openlocfilehash: 9258613161a61e36b1d0c5796d5763c916d66859
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="1c3d4-103">Eseguire la replica delle VM di Azure tra le aree con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1c3d4-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="1c3d4-104">Questo articolo offre una panoramica della procedura necessaria per eseguire la replica di macchine virtuali di Azure in un'area di Azure a macchine virtuali in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-104">This article provides an overview of the steps required to replicate Azure virtual machines (VMs) in one Azure region to Azure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="1c3d4-105">La replica delle macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="1c3d4-106">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum su Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1c3d4-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="1c3d4-107">Passaggio 1: Esaminare l'architettura</span><span class="sxs-lookup"><span data-stu-id="1c3d4-107">Step 1: Review architecture</span></span>

<span data-ttu-id="1c3d4-108">Prima di iniziare la distribuzione, esaminare l'architettura dello scenario e i componenti che è necessario distribuire.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-108">Before you start deployment, review the scenario architecture, and the components you need to deploy.</span></span>

<span data-ttu-id="1c3d4-109">Andare a [Passaggio 1: Esaminare l'architettura](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="1c3d4-109">Go to [Step 1: Review the architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="1c3d4-110">Passaggio 2: Esaminare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1c3d4-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="1c3d4-111">Verificare di aver soddisfatto i prerequisiti di Azure, tra cui una sottoscrizione, reti virtuali, account di archiviazione e i requisiti delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-111">Check that you have the Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="1c3d4-112">Andare a [Passaggio 2: Esaminare i prerequisiti e le limitazioni](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="1c3d4-112">Go to [Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="1c3d4-113">Passaggio 3: Pianificare la rete</span><span class="sxs-lookup"><span data-stu-id="1c3d4-113">Step 3: Plan networking</span></span>

<span data-ttu-id="1c3d4-114">Verificare che la connettività in uscita sia impostata nelle macchine virtuali di Azure da replicare e che le connessioni locali siano impostate.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-114">Check that outbound connectivity is set up on Azure VMs you want to replicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="1c3d4-115">Andare a [Passaggio 4: Pianificare la rete](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="1c3d4-115">Go to [Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="1c3d4-116">Passaggio 4: Creare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="1c3d4-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="1c3d4-117">È necessario configurare un insieme di credenziali di Servizi di ripristino per orchestrare e gestire la replica e anche specificare l'area di origine.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-117">You need to set up a Recovery Services vault to orchestrate and manage replication, and specify the source region.</span></span>

<span data-ttu-id="1c3d4-118">Andare a [Passaggio 4: Creare un insieme di credenziali](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="1c3d4-118">Go to [Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="1c3d4-119">Passaggio 5: Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="1c3d4-119">Step 5: Enable replication</span></span>


<span data-ttu-id="1c3d4-120">Per abilitare la replica, configurare le impostazioni del percorso di destinazione, impostare i criteri di replica e selezionare le macchine virtuali di Azure da replicare.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-120">To enable replication, you configure target location settings, set up a replication policy, and select the Azure VMs that you want to replicate.</span></span> <span data-ttu-id="1c3d4-121">Dopo l'abilitazione, viene eseguita la replica iniziale delle VM.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-121">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="1c3d4-122">Andare a [Passaggio 5: Abilitare la replica](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="1c3d4-122">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="1c3d4-123">Passaggio 6: Eseguire un failover di test</span><span class="sxs-lookup"><span data-stu-id="1c3d4-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="1c3d4-124">Dopo il completamento della replica iniziale e con la replica differenziale in esecuzione, è possibile eseguire un failover di test per verificare che tutto funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="1c3d4-124">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="1c3d4-125">Andare a [Passaggio 6: Eseguire un failover di test](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="1c3d4-125">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


