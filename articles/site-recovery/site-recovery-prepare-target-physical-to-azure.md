---
title: Preparazione di destinazione (tooAzure fisico) | Documenti Microsoft
description: Questo articolo viene descritto come tooprepare toostart l'ambiente Azure la replica di server fisici che eseguono tooAzure Windows o Linux.
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
ms.openlocfilehash: 126fb86133e1a00f5669410943565c4cd78e4369
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="e3120-103">Preparazione di destinazione (tooAzure VMware)</span><span class="sxs-lookup"><span data-stu-id="e3120-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3120-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="e3120-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="e3120-105">TooAzure fisico</span><span class="sxs-lookup"><span data-stu-id="e3120-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="e3120-106">Questo articolo viene descritto come tooprepare toostart l'ambiente Azure la replica di server fisici (x64) in esecuzione Windows o Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="e3120-106">This article describes how tooprepare your Azure environment toostart replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3120-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e3120-107">Prerequisites</span></span>

<span data-ttu-id="e3120-108">Hello presume seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e3120-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="e3120-109">È stato creato un archivio di servizi di ripristino di tooprotect i server fisici.</span><span class="sxs-lookup"><span data-stu-id="e3120-109">You have created a Recovery Services Vault tooprotect your physical servers.</span></span> <span data-ttu-id="e3120-110">È possibile creare un insieme di credenziali di servizi di ripristino da hello [portale di Azure](http://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="e3120-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="e3120-111">Hai [configurare l'ambiente locale](./site-recovery-set-up-physical-to-azure.md) tooreplicate tooAzure di server fisici.</span><span class="sxs-lookup"><span data-stu-id="e3120-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) tooreplicate physical servers tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="e3120-112">Preparare la destinazione</span><span class="sxs-lookup"><span data-stu-id="e3120-112">Prepare target</span></span>

<span data-ttu-id="e3120-113">Dopo aver completato hello **obiettivi della protezione dati passaggio 1: selezionare** e **passaggio 2: preparare origine**, si passa troppo**passaggio 3: destinazione**</span><span class="sxs-lookup"><span data-stu-id="e3120-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![Preparare la destinazione](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. <span data-ttu-id="e3120-115">**Sottoscrizione:** da hello menu a discesa, seleziona hello sottoscrizione che si desidera tooreplicate i server fisici.</span><span class="sxs-lookup"><span data-stu-id="e3120-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your physical servers to.</span></span>
2. <span data-ttu-id="e3120-116">**Modello di distribuzione:** modello di distribuzione selezionare hello (versione classica o Gestione risorse)</span><span class="sxs-lookup"><span data-stu-id="e3120-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="e3120-117">In base al modello di distribuzione scelto hello, una convalida viene eseguita tooensure che occorre almeno un account di archiviazione compatibile e la rete virtuale in tooreplicate sottoscrizione di destinazione hello e il failover dei server fisici per.</span><span class="sxs-lookup"><span data-stu-id="e3120-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your physical servers to.</span></span>

<span data-ttu-id="e3120-118">Una volta completate le convalide hello, fare clic su OK toogo toohello successivo passaggio.</span><span class="sxs-lookup"><span data-stu-id="e3120-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="e3120-119">Se si non dispone di un account di archiviazione compatibile di gestione delle risorse o una rete virtuale o si desidera tooadd altre, è possibile farlo facendo hello **+ Account di archiviazione** o **+ rete** pulsanti nella parte superiore di hello di hello pannello.</span><span class="sxs-lookup"><span data-stu-id="e3120-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3120-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3120-120">Next steps</span></span>
<span data-ttu-id="e3120-121">[Configurare le impostazioni di replica](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="e3120-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
