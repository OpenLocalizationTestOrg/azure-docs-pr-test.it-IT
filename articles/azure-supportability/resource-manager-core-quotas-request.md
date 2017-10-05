---
title: Richieste di aumento della quota di core per Azure Resource Manager | Documentazione Microsoft
description: Richieste di aumento della quota di core per Azure Resource Manager
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="62223-103">Richieste di aumento della quota di core per Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62223-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="62223-104">Le quote di core per Resource Manager sono imposte a livello di area e a livello di famiglia di SKU.</span><span class="sxs-lookup"><span data-stu-id="62223-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="62223-105">Per altre informazioni su come vengono imposte le quote, vedere la pagina relativa ai [limiti del servizio e della sottoscrizione di Azure](http://aka.ms/quotalimits).</span><span class="sxs-lookup"><span data-stu-id="62223-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="62223-106">Per altre informazioni sulle famiglie di SKU e per confrontare costi e prestazioni, vedere la pagina [Prezzi di Macchine virtuali](http://aka.ms/pricingcompute).</span><span class="sxs-lookup"><span data-stu-id="62223-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="62223-107">Per richiedere un aumento, creare una richiesta di supporto per la quota dei core nel portale di Azure, all'indirizzo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="62223-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="62223-108">Informazioni su come [creare una richiesta di supporto](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="62223-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="62223-109">Nella pagina della nuova richiesta di supporto selezionare "Quota" in Tipo di problema e quindi scegliere "Core" in Tipo di quota.</span><span class="sxs-lookup"><span data-stu-id="62223-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![Pannello Informazioni di base della quota](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="62223-111">In Modello di distribuzione selezionare "Resource Manager" e quindi scegliere una località.</span><span class="sxs-lookup"><span data-stu-id="62223-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Pannello Problema della quota](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="62223-113">Selezionare le famiglie di SKU per cui si richiede l'aumento.</span><span class="sxs-lookup"><span data-stu-id="62223-113">Select the SKU Families that require an increase.</span></span>

    ![Serie SKU selezionata](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="62223-115">Immettere i nuovi limiti da applicare alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="62223-115">Enter the new limits you would like on the subscription.</span></span>

    ![Richiesta di nuova quota per lo SKU](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="62223-117">Per rimuovere una riga, deselezionare lo SKU dall'elenco a discesa delle famiglie di SKU oppure fare clic sull'icona di eliminazione "x".</span><span class="sxs-lookup"><span data-stu-id="62223-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="62223-118">Dopo aver immesso la quota desiderata per ogni famiglia di SKU, fare clic su "Avanti" nella pagina del passaggio del problema per procedere con la creazione della richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="62223-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
