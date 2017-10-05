---
title: Preparare la destinazione (da VMware ad Azure) | Documentazione Microsoft
description: Questo articolo descrive come preparare l'ambiente Azure per avviare la replica di macchine virtuali VMware in Azure.
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: c84a775564769ddc796aa9d75add019ef1003175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="3aea9-103">Preparare la destinazione (da VMware ad Azure)</span><span class="sxs-lookup"><span data-stu-id="3aea9-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3aea9-104">Da VMware ad Azure</span><span class="sxs-lookup"><span data-stu-id="3aea9-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="3aea9-105">Da fisico ad Azure</span><span class="sxs-lookup"><span data-stu-id="3aea9-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="3aea9-106">Questo articolo descrive come preparare l'ambiente Azure per avviare la replica di macchine virtuali VMware in Azure.</span><span class="sxs-lookup"><span data-stu-id="3aea9-106">This article describes how to prepare your Azure environment to start replicating VMware virtual machines to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3aea9-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3aea9-107">Prerequisites</span></span>

<span data-ttu-id="3aea9-108">In questo articolo si presuppone quanto segue:</span><span class="sxs-lookup"><span data-stu-id="3aea9-108">The article assumes the following:</span></span>
- <span data-ttu-id="3aea9-109">È stato creato un insieme di credenziali di Servizi di ripristino per proteggere le macchine virtuali VMware.</span><span class="sxs-lookup"><span data-stu-id="3aea9-109">You have created a Recovery Services Vault to protect your VMware virtual machines.</span></span> <span data-ttu-id="3aea9-110">È possibile creare un insieme di credenziali di Servizi di ripristino nel [portale di Azure](http://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="3aea9-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="3aea9-111">Per replicare le macchine virtuali VMware in Azure, è necessario avere [configurato l'ambiente locale](./site-recovery-set-up-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="3aea9-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) to replicate VMware virtual machines to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="3aea9-112">Preparare la destinazione</span><span class="sxs-lookup"><span data-stu-id="3aea9-112">Prepare target</span></span>

<span data-ttu-id="3aea9-113">Dopo aver completato il **Passaggio 1: Selezionare l'obiettivo di protezione** e il **Passaggio 2: Preparare l'origine**, si passa al **Passaggio 3: Destinazione**.</span><span class="sxs-lookup"><span data-stu-id="3aea9-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Preparare la destinazione](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="3aea9-115">**Sottoscrizione**: nel menu a discesa selezionare la sottoscrizione nella quale replicare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="3aea9-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your virtual machines to.</span></span>
2. <span data-ttu-id="3aea9-116">**Modello di distribuzione**: selezionare il modello di distribuzione (classica o di Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="3aea9-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="3aea9-117">In base al modello di distribuzione scelto, viene eseguita una convalida per verificare di avere almeno un account di archiviazione e una rete virtuale compatibili nella sottoscrizione di destinazione in cui vengono eseguiti replica e failover della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3aea9-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your virtual machine to.</span></span>

<span data-ttu-id="3aea9-118">Dopo aver completato la convalida, fare clic su OK per andare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="3aea9-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="3aea9-119">Se non si dispone di un account di archiviazione di Resource Manager o di una rete virtuale compatibile o se si vuole aggiungerne altri, fare clic sui pulsanti **+ Account di archiviazione** o **+ Rete** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="3aea9-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aea9-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3aea9-120">Next steps</span></span>
<span data-ttu-id="3aea9-121">[Configurare le impostazioni di replica](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="3aea9-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
