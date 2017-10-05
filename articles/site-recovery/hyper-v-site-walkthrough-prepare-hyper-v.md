---
title: Preparare gli host Hyper-V (senza System Center VMM) per la replica in Azure | Microsoft Docs
description: Viene descritto come preparare gli host Hyper-V per la replica in Azure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: f9bcaa8e55be6e8fddaf88ebc3f18f5dbb2811e4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-to-azure"></a><span data-ttu-id="c3d32-103">Passaggio 6: Preparare gli host Hyper-V per la replica in Azure</span><span class="sxs-lookup"><span data-stu-id="c3d32-103">Step 6: Prepare Hyper-V hosts for replication to Azure</span></span>

<span data-ttu-id="c3d32-104">Usare le istruzioni riportate in questo articolo per preparare gli host Hyper-V locali per l'interazione con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c3d32-104">Use the instructions in this article to prepare on-premises Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="c3d32-105">Dopo la lettura di questo articolo, è possibile inserire commenti nella parte inferiore oppure porre domande tecniche nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c3d32-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="c3d32-106">Preparare gli host</span><span class="sxs-lookup"><span data-stu-id="c3d32-106">Prepare hosts</span></span>

- <span data-ttu-id="c3d32-107">Assicurarsi che gli host Hyper-V soddisfino i [prerequisiti](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="c3d32-107">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="c3d32-108">Assicurarsi che gli host possano accedere agli URL necessari:</span><span class="sxs-lookup"><span data-stu-id="c3d32-108">Make sure that the hosts can access the required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="c3d32-109">Se sono presenti regole del firewall basate sull'indirizzo IP, verificare che consentano la comunicazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="c3d32-109">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="c3d32-110">Consentire gli [intervalli IP del data center di Azure ](https://www.microsoft.com/download/confirmation.aspx?id=41653) e la porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="c3d32-110">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="c3d32-111">Consentire gli intervalli di indirizzi IP per l'area di Azure della sottoscrizione e per gli Stati Uniti occidentali (usati per il controllo di accesso e la gestione delle identità).</span><span class="sxs-lookup"><span data-stu-id="c3d32-111">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="c3d32-112">Durante la distribuzione di Site Recovery, aggiungere gli host Hyper-V che contengono le VM da replicare in un sito Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c3d32-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want to replicate to a Hyper-V site.</span></span> <span data-ttu-id="c3d32-113">Il provider di Site Recovery e l'agente di Servizi di ripristino sono installati in ogni host.</span><span class="sxs-lookup"><span data-stu-id="c3d32-113">The Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="c3d32-114">Il sito Hyper-V è registrato nell'insieme di credenziali di Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="c3d32-114">The Hyper-V site is registered in the Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3d32-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3d32-115">Next steps</span></span>

<span data-ttu-id="c3d32-116">Andare a [Passaggio 7: Creare un insieme di credenziali](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="c3d32-116">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

