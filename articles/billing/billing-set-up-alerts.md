---
title: aaaSet di avvisi di fatturazione o carta di credito per le sottoscrizioni di Azure | Documenti Microsoft
description: "Viene descritto come è possibile impostare gli avvisi di fatturazione di Azure per evitare sorprese fatturazione."
keywords: avviso di credito, avviso di fatturazione
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="cf91d-104">Impostare avvisi di fatturazione o di credito per le sottoscrizioni di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="cf91d-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="cf91d-105">Se si è amministratore dell'Account di hello per una sottoscrizione di Azure, è possibile utilizzare hello Azure fatturazione avviso servizio avvisi di fatturazione toocreate personalizzati che consentono di monitorare e gestire attività di fatturazione per l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf91d-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="cf91d-106">Questo servizio è in anteprima, pertanto è necessario tooenable nella pagina di funzionalità di anteprima hello prima.</span><span class="sxs-lookup"><span data-stu-id="cf91d-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="cf91d-107">Impostare i destinatari di posta elettronica e di soglia avviso hello</span><span class="sxs-lookup"><span data-stu-id="cf91d-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="cf91d-108">Visitare [pagina di funzionalità di anteprima hello](https://account.windowsazure.com/PreviewFeatures) e abilitare **servizio di avvisi di fatturazione**.</span><span class="sxs-lookup"><span data-stu-id="cf91d-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="cf91d-109">Dopo aver ricevuto una conferma tramite posta elettronica hello che servizio di fatturazione hello è attivata per la sottoscrizione, visitare [pagina sottoscrizioni hello](https://account.windowsazure.com/Subscriptions) nel portale di account hello.</span><span class="sxs-lookup"><span data-stu-id="cf91d-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="cf91d-110">Fare clic su sottoscrizione hello desidera toomonitor e quindi fare clic su **avvisi**.</span><span class="sxs-lookup"><span data-stu-id="cf91d-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![Schermata di vista delle sottoscrizioni hello del centro Account Azure, con gli avvisi evidenziato][Image1]

2. <span data-ttu-id="cf91d-112">Successivamente, fare clic su **Aggiungi avviso** toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="cf91d-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="cf91d-113">È possibile impostare su un totale di cinque avvisi di fatturazione per sottoscrizione, con un'altra soglia e dei destinatari di posta elettronica tootwo per ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="cf91d-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Schermata di visualizzazione di avvisi, in cui è possibile aggiungere avviso hello][Image2]

3. <span data-ttu-id="cf91d-115">Quando si aggiunge un avviso, assegnare un nome univoco, scegliere una soglia di spesa e scegliere hello indirizzi di posta elettronica in cui gli avvisi vengono inviati.</span><span class="sxs-lookup"><span data-stu-id="cf91d-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="cf91d-116">Quando si imposta la soglia hello, è possibile scegliere un **totale fattura** o **credito monetario** da hello **avviso per** elenco.</span><span class="sxs-lookup"><span data-stu-id="cf91d-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="cf91d-117">Per un totale di fatturazione, viene inviato un avviso quando spesa per la sottoscrizione supera la soglia di hello.</span><span class="sxs-lookup"><span data-stu-id="cf91d-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="cf91d-118">Per un credito monetario, viene inviato un avviso quando il credito monetario scende sotto il limite di hello.</span><span class="sxs-lookup"><span data-stu-id="cf91d-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="cf91d-119">I crediti monetari in genere applicano tooFree le sottoscrizioni di valutazione e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf91d-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![Schermata della visualizzazione di avvisi aggiunta hello, in cui è possibile configurare destinatari][Image3]

<span data-ttu-id="cf91d-121">Azure supporta qualsiasi indirizzo di posta elettronica, ma non verificare il funzionamento dell'indirizzo di posta elettronica hello, pertanto si consiglia di controllare gli errori di battitura.</span><span class="sxs-lookup"><span data-stu-id="cf91d-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="cf91d-122">Controllare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="cf91d-122">Check on your alerts</span></span>
<span data-ttu-id="cf91d-123">Dopo aver impostato gli avvisi, hello centro Account li elenca e illustra il numero è più possibile configurare.</span><span class="sxs-lookup"><span data-stu-id="cf91d-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="cf91d-124">Per ogni avviso, vedere hello data e l'ora di invio, se si tratta di un avviso per totale fattura o a crediti monetari e limite hello impostati.</span><span class="sxs-lookup"><span data-stu-id="cf91d-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="cf91d-125">il formato di data e ora Hello è 24 ore coordinare UTC (Universal Time) e data hello è formato aaaa-mm-gg.</span><span class="sxs-lookup"><span data-stu-id="cf91d-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="cf91d-126">Scegliere hello e firmarlo per un avviso in hello elenco tooedit o toodelete Cestino hello è.</span><span class="sxs-lookup"><span data-stu-id="cf91d-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="cf91d-127">Avvisi di fatturazione per i clienti con contratto Enterprise (EA, Enterprise Agreement)</span><span class="sxs-lookup"><span data-stu-id="cf91d-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="cf91d-128">Nell'ambito di una registrazione i clienti EA possono usufruire di avvisi per ogni reparto, impostando le quote di spesa.</span><span class="sxs-lookup"><span data-stu-id="cf91d-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="cf91d-129">Vedere [reparto spesa quote](https://ea.azure.com/helpdocs/departmentSpendingQuotas) nel portale tooget EA hello avviato.</span><span class="sxs-lookup"><span data-stu-id="cf91d-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="cf91d-130">Altre informazioni sulla gestione dei costi in Azure</span><span class="sxs-lookup"><span data-stu-id="cf91d-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="cf91d-131">Stima dei costi mediante hello [calcolatore dei costi](https://azure.microsoft.com/pricing/calculator/), [costo totale di calcolatrice di proprietà](https://aka.ms/azure-tco-calculator), e quando si aggiunge un servizio.</span><span class="sxs-lookup"><span data-stu-id="cf91d-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="cf91d-132">[Verificare regolarmente uso e costi nel portale di Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="cf91d-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="cf91d-133">Attivare i [consigli di Azure Advisor sui costi](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="cf91d-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="cf91d-134">vedere, più toolearn [Guida alla gestione dei costi Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="cf91d-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
