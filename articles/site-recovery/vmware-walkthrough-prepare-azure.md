---
title: aaaPrepare risorse di Azure tooreplicate locale tooAzure le macchine virtuali VMware usando Azure Site Recovery | Documenti Microsoft
description: Descrive i passaggi presenti in Azure prima di iniziare la replica locale le macchine virtuali VMware tooAzure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a><span data-ttu-id="e9e0f-103">Passaggio 5: Preparare le risorse di Azure per tooAzure replica VMWare</span><span class="sxs-lookup"><span data-stu-id="e9e0f-103">Step 5: Prepare Azure resources for VMWare replication tooAzure</span></span>


<span data-ttu-id="e9e0f-104">Utilizzare istruzioni hello in questa tooprepare articolo Azure le risorse in modo che è possibile replicare tooAzure macchine locali utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises machines tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="e9e0f-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e9e0f-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e9e0f-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e9e0f-106">Before you start</span></span>

<span data-ttu-id="e9e0f-107">Assicurarsi di avere letto hello [prerequisiti](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="e9e0f-107">Make sure you've read hello [prerequisites](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="e9e0f-108">Configurare un account Azure</span><span class="sxs-lookup"><span data-stu-id="e9e0f-108">Set up an Azure account</span></span>

- <span data-ttu-id="e9e0f-109">Ottenere un [account Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e9e0f-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="e9e0f-110">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9e0f-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="e9e0f-111">Verificare le aree di hello è supportato per il ripristino del sito, in aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="e9e0f-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="e9e0f-112">Informazioni su [dei prezzi di Site Recovery](site-recovery-faq.md#pricing)e ottenere hello [prezzi](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="e9e0f-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="e9e0f-113">Configurare una rete di Azure</span><span class="sxs-lookup"><span data-stu-id="e9e0f-113">Set up an Azure network</span></span>

- <span data-ttu-id="e9e0f-114">Configurare una rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-114">Set up an Azure network.</span></span> <span data-ttu-id="e9e0f-115">Le VM di Azure create dopo il failover verranno inserite in questa rete.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="e9e0f-116">Il ripristino del sito nel portale di Azure hello può utilizzare reti configurate in [Gestione risorse](../resource-manager-deployment-model.md), o in modalità classica.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="e9e0f-117">rete Hello devono trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="e9e0f-117">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="e9e0f-118">Leggere le informazioni sui [prezzi per la rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="e9e0f-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="e9e0f-119">Altre informazioni sulla [connettività della macchina virtuale di Azure](site-recovery-network-design.md) dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-119">Learn more about [Azure VM connectivity](site-recovery-network-design.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="e9e0f-120">Configurare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e9e0f-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="e9e0f-121">Il ripristino del sito vengono replicati archiviazione tooAzure di computer locale.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-121">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="e9e0f-122">Macchine virtuali di Azure vengono create dall'archiviazione hello dopo che si verifica il failover.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="e9e0f-123">Configurare un [account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) per i dati replicati.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="e9e0f-124">Ripristino del sito in hello portale di Azure è possibile utilizzare gli account di archiviazione impostato in Gestione risorse o in modalità classica.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="e9e0f-125">account di archiviazione Hello può essere standard o [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e9e0f-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="e9e0f-126">Se si configura un account Premium, sarà necessario anche un altro account Standard per i dati di log.</span><span class="sxs-lookup"><span data-stu-id="e9e0f-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e9e0f-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e9e0f-127">Next steps</span></span>

<span data-ttu-id="e9e0f-128">Andare troppo[passaggio 6: preparazione VMware risorse](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="e9e0f-128">Go too[Step 6: Prepare VMware resources](vmware-walkthrough-prepare-vmware.md)</span></span>
