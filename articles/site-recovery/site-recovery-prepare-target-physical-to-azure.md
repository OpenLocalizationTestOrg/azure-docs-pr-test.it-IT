---
title: Preparare la destinazione (da fisico ad Azure) | Documentazione Microsoft
description: Questo articolo descrive come preparare l'ambiente di Azure per avviare la replica di server fisici che eseguono Windows o Linux in Azure.
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
ms.openlocfilehash: aa7a32ace8354f615a8b8cc137f6bdf48fbadf48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="5f1cc-103">Preparare la destinazione (da VMware ad Azure)</span><span class="sxs-lookup"><span data-stu-id="5f1cc-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f1cc-104">Da VMware ad Azure</span><span class="sxs-lookup"><span data-stu-id="5f1cc-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="5f1cc-105">Da fisico ad Azure</span><span class="sxs-lookup"><span data-stu-id="5f1cc-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="5f1cc-106">Questo articolo descrive come preparare l'ambiente di Azure per avviare la replica di server fisici (x64) che eseguono Windows o Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="5f1cc-106">This article describes how to prepare your Azure environment to start replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f1cc-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5f1cc-107">Prerequisites</span></span>

<span data-ttu-id="5f1cc-108">In questo articolo si presuppone quanto segue:</span><span class="sxs-lookup"><span data-stu-id="5f1cc-108">The article assumes the following:</span></span>
- <span data-ttu-id="5f1cc-109">È stato creato un insieme di credenziali dei servizi di ripristino per proteggere i server fisici.</span><span class="sxs-lookup"><span data-stu-id="5f1cc-109">You have created a Recovery Services Vault to protect your physical servers.</span></span> <span data-ttu-id="5f1cc-110">È possibile creare un insieme di credenziali di Servizi di ripristino nel [portale di Azure](http://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="5f1cc-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="5f1cc-111">Per replicare i server fisici in Azure, è necessario aver [configurato l'ambiente locale](./site-recovery-set-up-physical-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5f1cc-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) to replicate physical servers to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="5f1cc-112">Preparare la destinazione</span><span class="sxs-lookup"><span data-stu-id="5f1cc-112">Prepare target</span></span>

<span data-ttu-id="5f1cc-113">Dopo aver completato il **Passaggio 1: Selezionare l'obiettivo di protezione** e il **Passaggio 2: Preparare l'origine**, si passa al **Passaggio 3: Destinazione**.</span><span class="sxs-lookup"><span data-stu-id="5f1cc-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Preparare la destinazione](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="5f1cc-115">**Sottoscrizione**: dal menu a discesa selezionare la sottoscrizione nella quale replicare i server fisici.</span><span class="sxs-lookup"><span data-stu-id="5f1cc-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your physical servers to.</span></span>
2. <span data-ttu-id="5f1cc-116">**Modello di distribuzione**: selezionare il modello di distribuzione (classica o di Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="5f1cc-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="5f1cc-117">In base al modello di distribuzione scelto, viene eseguita una convalida per verificare di avere almeno un account di archiviazione compatibile e una rete virtuale nella sottoscrizione di destinazione in cui vengono eseguiti replica e failover dei server fisici.</span><span class="sxs-lookup"><span data-stu-id="5f1cc-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your physical servers to.</span></span>

<span data-ttu-id="5f1cc-118">Dopo aver completato la convalida, fare clic su OK per andare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="5f1cc-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="5f1cc-119">Se non si dispone di un account di archiviazione di Resource Manager o di una rete virtuale compatibile o se si vuole aggiungerne altri, fare clic sui pulsanti **+ Account di archiviazione** o **+ Rete** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="5f1cc-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f1cc-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f1cc-120">Next steps</span></span>
<span data-ttu-id="5f1cc-121">[Configurare le impostazioni di replica](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="5f1cc-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
