---
title: Preparare le risorse di Azure per la replica di VM Hyper-V (senza System Center VMM) in Azure usando Azure Site Recovery| Microsoft Docs
description: Vengono descritti gli elementi necessari in Azure prima di iniziare la replica di VM Hyper-V (senza VMM) in Azure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="def7c-103">Passaggio 5: Preparare le risorse di Azure per la replica Hyper-V in Azure</span><span class="sxs-lookup"><span data-stu-id="def7c-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="def7c-104">Usare le istruzioni in questo articolo per preparare le risorse di Azure in modo che sia possibile eseguire la replica delle VM Hyper-V locali (senza System Center VMM) in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="def7c-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="def7c-105">Dopo la lettura di questo articolo, è possibile inserire commenti nella parte inferiore oppure porre domande tecniche nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="def7c-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="def7c-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="def7c-106">Before you start</span></span>

<span data-ttu-id="def7c-107">Assicurarsi di aver letto i [prerequisiti](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="def7c-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="def7c-108">Configurare un account Azure</span><span class="sxs-lookup"><span data-stu-id="def7c-108">Set up an Azure account</span></span>

- <span data-ttu-id="def7c-109">Ottenere un [account Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="def7c-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="def7c-110">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="def7c-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="def7c-111">Consultare le informazioni sulla disponibilità a livello geografico e sulle aree supportate nella pagina relativa ai [dettagli sui prezzi per Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="def7c-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="def7c-112">Leggere le informazioni sui [prezzi di Site Recovery](site-recovery-faq.md#pricing) e ottenere i [dettagli dei prezzi](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="def7c-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="def7c-113">Configurare una rete di Azure</span><span class="sxs-lookup"><span data-stu-id="def7c-113">Set up an Azure network</span></span>

- <span data-ttu-id="def7c-114">Configurare una rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="def7c-114">Set up an Azure network.</span></span> <span data-ttu-id="def7c-115">Le VM di Azure create dopo il failover verranno inserite in questa rete.</span><span class="sxs-lookup"><span data-stu-id="def7c-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="def7c-116">La rete deve trovarsi nella stessa area dell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="def7c-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="def7c-117">Site Recovery nel portale di Azure può usare reti configurate in [Gestione risorse](../resource-manager-deployment-model.md) o in modalità classica.</span><span class="sxs-lookup"><span data-stu-id="def7c-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="def7c-118">È consigliabile configurare una rete prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="def7c-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="def7c-119">In caso contrario sarà necessario eseguire l'operazione durante la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="def7c-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="def7c-120">Leggere le informazioni sui [prezzi per la rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="def7c-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="def7c-121">Configurare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="def7c-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="def7c-122">Site Recovery replica le macchine locali in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="def7c-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="def7c-123">Le VM di Azure vengono create dalla risorsa di archiviazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="def7c-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="def7c-124">Configurare un [account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) Standard/Premium in cui inserire i dati replicati in Azure.</span><span class="sxs-lookup"><span data-stu-id="def7c-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="def7c-125">[Archiviazione Premium](../storage/common/storage-premium-storage.md) si usa in genere per le macchine virtuali che richiedono un livello di prestazioni di I/O costantemente elevato e bassa latenza per ospitare carichi di lavoro con numerose operazioni di I/O.</span><span class="sxs-lookup"><span data-stu-id="def7c-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="def7c-126">Se si vuole usare un account Premium per archiviare i dati replicati, sarà necessario anche un account di archiviazione standard per l'archiviazione dei log di replica in cui vengono acquisite le modifiche in corso ai dati locali.</span><span class="sxs-lookup"><span data-stu-id="def7c-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="def7c-127">A seconda del modello di risorsa da usare per le macchine virtuali di Azure di cui si esegue il failover, l'account deve essere configurato in [modalità Resource Manager](../storage/common/storage-create-storage-account.md) o in [modalità classica](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="def7c-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="def7c-128">È consigliabile configurare un account di archiviazione prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="def7c-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="def7c-129">In caso contrario sarà necessario eseguire l'operazione durante la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="def7c-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="def7c-130">L'account deve trovarsi nella stessa area dell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="def7c-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="def7c-131">Non è possibile spostare gli account di archiviazione usati da Site Recovery tra gruppi di risorse nella stessa sottoscrizione o in diverse sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="def7c-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="def7c-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="def7c-132">Next steps</span></span>

<span data-ttu-id="def7c-133">Andare a [Passaggio 6: Preparare le risorse Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="def7c-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
