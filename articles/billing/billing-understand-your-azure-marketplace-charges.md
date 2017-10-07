---
title: aaaUnderstand costi di servizio esterni Azure | Documenti Microsoft
description: Informazioni sulla fatturazione di servizi esterni, noti in precedenza come Marketplace, in Azure.
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="49dff-103">Informazioni sulla fatturazione di Azure per gli addebiti dei servizi esterni</span><span class="sxs-lookup"><span data-stu-id="49dff-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="49dff-104">Servizi esterni utilizzati toobe chiamato Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="49dff-104">External services used toobe called Azure Marketplace.</span></span> <span data-ttu-id="49dff-105">Si tratta in genere di servizi pubblicati da terze parti disponibili per Azure, ma integrati completamente in Azure.</span><span class="sxs-lookup"><span data-stu-id="49dff-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="49dff-106">Ad esempio, ClearDB e SendGrid sono servizi esterni che è possibile acquistare in Azure, ma che non vengono pubblicati da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="49dff-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="49dff-107">Durante il provisioning di un nuovo servizio esterno o di una nuova risorsa, viene visualizzato un avviso:</span><span class="sxs-lookup"><span data-stu-id="49dff-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Avviso di acquisto di Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="49dff-109">I servizi esterni vengono pubblicati da società non Microsoft, ma talvolta anche i prodotti Microsoft sono classificati come servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="49dff-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="49dff-110">Modalità di fatturazione dei servizi esterni</span><span class="sxs-lookup"><span data-stu-id="49dff-110">How external services are billed</span></span>
- <span data-ttu-id="49dff-111">I servizi esterni vengono fatturati separatamente.</span><span class="sxs-lookup"><span data-stu-id="49dff-111">External services are billed separately.</span></span> <span data-ttu-id="49dff-112">Vengono gestiti come ordini singoli all'interno della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="49dff-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="49dff-113">periodo di fatturazione Hello per ogni servizio è impostato al momento dell'acquisto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="49dff-113">hello billing period for each service is set when you purchase hello service.</span></span> <span data-ttu-id="49dff-114">Non i toobe confusa con periodo di fatturazione della sottoscrizione hello in cui è stato acquistato hello.</span><span class="sxs-lookup"><span data-stu-id="49dff-114">Not toobe confused with hello billing period of hello subscription under which you purchased it.</span></span> <span data-ttu-id="49dff-115">Si ricevono anche fatture separate e l'addebito sulla carta di credito viene applicato separatamente.</span><span class="sxs-lookup"><span data-stu-id="49dff-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="49dff-116">Per ogni servizio esterno è previsto un modello di fatturazione diverso.</span><span class="sxs-lookup"><span data-stu-id="49dff-116">Each external service has a different billing model.</span></span> <span data-ttu-id="49dff-117">Alcuni servizi vengono fatturati con pagamento in base al consumo, mentre altri prevedono un modello di pagamento su base mensile.</span><span class="sxs-lookup"><span data-stu-id="49dff-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="49dff-118">Per i servizi esterni di Azure è necessaria una carta di credito e non è possibile pagare tramite fattura.</span><span class="sxs-lookup"><span data-stu-id="49dff-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="49dff-119">Non è possibile usare i crediti gratuiti mensili per i servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="49dff-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="49dff-120">Se si utilizza una sottoscrizione di Azure che include [libero crediti](https://azure.microsoft.com/pricing/spending-limits/), non possono essere applicati tooexternal servizio distinte.</span><span class="sxs-lookup"><span data-stu-id="49dff-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied tooexternal service bills.</span></span> <span data-ttu-id="49dff-121">Utilizzare i servizi esterni di toopurchase una carta di credito.</span><span class="sxs-lookup"><span data-stu-id="49dff-121">Use a credit card toopurchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a><span data-ttu-id="49dff-122">Uso dei servizi esterni di visualizzazione e la cronologia nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="49dff-122">View external service spending and history in hello Azure portal</span></span>
<span data-ttu-id="49dff-123">È possibile visualizzare un elenco di servizi esterni hello in ogni sottoscrizione all'interno di hello [portale di Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="49dff-123">You can view a list of hello external services that are on each subscription within hello [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="49dff-124">Accedi toohello [portale di Azure](https://portal.azure.com/) come amministratore dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="49dff-124">Sign in toohello [Azure portal](https://portal.azure.com/) as hello account administrator.</span></span>
2. <span data-ttu-id="49dff-125">Nel menu Hub hello, selezionare **sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="49dff-125">In hello Hub menu, select **Subscriptions**.</span></span>
   
    ![Selezionare le sottoscrizioni nel menu Hub hello](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="49dff-127">In hello **sottoscrizioni** blade, sottoscrizione selezionare hello desidera tooview e quindi selezionare **servizi esterni**.</span><span class="sxs-lookup"><span data-stu-id="49dff-127">In hello **Subscriptions** blade, select hello subscription that you want tooview, and then select **External services**.</span></span>
   
    ![Selezionare una sottoscrizione nel pannello fatturazione hello](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="49dff-129">Si dovrebbero apparire gli ordini di servizio esterno, il nome di server di pubblicazione hello, il livello di servizio che è stato acquistato, nome assegnato alla risorsa hello e lo stato dell'ordine corrente hello.</span><span class="sxs-lookup"><span data-stu-id="49dff-129">You should see each of your external service orders, hello publisher name, service tier you bought, name you gave hello resource, and hello current order status.</span></span> <span data-ttu-id="49dff-130">toosee oltre distinte, selezionare un servizio esterno.</span><span class="sxs-lookup"><span data-stu-id="49dff-130">toosee past bills, select an external service.</span></span>
   
    ![Selezionare un servizio esterno](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="49dff-132">Da qui è possibile visualizzare oltre gli importi degli effetti inclusi dettagli imposte hello.</span><span class="sxs-lookup"><span data-stu-id="49dff-132">From here, you can view past bill amounts including hello tax breakdown.</span></span>
   
    ![Visualizzare la cronologia di fatturazione dei servizi esterni](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="49dff-134">Visualizzare la spesa dei servizi esterni per i clienti con contratto Enterprise (EA, Enterprise Agreement)</span><span class="sxs-lookup"><span data-stu-id="49dff-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="49dff-135">I clienti EA vedere spesa servizio esterno e scaricare i report nel portale di hello EA.</span><span class="sxs-lookup"><span data-stu-id="49dff-135">EA customers can see external service spending and download reports in hello EA portal.</span></span> <span data-ttu-id="49dff-136">Vedere [Azure Marketplace per i clienti EA](https://ea.azure.com/helpdocs/azureMarketplace) tooget avviato.</span><span class="sxs-lookup"><span data-stu-id="49dff-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) tooget started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="49dff-137">Gestire i metodi di pagamento per gli ordini di servizi esterni</span><span class="sxs-lookup"><span data-stu-id="49dff-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="49dff-138">Aggiornare i metodi di pagamento per gli ordini di servizio esterno da hello [centro Account](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="49dff-138">Update your payment methods for external service orders from hello [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="49dff-139">Se è stata acquistata una sottoscrizione con un account aziendale o dell'istituto di istruzione, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake Modifica metodo di pagamento tooyour.</span><span class="sxs-lookup"><span data-stu-id="49dff-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake changes tooyour payment method.</span></span>
> 
> 

1. <span data-ttu-id="49dff-140">Accedi toohello [centro Account](https://account.windowsazure.com/) e [passare toohello **marketplace** scheda](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="49dff-140">Sign in toohello [Account Center](https://account.windowsazure.com/) and [navigate toohello **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Selezionare marketplace nel centro account hello](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="49dff-142">Selezionare hello esterno servizio toomanage</span><span class="sxs-lookup"><span data-stu-id="49dff-142">Select hello external service you want toomanage</span></span>
   
    ![Selezionare hello esterno servizio toomanage](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="49dff-144">Fare clic su **modificare il metodo di pagamento** hello destra della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="49dff-144">Click **Change payment method** on hello right side of hello page.</span></span> <span data-ttu-id="49dff-145">Questo collegamento consente di visualizzare è tooa diversi portale toomanage il metodo di pagamento.</span><span class="sxs-lookup"><span data-stu-id="49dff-145">This link brings you tooa different portal toomanage your payment method.</span></span>
   
    ![Riepilogo degli ordini](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="49dff-147">Fare clic su **Modifica informazioni** e seguire le istruzioni tooupdate le informazioni di pagamento.</span><span class="sxs-lookup"><span data-stu-id="49dff-147">Click **Edit info** and follow instructions tooupdate your payment information.</span></span>
   
    ![Selezionare Modifica informazioni](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="49dff-149">Annullare un ordine di servizio esterno</span><span class="sxs-lookup"><span data-stu-id="49dff-149">Cancel an external service order</span></span>
<span data-ttu-id="49dff-150">Se si desidera toocancel l'ordine di servizio esterno, eliminare la risorsa hello in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="49dff-150">If you want toocancel your external service order, delete hello resource in hello [Azure portal](https://portal.azure.com).</span></span>

![Eliminare una risorsa](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="49dff-152">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="49dff-152">Need help?</span></span> <span data-ttu-id="49dff-153">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="49dff-153">Contact support.</span></span>
<span data-ttu-id="49dff-154">Se hai domande, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.</span><span class="sxs-lookup"><span data-stu-id="49dff-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

