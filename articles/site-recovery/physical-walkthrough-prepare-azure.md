---
title: Preparare le risorse di Azure per replicare i server fisici in Azure usando Azure Site Recovery | Microsoft Docs
description: Descrive gli elementi necessari in Azure prima di iniziare la replica di server fisici locali in Azure usando il servizio Azure Site Recovery
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
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b7411fa6aba04ffd34f3f4bd03e706ca75afc9c8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-to-azure"></a><span data-ttu-id="5c3fc-103">Passaggio 5: Preparare le risorse di Azure per la replica di server fisici in Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fc-103">Step 5: Prepare Azure resources for physical server replication to Azure</span></span>


<span data-ttu-id="5c3fc-104">Usare le istruzioni in questo articolo per preparare le risorse di Azure in modo che sia possibile replicare i server locali in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="5c3fc-105">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5c3fc-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5c3fc-106">Before you start</span></span>

<span data-ttu-id="5c3fc-107">Assicurarsi di aver letto i [prerequisiti](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-107">Make sure you've read the [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="5c3fc-108">Configurare un account Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fc-108">Set up an Azure account</span></span>

- <span data-ttu-id="5c3fc-109">Ottenere un [account Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="5c3fc-110">È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="5c3fc-111">Controllare le aree supportare per Site Recovery nella sezione **Disponibilità a livello geografico** della pagina [Dettagli sui prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-111">Check the supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="5c3fc-112">Leggere le informazioni sui [prezzi di Site Recovery](site-recovery-faq.md#pricing) e ottenere i [dettagli dei prezzi](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="5c3fc-113">Configurare una rete di Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fc-113">Set up an Azure network</span></span>

- <span data-ttu-id="5c3fc-114">Configurare una rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-114">Set up an Azure network.</span></span> <span data-ttu-id="5c3fc-115">Le VM di Azure create dopo il failover verranno inserite in questa rete.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="5c3fc-116">Site Recovery nel portale di Azure può usare reti configurate in [Gestione risorse](../resource-manager-deployment-model.md) o in modalità classica.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-116">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="5c3fc-117">La rete deve trovarsi nella stessa area dell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-117">The network should be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="5c3fc-118">Leggere le informazioni sui [prezzi per la rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="5c3fc-119">Altre informazioni sulla [connettività della macchina virtuale di Azure](physical-walkthrough-network.md) dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="5c3fc-120">Configurare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5c3fc-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="5c3fc-121">Site Recovery replica i server locali in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-121">Site Recovery replicates on-premises servers to Azure storage.</span></span> <span data-ttu-id="5c3fc-122">Le macchine virtuali di Azure vengono create dalla risorsa di archiviazione dopo che si verifica il failover.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-122">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="5c3fc-123">Configurare un [account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) per i dati replicati.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="5c3fc-124">Site Recovery nel portale di Azure può usare gli account di archiviazione configurati in Gestione risorse o in modalità classica.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-124">Site Recovery in the Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="5c3fc-125">L'account di archiviazione può essere Standard o [Premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5c3fc-125">The storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="5c3fc-126">Se si configura un account Premium, sarà necessario anche un altro account Standard per i dati di log.</span><span class="sxs-lookup"><span data-stu-id="5c3fc-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5c3fc-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c3fc-127">Next steps</span></span>

<span data-ttu-id="5c3fc-128">Andare a [Passaggio 6: Configurare un insieme di credenziali](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="5c3fc-128">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
