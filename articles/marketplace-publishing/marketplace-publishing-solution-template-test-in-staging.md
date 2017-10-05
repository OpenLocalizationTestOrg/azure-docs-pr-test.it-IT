---
title: Test dell'offerta di modello di soluzione per il Marketplace | Documentazione Microsoft
description: Informazioni su come testare l'offerta di modello di soluzione per Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="52b40-103">Test dell'offerta di modello di soluzione in gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="52b40-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="52b40-104">Per gestione temporanea si intende la distribuzione dell'offerta in un ambiente "sandbox" privato, in cui è possibile testarne e verificarne le funzionalità prima di eseguirne il push in produzione.</span><span class="sxs-lookup"><span data-stu-id="52b40-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="52b40-105">L'offerta viene visualizzata nella gestione temporanea esattamente come verrebbe mostrata a un cliente che l'ha distribuita.</span><span class="sxs-lookup"><span data-stu-id="52b40-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="52b40-106">L'offerta deve essere certificata per il push nella gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="52b40-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="52b40-107">Quando l'offerta è in gestione temporanea, è possibile visualizzarla e testarla nel [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="52b40-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="52b40-108">Per il push dell'offerta in gestione temporanea e l'esecuzione del test nel [portale di Azure](https://portal.azure.com/), seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="52b40-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="52b40-109">Passare al [portale di pubblicazione](https://publish.windowsazure.com) >  **scheda Modelli di soluzioni** > la propria offerta > **Pubblica** > **Push in Gestione temporanea**.</span><span class="sxs-lookup"><span data-stu-id="52b40-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="52b40-110">Specificare l'elenco di sottoscrizioni di Azure che verrà usato per la visualizzazione in anteprima e il test dell'offerta.</span><span class="sxs-lookup"><span data-stu-id="52b40-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="52b40-111">Accedere al portale di anteprima di Azure usando l'ID sottoscrizione usato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="52b40-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="52b40-112">Eseguire almeno un ciclo di test nel portale di anteprima di Azure sui punti riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="52b40-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="52b40-113">Assicurarsi che il contenuto di marketing venga visualizzato correttamente in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="52b40-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="52b40-114">Distribuzione end-to-end della topologia.</span><span class="sxs-lookup"><span data-stu-id="52b40-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="52b40-115">Eseguire test delle prestazioni e test di stress.</span><span class="sxs-lookup"><span data-stu-id="52b40-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="52b40-116">Assicurarsi che la topologia sia conforme alle procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="52b40-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52b40-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52b40-117">Next steps</span></span>
<span data-ttu-id="52b40-118">Se si è soddisfatti dei risultati, è possibile procedere alla fase di pubblicazione dell'offerta finale, ovvero il **passaggio 4**: [Distribuzione dell'offerta nel Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="52b40-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="52b40-119">In caso contrario, apportare le modifiche all'offerta e richiedere nuovamente la certificazione.</span><span class="sxs-lookup"><span data-stu-id="52b40-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="52b40-120">Per le modifiche ai contenuti marketing, la certificazione non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="52b40-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="52b40-121">Per una guida a tutte le attività del server di pubblicazione, vedere [Come pubblicare un'offerta in Microsoft Azure Marketplace](marketplace-publishing-getting-started.md) .</span><span class="sxs-lookup"><span data-stu-id="52b40-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>

