---
title: aaaScale quote e limiti nell'ambiente lab in Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come tooscale un laboratorio di Azure DevTest Labs
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
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="cdfa5-103">Ridimensionare i limiti e le quote in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="cdfa5-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="cdfa5-104">Mentre si lavora in DevTest Labs, è possibile notare che esistono determinati toosome limiti predefinito risorse di Azure, che possono influire sul servizio di DevTest Labs hello.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="cdfa5-105">Questi limiti sono cui tooas **quote**.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="cdfa5-106">servizio di DevTest Labs Hello non imporre le quote.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="cdfa5-107">Le quote che possono verificarsi sono vincoli predefiniti di hello sottoscrizione globale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="cdfa5-108">È possibile usare ogni risorsa di Azure finché non si raggiunge la quota.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="cdfa5-109">Ogni sottoscrizione dispone di quote separate il cui uso viene controllato per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="cdfa5-110">Ad esempio, ogni sottoscrizione ha una quota predefinita di 20 core.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="cdfa5-111">Pertanto, se si siano creano macchine virtuali nel lab con quattro core, è possibile creare solo cinque macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="cdfa5-112">[Sottoscrizione di Azure e limiti dei servizi](https://docs.microsoft.com/azure/azure-subscription-service-limits) vengono elencate alcune delle quote più comuni di hello per le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="cdfa5-113">Hello le risorse usate più di frequente in un ambiente lab e per cui potrebbero verificarsi le quote, includere core VM, gli indirizzi IP pubblici, l'interfaccia di rete, dischi gestiti, assegnazione di ruolo RBAC e circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="cdfa5-114">Visualizzare le quote e l'uso</span><span class="sxs-lookup"><span data-stu-id="cdfa5-114">View your usage and quotas</span></span>
<span data-ttu-id="cdfa5-115">Questi passaggi mostrano come tooview hello quote corrente nella sottoscrizione per le risorse di Azure specifiche e toosee la percentuale di ogni quota utilizzata.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="cdfa5-116">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="cdfa5-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="cdfa5-117">Selezionare **più servizi**, quindi selezionare **fatturazione** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="cdfa5-118">Nel pannello fatturazione hello, selezionare una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="cdfa5-119">Selezionare **Utilizzo e quote**.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-119">Select **Usage + quotas**.</span></span>

   ![Pulsante Utilizzo e quote](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="cdfa5-121">Hello utilizzo + quote pannello verrà visualizzata, varie risorse disponibili in tale sottoscrizione e hello percentuale della quota di hello che viene utilizzato per ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Utilizzo e quote](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="cdfa5-123">Richiesta di altre risorse nella sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="cdfa5-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="cdfa5-124">Se si raggiunge un limite di quota, il limite predefinito hello di una risorsa in una sottoscrizione può essere aumentato di limite massimo tooa, come descritto in [sottoscrizione di Azure e limiti dei servizi](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="cdfa5-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="cdfa5-125">La procedura mostra come toorequest aumentare di una quota tramite hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="cdfa5-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="cdfa5-126">Selezionare **Altri servizi**, quindi **Fatturazione** e **Utilizzo e quote**.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="cdfa5-127">In utilizzo hello + pannello quote, selezionare hello **richiesta aumentare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![Pulsante Richiedi aumento](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="cdfa5-129">toocomplete e inviare la richiesta di hello, immettere le informazioni necessarie hello in tutte e tre le schede di hello **nuova richiesta di assistenza** form.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![Modulo Richiedi aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="cdfa5-131">[Informazioni sui limiti di Azure e di aumentare](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) fornisce ulteriori informazioni su come contattare il supporto di Azure toorequest una quota aumento.</span><span class="sxs-lookup"><span data-stu-id="cdfa5-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="cdfa5-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cdfa5-132">Next steps</span></span>
* <span data-ttu-id="cdfa5-133">Esplorare hello [raccolta di modelli di DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="cdfa5-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
