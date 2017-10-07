---
title: aaaView hello mensile stimato del lab tendenza dei costi in Azure DevTest Labs | Documenti Microsoft
description: Informazioni sul grafico di tendenza mensile costo stimato di hello Azure DevTest Labs.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="a31f7-103">Visualizzazione hello mensile stimato del lab tendenza dei costi in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a31f7-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="a31f7-104">funzionalità di gestione dei costi Hello di DevTest Labs consente di tenere traccia dei costi di hello del lab.</span><span class="sxs-lookup"><span data-stu-id="a31f7-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="a31f7-105">Questo articolo illustra come hello toouse **mensile tendenza costo stimato** tooview grafico hello stimato costo-to-date del mese di calendario corrente e hello costo del mese di fine per hello mese di calendario corrente.</span><span class="sxs-lookup"><span data-stu-id="a31f7-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="a31f7-106">In questo articolo viene illustrato come tooview hello grafico di tendenza mensile costo stimato in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a31f7-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="a31f7-107">Visualizzazione grafico di tendenza di costo stimato mensile hello</span><span class="sxs-lookup"><span data-stu-id="a31f7-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="a31f7-108">hello tooview grafico di tendenza di costo stimato mensile, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a31f7-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="a31f7-109">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a31f7-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="a31f7-110">Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="a31f7-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="a31f7-111">Elenco dei laboratori hello selezionare lab desiderato hello.</span><span class="sxs-lookup"><span data-stu-id="a31f7-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="a31f7-112">Nel pannello del lab hello, selezionare **costo impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="a31f7-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="a31f7-113">Nel lab di hello **costo impostazioni** pannello seleziona **Lab costo tendenza**.</span><span class="sxs-lookup"><span data-stu-id="a31f7-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="a31f7-114">Hello schermata riportata di seguito viene illustrato un esempio di un grafico di costo.</span><span class="sxs-lookup"><span data-stu-id="a31f7-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![Grafico dei costi](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="a31f7-116">Hello **costo stimato** valore è hello stimato costo-to-date del mese di calendario corrente.</span><span class="sxs-lookup"><span data-stu-id="a31f7-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="a31f7-117">Hello **costo previsto** hello costo stimato per hello intero mese di calendario corrente, calcolato utilizzando costo lab hello per hello cinque giorni precedenti.</span><span class="sxs-lookup"><span data-stu-id="a31f7-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="a31f7-118">gli importi di costo Hello vengono arrotondati toohello successivo numero intero.</span><span class="sxs-lookup"><span data-stu-id="a31f7-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="a31f7-119">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a31f7-119">For example:</span></span> 

* <span data-ttu-id="a31f7-120">5.01 Arrotonda too6</span><span class="sxs-lookup"><span data-stu-id="a31f7-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="a31f7-121">5,50 Arrotonda too6</span><span class="sxs-lookup"><span data-stu-id="a31f7-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="a31f7-122">5.99 Arrotonda too6</span><span class="sxs-lookup"><span data-stu-id="a31f7-122">5.99 rounds up too6</span></span>

<span data-ttu-id="a31f7-123">, Come indicato sopra il grafico hello costi hello viene visualizzato nel grafico hello sono *stimato* costi utilizzando [consumo](https://azure.microsoft.com/offers/ms-azr-0003p/) offrono tariffe.</span><span class="sxs-lookup"><span data-stu-id="a31f7-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="a31f7-124">Sono inoltre seguente hello *non* incluso nel calcolo del costo hello:</span><span class="sxs-lookup"><span data-stu-id="a31f7-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="a31f7-125">CSP e Dreamspark sottoscrizioni attualmente non sono supportate in Azure DevTest Labs utilizza hello [Azure API fatturazione](../billing/billing-usage-rate-card-overview.md) lab hello toocalculate costo, che non supporta le sottoscrizioni Dreamspark o di CSP.</span><span class="sxs-lookup"><span data-stu-id="a31f7-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="a31f7-126">Le tariffe della propria offerta.</span><span class="sxs-lookup"><span data-stu-id="a31f7-126">Your offer rates.</span></span> <span data-ttu-id="a31f7-127">Attualmente, non è in grado di toouse (mostrate sotto della sottoscrizione) che hanno negoziate con Microsoft o Microsoft partner per le tariffe di offerta.</span><span class="sxs-lookup"><span data-stu-id="a31f7-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="a31f7-128">Vengono usate tariffe a consumo.</span><span class="sxs-lookup"><span data-stu-id="a31f7-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="a31f7-129">Le imposte</span><span class="sxs-lookup"><span data-stu-id="a31f7-129">Your taxes</span></span>
* <span data-ttu-id="a31f7-130">Gli sconti</span><span class="sxs-lookup"><span data-stu-id="a31f7-130">Your discounts</span></span>
* <span data-ttu-id="a31f7-131">La valuta di fatturazione</span><span class="sxs-lookup"><span data-stu-id="a31f7-131">Your billing currency.</span></span> <span data-ttu-id="a31f7-132">Attualmente, il costo di lab hello viene visualizzato solo nella valuta USD.</span><span class="sxs-lookup"><span data-stu-id="a31f7-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="a31f7-133">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="a31f7-133">Related blog posts</span></span>
* [<span data-ttu-id="a31f7-134">Due altre tookeep di operazioni dei costi in modo corretto in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a31f7-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="a31f7-135">Why Cost Thresholds? (Perché usare le soglie dei costi?)</span><span class="sxs-lookup"><span data-stu-id="a31f7-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="a31f7-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a31f7-136">Next steps</span></span>
<span data-ttu-id="a31f7-137">Ecco alcuni aspetti tootry accanto:</span><span class="sxs-lookup"><span data-stu-id="a31f7-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="a31f7-138">[Definire i criteri di lab](devtest-lab-set-lab-policy.md) -informazioni su come tooset hello vari criteri utilizzati toogovern come vengono usati nel lab e delle relative macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="a31f7-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="a31f7-139">[Creare un'immagine personalizzata](devtest-lab-create-template.md): quando si crea una VM, si specifica una base, che può essere un'immagine personalizzata o un'immagine del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a31f7-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="a31f7-140">Questo articolo illustra come toocreate immagine personalizzata da un file VHD.</span><span class="sxs-lookup"><span data-stu-id="a31f7-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="a31f7-141">[Configurare le immagini del Marketplace](devtest-lab-configure-marketplace-images.md): DevTest Labs supporta la creazione di VM basate su immagini di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a31f7-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="a31f7-142">Questo articolo illustra come toospecify che, se presente, le immagini di Azure Marketplace possono essere utilizzati durante la creazione di macchine virtuali in un ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="a31f7-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="a31f7-143">[Creare una macchina virtuale in un ambiente lab](devtest-lab-add-vm-with-artifacts.md) -illustra come toocreate una macchina virtuale da un'immagine di base (entrambi personalizzato o Marketplace) e come toowork con gli elementi di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a31f7-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

