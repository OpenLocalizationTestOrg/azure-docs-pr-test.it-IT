---
title: Ridimensionare i limiti e le quote nel lab in Azure DevTest Labs | Microsoft Docs
description: Informazioni su come ridimensionare un lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="fe333-103">Ridimensionare i limiti e le quote in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fe333-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="fe333-104">Quando si lavora in DevTest Labs, è possibile notare che esistono limiti predefiniti per determinate le risorse di Azure, che possono influenzare il servizio DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="fe333-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="fe333-105">Questi limiti sono definiti **quote**.</span><span class="sxs-lookup"><span data-stu-id="fe333-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="fe333-106">Il servizio DevTest Labs non impone le quote.</span><span class="sxs-lookup"><span data-stu-id="fe333-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="fe333-107">Le quote che gli utenti notano sono vincoli predefiniti di tutta la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe333-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="fe333-108">È possibile usare ogni risorsa di Azure finché non si raggiunge la quota.</span><span class="sxs-lookup"><span data-stu-id="fe333-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="fe333-109">Ogni sottoscrizione dispone di quote separate il cui uso viene controllato per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fe333-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="fe333-110">Ad esempio, ogni sottoscrizione ha una quota predefinita di 20 core.</span><span class="sxs-lookup"><span data-stu-id="fe333-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="fe333-111">Pertanto, se si siano creano macchine virtuali nel lab con quattro core, è possibile creare solo cinque macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fe333-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="fe333-112">[Sottoscrizione di Azure e limiti dei servizi](https://docs.microsoft.com/azure/azure-subscription-service-limits) elenca alcune delle quote più comuni per le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="fe333-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="fe333-113">Le risorse più comunemente usate in un lab e per cui è possibile che ci siano quote, includono i core di una macchina virtuale, gli indirizzi IP pubblici, l'interfaccia di rete, i dischi gestiti, l'assegnazione di ruoli controllo degli accessi in base al ruolo e i circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe333-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="fe333-114">Visualizzare le quote e l'uso</span><span class="sxs-lookup"><span data-stu-id="fe333-114">View your usage and quotas</span></span>
<span data-ttu-id="fe333-115">Questa procedura illustra come visualizzare le quote correnti nella sottoscrizione per risorse specifiche di Azure e per visualizzare la percentuale di ogni quota usata.</span><span class="sxs-lookup"><span data-stu-id="fe333-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="fe333-116">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fe333-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="fe333-117">Selezionare **Altri servizi** e quindi **Fatturazione** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="fe333-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="fe333-118">Selezionare una sottoscrizione nel pannello Fatturazione.</span><span class="sxs-lookup"><span data-stu-id="fe333-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="fe333-119">Selezionare **Utilizzo e quote**.</span><span class="sxs-lookup"><span data-stu-id="fe333-119">Select **Usage + quotas**.</span></span>

   ![Pulsante Utilizzo e quote](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="fe333-121">Viene visualizzato il pannello Utilizzo e quote che elenca le varie risorse disponibili nella sottoscrizione e la percentuale della quota usata per ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="fe333-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![Utilizzo e quote](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="fe333-123">Richiesta di altre risorse nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="fe333-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="fe333-124">Se si raggiunge un limite di quota, il limite predefinito di una risorsa in una sottoscrizione può essere aumentato fino a un limite massimo, come descritto in [Sottoscrizione di Azure e limiti dei servizi](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="fe333-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="fe333-125">Questa procedura mostra come richiedere un aumento di quota usando il [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fe333-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="fe333-126">Selezionare **Altri servizi**, quindi **Fatturazione** e **Utilizzo e quote**.</span><span class="sxs-lookup"><span data-stu-id="fe333-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="fe333-127">Nel pannello Utilizzo + quote selezionare il pulsante **Richiedi aumento**.</span><span class="sxs-lookup"><span data-stu-id="fe333-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![Pulsante Richiedi aumento](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="fe333-129">Per completare e inviare la richiesta, inserire le informazioni necessarie sulle tre schede del modulo **Nuova richiesta di supporto**.</span><span class="sxs-lookup"><span data-stu-id="fe333-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![Modulo Richiedi aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="fe333-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) (Informazioni sui limiti e gli aumenti di Azure) contiene altre informazioni su come contattare il supporto di Azure per richiedere un aumento della quota.</span><span class="sxs-lookup"><span data-stu-id="fe333-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="fe333-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe333-132">Next steps</span></span>
* <span data-ttu-id="fe333-133">Esplorare la [raccolta dei modelli di avvio rapido di Azure Resource Manager di DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="fe333-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
