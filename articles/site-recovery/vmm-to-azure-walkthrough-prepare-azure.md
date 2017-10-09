---
title: aaaPrepare risorse di Azure tooreplicate macchine virtuali Hyper-V (con System Center VMM) tooAzure usando Azure Site Recovery | Documenti Microsoft
description: Descrive i passaggi presenti in Azure prima di iniziare la replica delle macchine virtuali Hyper-V (con VMM) tooAzure, usando Azure Site Recovery
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
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="34ef0-103">Passaggio 5: Preparare le risorse di Azure per Hyper-V replica (con VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="34ef0-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="34ef0-104">Dopo aver verificato [requisiti di rete](vmm-to-azure-walkthrough-network.md), utilizzare istruzioni hello in questa tooprepare articolo Azure le risorse in modo che è possibile replicare le macchine virtuali Hyper-V in locale in System Center Virtual Machine Manager (VMM) cloud tooAzure, utilizzando Hello [Azure Site Recovery](site-recovery-overview.md) servizio.</span><span class="sxs-lookup"><span data-stu-id="34ef0-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="34ef0-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="34ef0-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="34ef0-106">Configurare un account Azure</span><span class="sxs-lookup"><span data-stu-id="34ef0-106">Set up an Azure account</span></span>

- <span data-ttu-id="34ef0-107">Ottenere un [account Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="34ef0-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="34ef0-108">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34ef0-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="34ef0-109">Verificare le aree di hello è supportato per il ripristino del sito, in aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="34ef0-109">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="34ef0-110">Informazioni su [dei prezzi di Site Recovery](site-recovery-faq.md#pricing)e ottenere hello [prezzi](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="34ef0-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="34ef0-111">Verificare che l'account di Azure è hello corretto [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="34ef0-111">Make sure your Azure account has hello correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VMs.</span></span> <span data-ttu-id="34ef0-112">[Altre informazioni](../active-directory/role-based-access-built-in-roles.md) sul controllo degli accessi in base al ruolo di Azure.</span><span class="sxs-lookup"><span data-stu-id="34ef0-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="34ef0-113">Configurare una rete di Azure</span><span class="sxs-lookup"><span data-stu-id="34ef0-113">Set up an Azure network</span></span>

- <span data-ttu-id="34ef0-114">Configurare una [rete di Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="34ef0-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="34ef0-115">Le VM di Azure create dopo il failover verranno inserite in questa rete.</span><span class="sxs-lookup"><span data-stu-id="34ef0-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="34ef0-116">rete Hello devono trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="34ef0-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="34ef0-117">Il ripristino del sito nel portale di Azure hello può utilizzare reti configurate in [Gestione risorse](../resource-manager-deployment-model.md), o in modalità classica.</span><span class="sxs-lookup"><span data-stu-id="34ef0-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="34ef0-118">È consigliabile configurare una rete prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="34ef0-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="34ef0-119">In caso contrario, è necessario toodo durante la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="34ef0-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="34ef0-120">Leggere le informazioni sui [prezzi per la rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="34ef0-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="34ef0-121">Configurare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="34ef0-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="34ef0-122">Il ripristino del sito vengono replicati archiviazione tooAzure di computer locale.</span><span class="sxs-lookup"><span data-stu-id="34ef0-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="34ef0-123">Macchine virtuali di Azure vengono create dall'archiviazione hello dopo che si verifica il failover.</span><span class="sxs-lookup"><span data-stu-id="34ef0-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="34ef0-124">Impostare un standard o premium [account di archiviazione Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dati replicati tooAzure.</span><span class="sxs-lookup"><span data-stu-id="34ef0-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="34ef0-125">[Archiviazione Premium](../storage/common/storage-premium-storage.md) viene in genere utilizzato per le macchine virtuali che richiedono un costantemente elevato delle prestazioni dei / o e carichi di lavoro con utilizzo intensivo a bassa latenza toohost IO.</span><span class="sxs-lookup"><span data-stu-id="34ef0-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="34ef0-126">Se si desidera toouse un toostore account premium dati replicati, è inoltre necessario disporre di un log del replica toostore account di archiviazione standard che in corso di acquisizione Cambia dati tooon locali.</span><span class="sxs-lookup"><span data-stu-id="34ef0-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="34ef0-127">A seconda del modello di risorsa hello desiderate toouse per eseguire il failover le macchine virtuali di Azure, è configurato un account in [modalità di gestione risorse](../storage/common/storage-create-storage-account.md), o [modalità classica](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="34ef0-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="34ef0-128">È consigliabile configurare un account di archiviazione prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="34ef0-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="34ef0-129">In caso contrario, è necessario toodo durante la distribuzione di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="34ef0-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="34ef0-130">Hello devono trovarsi nello hello stessa area hello insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="34ef0-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="34ef0-131">Non è possibile spostare gli account di archiviazione utilizzato da Site Recovery nei gruppi di risorse all'interno di hello stessa sottoscrizione, o in diverse sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="34ef0-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="34ef0-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34ef0-132">Next steps</span></span>

<span data-ttu-id="34ef0-133">Andare troppo[passaggio 6: preparazione di VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="34ef0-133">Go too[Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
