---
title: Preparare le risorse di Azure per la replica di VM Hyper-V (con System Center VMM) in Azure usando Azure Site Recovery| Microsoft Docs
description: Illustra gli elementi necessari in Azure prima di iniziare la replica di VM Hyper-V (con VMM) in Azure tramite Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 63b005f37ab5e15e8a1b4645446d65f1529f1bbd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="78d44-103">Passaggio 5: Preparare le risorse di Azure per la replica Hyper-V in Azure (con VMM)</span><span class="sxs-lookup"><span data-stu-id="78d44-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="78d44-104">Dopo avere verificato i [requisiti di rete](vmm-to-azure-walkthrough-network.md), usare le istruzioni disponibili in questo articolo per preparare le risorse di Azure in modo da replicare le VM Hyper-V locali in cloud System Center Virtual Machine Manager (VMM) in Azure tramite il servizio [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78d44-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="78d44-105">Dopo la lettura di questo articolo, è possibile inserire commenti nella parte inferiore oppure porre domande tecniche nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="78d44-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="78d44-106">Configurare un account Azure</span><span class="sxs-lookup"><span data-stu-id="78d44-106">Set up an Azure account</span></span>

- <span data-ttu-id="78d44-107">Ottenere un [account Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="78d44-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="78d44-108">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78d44-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="78d44-109">Consultare le informazioni sulla disponibilità a livello geografico e sulle aree supportate nella pagina relativa ai [dettagli sui prezzi per Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="78d44-109">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="78d44-110">Leggere le informazioni sui [prezzi di Site Recovery](site-recovery-faq.md#pricing) e ottenere i [dettagli dei prezzi](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="78d44-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="78d44-111">Assicurarsi che l'account Azure includa le [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) corrette per la creazione di VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="78d44-111">Make sure your Azure account has the correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)to create Azure VMs.</span></span> <span data-ttu-id="78d44-112">[Altre informazioni](../active-directory/role-based-access-built-in-roles.md) sul controllo degli accessi in base al ruolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="78d44-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="78d44-113">Configurare una rete di Azure</span><span class="sxs-lookup"><span data-stu-id="78d44-113">Set up an Azure network</span></span>

- <span data-ttu-id="78d44-114">Configurare una [rete di Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="78d44-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="78d44-115">Le VM di Azure create dopo il failover verranno inserite in questa rete.</span><span class="sxs-lookup"><span data-stu-id="78d44-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="78d44-116">La rete deve trovarsi nella stessa area dell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="78d44-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="78d44-117">Site Recovery nel portale di Azure può usare reti configurate in [Gestione risorse](../resource-manager-deployment-model.md) o in modalità classica.</span><span class="sxs-lookup"><span data-stu-id="78d44-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="78d44-118">È consigliabile configurare una rete prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="78d44-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="78d44-119">In caso contrario sarà necessario eseguire l'operazione durante la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="78d44-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="78d44-120">Leggere le informazioni sui [prezzi per la rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="78d44-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="78d44-121">Configurare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="78d44-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="78d44-122">Site Recovery replica le macchine locali in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="78d44-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="78d44-123">Le VM di Azure vengono create dalla risorsa di archiviazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="78d44-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="78d44-124">Configurare un [account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) Standard/Premium in cui inserire i dati replicati in Azure.</span><span class="sxs-lookup"><span data-stu-id="78d44-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="78d44-125">[Archiviazione Premium](../storage/common/storage-premium-storage.md) si usa in genere per le macchine virtuali che richiedono un livello di prestazioni di I/O costantemente elevato e bassa latenza per ospitare carichi di lavoro con numerose operazioni di I/O.</span><span class="sxs-lookup"><span data-stu-id="78d44-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="78d44-126">Se si vuole usare un account Premium per archiviare i dati replicati, sarà necessario anche un account di archiviazione standard per l'archiviazione dei log di replica in cui vengono acquisite le modifiche in corso ai dati locali.</span><span class="sxs-lookup"><span data-stu-id="78d44-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="78d44-127">A seconda del modello di risorsa da usare per le macchine virtuali di Azure di cui si esegue il failover, l'account deve essere configurato in [modalità Resource Manager](../storage/common/storage-create-storage-account.md) o in [modalità classica](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="78d44-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="78d44-128">È consigliabile configurare un account di archiviazione prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="78d44-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="78d44-129">In caso contrario sarà necessario eseguire l'operazione durante la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="78d44-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="78d44-130">L'account deve trovarsi nella stessa area dell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="78d44-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="78d44-131">Non è possibile spostare gli account di archiviazione usati da Site Recovery tra gruppi di risorse nella stessa sottoscrizione o in diverse sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="78d44-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="78d44-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78d44-132">Next steps</span></span>

<span data-ttu-id="78d44-133">Andare al [Passaggio 6: Preparare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="78d44-133">Go to [Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
