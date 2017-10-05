---
title: Preparare System Center VMM per la replica Hyper-V in Azure | Microsoft Docs
description: Illustra come preparare un server System Center VMM per la replica Hyper-V in Azure tramite Azure Site Recovery
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
ms.openlocfilehash: ec118ed837dbf140083b3ae1e4ecd41c81562018
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-to-azure"></a><span data-ttu-id="ad3bc-103">Passaggio 6: Preparare i server VMM e gli host Hyper-V per la replica Hyper-V in Azure</span><span class="sxs-lookup"><span data-stu-id="ad3bc-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication to Azure</span></span>

<span data-ttu-id="ad3bc-104">Al termine della configurazione dei [componenti di Azure](vmm-to-azure-walkthrough-prepare-azure.md) per la distribuzione, usare le istruzioni disponibili in questo articolo per preparare i server VMM locali e gli host Hyper-V per l'interazione con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ad3bc-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for the deployment, use the instructions in this article to prepare on-premises VMM servers and Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="ad3bc-105">Dopo la lettura di questo articolo, è possibile inserire commenti nella parte inferiore oppure porre domande tecniche nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ad3bc-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="ad3bc-106">Preparare i server VMM</span><span class="sxs-lookup"><span data-stu-id="ad3bc-106">Prepare VMM servers</span></span>

- <span data-ttu-id="ad3bc-107">È necessario almeno un server VMM che soddisfi i requisiti di supporto per la replica tramite Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="ad3bc-107">You need at least one VMM server that meet the support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="ad3bc-108">Assicurarsi di avere preparato il server VMM per il [mapping di rete](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="ad3bc-108">Make sure you've prepared the VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="ad3bc-109">Assicurarsi che il server VMM possa accedere a questi URL</span><span class="sxs-lookup"><span data-stu-id="ad3bc-109">Make sure that the VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="ad3bc-110">Se sono presenti regole del firewall basate sull'indirizzo IP, verificare che consentano la comunicazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="ad3bc-110">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="ad3bc-111">Consentire gli [intervalli IP del data center di Azure ](https://www.microsoft.com/download/confirmation.aspx?id=41653) e la porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="ad3bc-111">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="ad3bc-112">Consentire gli intervalli di indirizzi IP per l'area di Azure della sottoscrizione e per gli Stati Uniti occidentali (usati per il controllo di accesso e la gestione delle identità).</span><span class="sxs-lookup"><span data-stu-id="ad3bc-112">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="ad3bc-113">Durante la distribuzione di Site Recovery, il provider di Site Recovery viene scaricato e installato in ogni server VMM.</span><span class="sxs-lookup"><span data-stu-id="ad3bc-113">During Site Recovery deployment, you download the Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="ad3bc-114">Il server VMM è registrato nell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ad3bc-114">The VMM server is registered in the Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="ad3bc-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad3bc-115">Next steps</span></span>

<span data-ttu-id="ad3bc-116">Andare a [Passaggio 7: Creare un insieme di credenziali](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="ad3bc-116">Go to [Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

