---
title: Informazioni sugli addebiti per i servizi esterni di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="2861d-103">Informazioni sulla fatturazione di Azure per gli addebiti dei servizi esterni</span><span class="sxs-lookup"><span data-stu-id="2861d-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="2861d-104">I servizi esterni erano denominati Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2861d-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="2861d-105">Si tratta in genere di servizi pubblicati da terze parti disponibili per Azure, ma integrati completamente in Azure.</span><span class="sxs-lookup"><span data-stu-id="2861d-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="2861d-106">Ad esempio, ClearDB e SendGrid sono servizi esterni che è possibile acquistare in Azure, ma che non vengono pubblicati da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2861d-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="2861d-107">Durante il provisioning di un nuovo servizio esterno o di una nuova risorsa, viene visualizzato un avviso:</span><span class="sxs-lookup"><span data-stu-id="2861d-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Avviso di acquisto di Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="2861d-109">I servizi esterni vengono pubblicati da società non Microsoft, ma talvolta anche i prodotti Microsoft sono classificati come servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="2861d-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="2861d-110">Modalità di fatturazione dei servizi esterni</span><span class="sxs-lookup"><span data-stu-id="2861d-110">How external services are billed</span></span>
- <span data-ttu-id="2861d-111">I servizi esterni vengono fatturati separatamente.</span><span class="sxs-lookup"><span data-stu-id="2861d-111">External services are billed separately.</span></span> <span data-ttu-id="2861d-112">Vengono gestiti come ordini singoli all'interno della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2861d-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="2861d-113">Il periodo di fatturazione per ogni servizio è impostato al momento dell'acquisto del servizio.</span><span class="sxs-lookup"><span data-stu-id="2861d-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="2861d-114">Non deve essere confuso con il periodo di fatturazione della sottoscrizione in cui è stato eseguito l'acquisto.</span><span class="sxs-lookup"><span data-stu-id="2861d-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="2861d-115">Si ricevono anche fatture separate e l'addebito sulla carta di credito viene applicato separatamente.</span><span class="sxs-lookup"><span data-stu-id="2861d-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="2861d-116">Per ogni servizio esterno è previsto un modello di fatturazione diverso.</span><span class="sxs-lookup"><span data-stu-id="2861d-116">Each external service has a different billing model.</span></span> <span data-ttu-id="2861d-117">Alcuni servizi vengono fatturati con pagamento in base al consumo, mentre altri prevedono un modello di pagamento su base mensile.</span><span class="sxs-lookup"><span data-stu-id="2861d-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="2861d-118">Per i servizi esterni di Azure è necessaria una carta di credito e non è possibile pagare tramite fattura.</span><span class="sxs-lookup"><span data-stu-id="2861d-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="2861d-119">Non è possibile usare i crediti gratuiti mensili per i servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="2861d-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="2861d-120">Se si usa una sottoscrizione di Azure che include [crediti gratuiti](https://azure.microsoft.com/pricing/spending-limits/), questi non possono essere applicati ai pagamenti per i servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="2861d-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="2861d-121">Usare una carta di credito per acquistare servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="2861d-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="2861d-122">Visualizzare la spesa e la cronologia dei servizi esterni nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2861d-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="2861d-123">È possibile visualizzare un elenco di servizi esterni inclusi in ogni sottoscrizione all'interno del [portale di Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="2861d-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="2861d-124">Accedere al [portale di Azure](https://portal.azure.com/) come amministratore account.</span><span class="sxs-lookup"><span data-stu-id="2861d-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="2861d-125">Nel menu Hub selezionare **Sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="2861d-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![Selezionare Sottoscrizioni nel menu Hub](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="2861d-127">Nel pannello **Sottoscrizioni** selezionare la sottoscrizione che si vuole visualizzare e quindi **Servizi esterni**.</span><span class="sxs-lookup"><span data-stu-id="2861d-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Selezionare una sottoscrizione nel pannello Fatturazione](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="2861d-129">Vengono visualizzati gli ordini di servizi esterni, il nome del publisher, il livello di servizio acquistato, il nome assegnato alla risorsa e lo stato corrente dell'ordine.</span><span class="sxs-lookup"><span data-stu-id="2861d-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="2861d-130">Selezionare un servizio esterno per visualizzare le fatture precedenti.</span><span class="sxs-lookup"><span data-stu-id="2861d-130">To see past bills, select an external service.</span></span>
   
    ![Selezionare un servizio esterno](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="2861d-132">A questo punto è possibile visualizzare gli importi di fatture precedenti, inclusa la ripartizione fiscale.</span><span class="sxs-lookup"><span data-stu-id="2861d-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![Visualizzare la cronologia di fatturazione dei servizi esterni](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="2861d-134">Visualizzare la spesa dei servizi esterni per i clienti con contratto Enterprise (EA, Enterprise Agreement)</span><span class="sxs-lookup"><span data-stu-id="2861d-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="2861d-135">I clienti EA possono visualizzare la spesa dei servizi esterni e scaricare i report nel portale EA.</span><span class="sxs-lookup"><span data-stu-id="2861d-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="2861d-136">Per iniziare, vedere [Azure Marketplace per i clienti EA](https://ea.azure.com/helpdocs/azureMarketplace).</span><span class="sxs-lookup"><span data-stu-id="2861d-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="2861d-137">Gestire i metodi di pagamento per gli ordini di servizi esterni</span><span class="sxs-lookup"><span data-stu-id="2861d-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="2861d-138">Aggiornare i metodi di pagamento per gli ordini di servizi esterni da [Centro account](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="2861d-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="2861d-139">Se la sottoscrizione è stata acquistata con un account aziendale o dell'istituto di istruzione, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per apportare modifiche al metodo di pagamento.</span><span class="sxs-lookup"><span data-stu-id="2861d-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="2861d-140">Accedere al [Centro account](https://account.windowsazure.com/) e [passare alla scheda **Marketplace**](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="2861d-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Selezionare Marketplace nel Centro account](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="2861d-142">Selezionare il servizio esterno da gestire</span><span class="sxs-lookup"><span data-stu-id="2861d-142">Select the external service you want to manage</span></span>
   
    ![Selezionare il servizio esterno da gestire](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="2861d-144">Sul lato destro della pagina fare clic su **Modifica il metodo di pagamento**.</span><span class="sxs-lookup"><span data-stu-id="2861d-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="2861d-145">Questo collegamento consente di accedere a un portale diverso per gestire il metodo di pagamento.</span><span class="sxs-lookup"><span data-stu-id="2861d-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Riepilogo degli ordini](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="2861d-147">Fare clic su **Modifica informazioni** e seguire le istruzioni per aggiornare le informazioni di pagamento.</span><span class="sxs-lookup"><span data-stu-id="2861d-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Selezionare Modifica informazioni](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="2861d-149">Annullare un ordine di servizio esterno</span><span class="sxs-lookup"><span data-stu-id="2861d-149">Cancel an external service order</span></span>
<span data-ttu-id="2861d-150">Se si desidera annullare l'ordine di servizio esterno, eliminare la risorsa nel [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2861d-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Eliminare una risorsa](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="2861d-152">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="2861d-152">Need help?</span></span> <span data-ttu-id="2861d-153">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="2861d-153">Contact support.</span></span>
<span data-ttu-id="2861d-154">Per eventuali domande, è possibile [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="2861d-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

