---
title: aaaMigrate le macchine virtuali IaaS di Azure tra le aree di Azure | Documenti Microsoft
description: Utilizzare macchine virtuali di Azure Site Recovery toomigrate IaaS di Azure da un'area di Azure tooanother.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="05c48-103">Eseguire la migrazione delle macchine virtuali IaaS di Azure tra aree di Azure con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="05c48-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="05c48-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="05c48-104">Overview</span></span>
<span data-ttu-id="05c48-105">Benvenuti tooAzure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="05c48-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="05c48-106">Se si desidera toomigrate macchine virtuali di Azure tra le aree di Azure, usare questo articolo.</span><span class="sxs-lookup"><span data-stu-id="05c48-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="05c48-107">Prima di iniziare, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="05c48-107">Before you start, note that:</span></span>

* <span data-ttu-id="05c48-108">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="05c48-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="05c48-109">Azure offre inoltre due portali: hello portale di Azure classico che supporta il modello di distribuzione classica hello e hello portale di Azure con il supporto per entrambi i modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="05c48-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="05c48-110">passaggi di base Hello per la migrazione sono hello stesso se si sta configurando il ripristino del sito di gestione risorse o classica.</span><span class="sxs-lookup"><span data-stu-id="05c48-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="05c48-111">Tuttavia hello istruzioni dell'interfaccia utente e le schermate contenute in questo articolo sono rilevanti per hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="05c48-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="05c48-112">**Attualmente è possibile migrare solo da un'area tooanother. È possibile eseguire il failover le macchine virtuali da un'area di Azure tooanother, ma non è possibile eseguire tali torna nuovamente.**</span><span class="sxs-lookup"><span data-stu-id="05c48-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="05c48-113">Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="05c48-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05c48-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="05c48-114">Prerequisites</span></span>
<span data-ttu-id="05c48-115">Per la distribuzione è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="05c48-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="05c48-116">**Macchine virtuali IaaS**: hello macchine virtuali che si desidera toomigrate.</span><span class="sxs-lookup"><span data-stu-id="05c48-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="05c48-117">Nella migrazione queste VM vengono considerate macchine fisiche.</span><span class="sxs-lookup"><span data-stu-id="05c48-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="05c48-118">Passaggi di distribuzione</span><span class="sxs-lookup"><span data-stu-id="05c48-118">Deployment steps</span></span>
<span data-ttu-id="05c48-119">Questa sezione descrive i passaggi di distribuzione hello nel nuovo portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="05c48-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="05c48-120">[Creare un insieme di credenziali](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="05c48-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="05c48-121">[Abilitare la replica](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="05c48-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="05c48-122">Abilitare la replica per le macchine virtuali toomigrate desiderato e scegliere Azure come origine hello.</span><span class="sxs-lookup"><span data-stu-id="05c48-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="05c48-123">[ Eseguire un failover non pianificato](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="05c48-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="05c48-124">Una volta completata la replica iniziale, è possibile eseguire un failover non pianificato da tooanother di una regione di Azure.</span><span class="sxs-lookup"><span data-stu-id="05c48-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="05c48-125">Facoltativamente, è possibile creare un piano di ripristino ed eseguire un failover non pianificato, toomigrate più macchine virtuali tra aree.</span><span class="sxs-lookup"><span data-stu-id="05c48-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="05c48-126">[Ulteriori informazioni](site-recovery-create-recovery-plans.md) sui piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="05c48-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05c48-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05c48-127">Next steps</span></span>
<span data-ttu-id="05c48-128">Per altre informazioni sui vari scenari di replica, vedere [Che cos'è Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="05c48-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
