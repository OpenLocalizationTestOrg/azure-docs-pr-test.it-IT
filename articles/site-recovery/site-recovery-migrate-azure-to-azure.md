---
title: Eseguire la migrazione di macchine virtuali IaaS di Azure tra aree di Azure | Documentazione Microsoft
description: "Utilizzare Site Recovery per la migrazione di macchine virtuali IaaS di Azure da un’area di Azure a un’altra."
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
ms.openlocfilehash: ef2972c077a2b1dd2b2fd6ce53cc6560520ea870
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="968c1-103">Eseguire la migrazione delle macchine virtuali IaaS di Azure tra aree di Azure con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="968c1-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="968c1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="968c1-104">Overview</span></span>
<span data-ttu-id="968c1-105">Benvenuti in Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="968c1-105">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="968c1-106">Consultare questo articolo se si desidera eseguire la migrazione di VM di Azure tra aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="968c1-106">Use this article if you want to migrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="968c1-107">Prima di iniziare, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="968c1-107">Before you start, note that:</span></span>

* <span data-ttu-id="968c1-108">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="968c1-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="968c1-109">Sono anche disponibili il portale di Azure classico, che supporta il modello di distribuzione classica, e il portale di Azure, che supporta entrambi i modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="968c1-109">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="968c1-110">I passaggi di base per la migrazione sono gli stessi indipendentemente dal fatto che si stia configurando Site Recovery in Resource Manager o nel modello classico.</span><span class="sxs-lookup"><span data-stu-id="968c1-110">The basic steps for migration are the same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="968c1-111">Tuttavia, le istruzioni e le schermate dell'interfaccia utente presenti in questo articolo sono pertinenti al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="968c1-111">However the UI instructions and screenshots in this article are relevant for the Azure portal.</span></span>
* <span data-ttu-id="968c1-112">**Attualmente è possibile eseguire la migrazione solo da un'area a un'altra. Si può eseguire il failover di VM da un'area di Azure a un'altra ma non è possibile eseguire il failback.**</span><span class="sxs-lookup"><span data-stu-id="968c1-112">**Currently you can only migrate from one region to another. You can fail over VMs from one Azure region to another, but you can't fail them back again.**</span></span>

<span data-ttu-id="968c1-113">Per inviare commenti o domande, è possibile usare la parte inferiore di questo articolo oppure il [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="968c1-113">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="968c1-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="968c1-114">Prerequisites</span></span>
<span data-ttu-id="968c1-115">Per la distribuzione è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="968c1-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="968c1-116">**Macchine virtuali IaaS**: le VM di cui si desidera eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="968c1-116">**IaaS virtual machines**: The VMs you want to migrate.</span></span> <span data-ttu-id="968c1-117">Nella migrazione queste VM vengono considerate macchine fisiche.</span><span class="sxs-lookup"><span data-stu-id="968c1-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="968c1-118">Passaggi di distribuzione</span><span class="sxs-lookup"><span data-stu-id="968c1-118">Deployment steps</span></span>
<span data-ttu-id="968c1-119">Questa sezione descrive i passaggi di distribuzione nel nuovo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="968c1-119">This section describes the deployment steps in the new Azure portal.</span></span>

1. <span data-ttu-id="968c1-120">[Creare un insieme di credenziali](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="968c1-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="968c1-121">[Abilitare la replica](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="968c1-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="968c1-122">Abilitare la replica per le VM da migrare, quindi scegliere Azure come origine.</span><span class="sxs-lookup"><span data-stu-id="968c1-122">Enable replication for the VMs you want to migrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="968c1-123">[ Eseguire un failover non pianificato](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="968c1-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="968c1-124">Dopo il completamento della replica iniziale, è possibile eseguire un failover non pianificato da un'area di Azure a un'altra.</span><span class="sxs-lookup"><span data-stu-id="968c1-124">After initial replication is complete, you can run an unplanned failover from one Azure region to another.</span></span> <span data-ttu-id="968c1-125">Facoltativamente, è possibile creare un piano di ripristino ed eseguire un failover non pianificato, per eseguire la migrazione di più macchine virtuali tra regioni.</span><span class="sxs-lookup"><span data-stu-id="968c1-125">Optionally, you can create a recovery plan and run an unplanned failover, to migrate multiple virtual machines between regions.</span></span> <span data-ttu-id="968c1-126">[Ulteriori informazioni](site-recovery-create-recovery-plans.md) sui piani di ripristino.</span><span class="sxs-lookup"><span data-stu-id="968c1-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="968c1-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="968c1-127">Next steps</span></span>
<span data-ttu-id="968c1-128">Per altre informazioni sui vari scenari di replica, vedere [Che cos'è Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="968c1-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
