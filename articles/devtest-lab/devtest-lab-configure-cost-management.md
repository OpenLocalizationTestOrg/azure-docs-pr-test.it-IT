---
title: Visualizzare la tendenza dei costi mensili stimati per il lab in Azure DevTest Labs | Documentazione Microsoft
description: Informazioni sul grafico relativo alla tendenza dei costi mensili stimati di Azure DevTest Labs.
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
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="1d9a7-103">Visualizzare la tendenza dei costi mensili stimati per il lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1d9a7-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="1d9a7-104">La funzionalità di gestione dei costi dei lab di sviluppo/test consente di tenere traccia dei costi del lab.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="1d9a7-105">Questo articolo spiega come usare il grafico della **tendenza dei costi mensili stimati** grafico per visualizzare i costi stimati del mese in corso fino alla data odierna e la proiezione dell'ammontare dei costi a fine mese per il mese in corso.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="1d9a7-106">Questo articolo illustra come visualizzare il grafico della tendenza dei costo mensili stimati nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="1d9a7-107">Visualizzazione del grafico della tendenza dei costi mensili stimati</span><span class="sxs-lookup"><span data-stu-id="1d9a7-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="1d9a7-108">Per visualizzare il grafico della tendenza dei costi mensili stimati, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d9a7-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="1d9a7-109">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="1d9a7-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="1d9a7-110">Selezionare **Altri servizi** e quindi **DevTest Labs** dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="1d9a7-111">Nell'elenco dei lab selezionare il lab desiderato.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="1d9a7-112">Nel pannello del lab, selezionare **Cost settings**(Impostazioni dei costi).</span><span class="sxs-lookup"><span data-stu-id="1d9a7-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="1d9a7-113">Nel pannello **Impostazioni dei costi** del lab selezionare **Tendenza costo lab**.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="1d9a7-114">La schermata seguente illustra un esempio di grafico dei costi.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Grafico dei costi](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="1d9a7-116">Il valore del **Costo stimato** corrisponde al costo attualmente stimato per il mese di calendario corrente.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="1d9a7-117">Il **Costo previsto** corrisponde al costo stimato per l'intero mese di calendario corrente, calcolato sulla base del costo del lab dei cinque giorni precedenti.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="1d9a7-118">Gli importi vengono arrotondati al numero intero successivo.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="1d9a7-119">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1d9a7-119">For example:</span></span> 

* <span data-ttu-id="1d9a7-120">5,01 arrotondato a 6</span><span class="sxs-lookup"><span data-stu-id="1d9a7-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="1d9a7-121">5,50 arrotondato a 6</span><span class="sxs-lookup"><span data-stu-id="1d9a7-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="1d9a7-122">5,99 arrotondato a 6</span><span class="sxs-lookup"><span data-stu-id="1d9a7-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="1d9a7-123">Come indicato sopra il grafico, i costi visualizzati nel grafico sono costi *stimati* in base alle tariffe del piano di [pagamento a consumo](https://azure.microsoft.com/offers/ms-azr-0003p/) .</span><span class="sxs-lookup"><span data-stu-id="1d9a7-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="1d9a7-124">Il calcolo dei costi *non* include quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1d9a7-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="1d9a7-125">Le sottoscrizioni CSP e Dreamspark non sono attualmente supportate in quanto, per calcolare il costo del lab, Azure DevTest Labs usa le [API di fatturazione di Azure](../billing/billing-usage-rate-card-overview.md) , che non supportano le sottoscrizioni CSP o Dreamspark.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="1d9a7-126">Le tariffe della propria offerta.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-126">Your offer rates.</span></span> <span data-ttu-id="1d9a7-127">Al momento non è possibile includere le tariffe, indicate nella sottoscrizione, negoziate con Microsoft o i partner Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="1d9a7-128">Vengono usate tariffe a consumo.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="1d9a7-129">Le imposte</span><span class="sxs-lookup"><span data-stu-id="1d9a7-129">Your taxes</span></span>
* <span data-ttu-id="1d9a7-130">Gli sconti</span><span class="sxs-lookup"><span data-stu-id="1d9a7-130">Your discounts</span></span>
* <span data-ttu-id="1d9a7-131">La valuta di fatturazione</span><span class="sxs-lookup"><span data-stu-id="1d9a7-131">Your billing currency.</span></span> <span data-ttu-id="1d9a7-132">Al momento i costi del lab vengono visualizzati solo in USD.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="1d9a7-133">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="1d9a7-133">Related blog posts</span></span>
* [<span data-ttu-id="1d9a7-134">Two more things to keep your cost on track in DevTest Labs (Altri due suggerimenti per contenere i costi in DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="1d9a7-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="1d9a7-135">Why Cost Thresholds? (Perché usare le soglie dei costi?)</span><span class="sxs-lookup"><span data-stu-id="1d9a7-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="1d9a7-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d9a7-136">Next steps</span></span>
<span data-ttu-id="1d9a7-137">Altre operazioni da eseguire:</span><span class="sxs-lookup"><span data-stu-id="1d9a7-137">Here are some things to try next:</span></span>

* <span data-ttu-id="1d9a7-138">[Definire i criteri del lab](devtest-lab-set-lab-policy.md): impostare i vari criteri che consentono di gestire il modo in cui vengono usati il lab e le relative VM.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="1d9a7-139">[Creare un'immagine personalizzata](devtest-lab-create-template.md): quando si crea una VM, si specifica una base, che può essere un'immagine personalizzata o un'immagine del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="1d9a7-140">Questo articolo illustra come creare un'immagine personalizzata da un file VHD.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="1d9a7-141">[Configurare le immagini del Marketplace](devtest-lab-configure-marketplace-images.md): DevTest Labs supporta la creazione di VM basate su immagini di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="1d9a7-142">Questo articolo illustra come specificare eventuali immagini di Azure Marketplace da usare durante la creazione di VM in un lab.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="1d9a7-143">[Creare una VM in un lab](devtest-lab-add-vm-with-artifacts.md): questo articolo illustra come creare una VM da un'immagine di base, personalizzata o del Marketplace, e come usare gli elementi nella VM.</span><span class="sxs-lookup"><span data-stu-id="1d9a7-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

