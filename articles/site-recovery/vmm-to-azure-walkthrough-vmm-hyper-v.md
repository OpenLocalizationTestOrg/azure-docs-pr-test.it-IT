---
title: aaaPrepare System Center VMM per Hyper-V replica tooAzure | Documenti Microsoft
description: Viene descritto come server di System Center VMM tooprepare per tooAzure di replica Hyper-V, usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="9203f-103">Passaggio 6: Preparare i server VMM e host Hyper-V per Hyper-V replica tooAzure</span><span class="sxs-lookup"><span data-stu-id="9203f-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="9203f-104">Dopo l'impostazione [componenti di Azure](vmm-to-azure-walkthrough-prepare-azure.md) per la distribuzione di hello, utilizzare le istruzioni di hello in questo server VMM locali tooprepare di articolo e toointeract gli host Hyper-V con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9203f-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="9203f-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="9203f-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="9203f-106">Preparare i server VMM</span><span class="sxs-lookup"><span data-stu-id="9203f-106">Prepare VMM servers</span></span>

- <span data-ttu-id="9203f-107">È necessario almeno un server VMM che soddisfano i requisiti di hello supporto per la replica di Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="9203f-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="9203f-108">Assicurarsi che preparato il server VMM hello per [mapping di rete](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="9203f-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="9203f-109">Verificare che il server VMM hello possibile accedere a questi URL</span><span class="sxs-lookup"><span data-stu-id="9203f-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="9203f-110">Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9203f-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="9203f-111">Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="9203f-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="9203f-112">Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).</span><span class="sxs-lookup"><span data-stu-id="9203f-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="9203f-113">Durante la distribuzione di Site Recovery, si scarica hello Provider di Site Recovery e installarlo in ogni server VMM.</span><span class="sxs-lookup"><span data-stu-id="9203f-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="9203f-114">server VMM Hello è registrato nell'insieme di credenziali di servizi di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="9203f-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="9203f-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9203f-115">Next steps</span></span>

<span data-ttu-id="9203f-116">Andare troppo[passaggio 7: creare un insieme di credenziali](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="9203f-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

