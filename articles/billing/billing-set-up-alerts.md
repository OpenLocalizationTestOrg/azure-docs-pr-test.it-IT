---
title: Impostare avvisi di fatturazione o di credito per le sottoscrizioni di Azure | Microsoft Docs
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
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="5860d-104">Impostare avvisi di fatturazione o di credito per le sottoscrizioni di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5860d-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="5860d-105">Se si amministrano gli account per una sottoscrizione di Azure, è possibile usare Azure Billing Alert Service per creare avvisi di fatturazione personalizzati che consentono di monitorare e gestire l'attività di fatturazione per gli account Azure.</span><span class="sxs-lookup"><span data-stu-id="5860d-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="5860d-106">Questo servizio è in anteprima, pertanto è necessario abilitarlo nella pagina relativa alle funzionalità di anteprima.</span><span class="sxs-lookup"><span data-stu-id="5860d-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="5860d-107">Impostare la soglia di avviso e i destinatari di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="5860d-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="5860d-108">Visitare la [pagina relativa alle funzionalità di anteprima](https://account.windowsazure.com/PreviewFeatures) e abilitare **Billing Alert Service**.</span><span class="sxs-lookup"><span data-stu-id="5860d-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="5860d-109">Dopo aver ricevuto tramite posta elettronica la conferma dell'attivazione del servizio di fatturazione per la sottoscrizione, visitare la [pagina relativa alle sottoscrizioni](https://account.windowsazure.com/Subscriptions) nel portale degli account.</span><span class="sxs-lookup"><span data-stu-id="5860d-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="5860d-110">Fare clic sulla sottoscrizione che si desidera monitorare, quindi selezionare **Avvisi**.</span><span class="sxs-lookup"><span data-stu-id="5860d-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Schermata delle sottoscrizioni del Centro account di Azure, con gli avvisi in evidenza][Image1]

2. <span data-ttu-id="5860d-112">Successivamente, fare clic su **Aggiungi avviso** per creare il primo avviso.</span><span class="sxs-lookup"><span data-stu-id="5860d-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="5860d-113">È possibile impostare un totale di cinque avvisi di fatturazione per sottoscrizione, con una soglia diversa e un massimo di due destinatari di posta elettronica per ciascun avviso.</span><span class="sxs-lookup"><span data-stu-id="5860d-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![Schermata degli avvisi, in cui è possibile aggiungere un avviso][Image2]

3. <span data-ttu-id="5860d-115">Quando si aggiunge un avviso, assegnare un nome univoco, scegliere una soglia di spesa e gli indirizzi di posta elettronica a cui verrà inviato.</span><span class="sxs-lookup"><span data-stu-id="5860d-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="5860d-116">Mentre si imposta la soglia, è possibile scegliere un valore per **Totale fattura** o **Credito monetario** dall'elenco **Avviso per**.</span><span class="sxs-lookup"><span data-stu-id="5860d-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="5860d-117">Se si specifica un totale fattura, viene inviato un avviso quando la spesa per la sottoscrizione supera la soglia.</span><span class="sxs-lookup"><span data-stu-id="5860d-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="5860d-118">Se si specifica un credito monetario, viene inviato un avviso quando i crediti monetari scendono al di sotto del limite.</span><span class="sxs-lookup"><span data-stu-id="5860d-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="5860d-119">I crediti monetari in genere si applicano alle sottoscrizioni della versione di valutazione gratuita e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5860d-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![Schermata della funzionalità di aggiunta avviso, in cui è possibile configurare i destinatari][Image3]

<span data-ttu-id="5860d-121">Azure supporta qualsiasi indirizzo di posta elettronica ma non ne verifica il corretto funzionamento, pertanto è necessario accertarsi che non siano presenti errori di digitazione.</span><span class="sxs-lookup"><span data-stu-id="5860d-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="5860d-122">Controllare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="5860d-122">Check on your alerts</span></span>
<span data-ttu-id="5860d-123">Dopo aver impostato gli avvisi, nel centro account viene visualizzato un elenco degli avvisi già impostati ed è indicato il numero di avvisi aggiuntivi che è possibile ancora impostare.</span><span class="sxs-lookup"><span data-stu-id="5860d-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="5860d-124">Per ogni avviso è possibile visualizzare la data e l'ora di invio, il tipo di avviso (per totale fattura o credito monetario) e il limite impostato.</span><span class="sxs-lookup"><span data-stu-id="5860d-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="5860d-125">Il formato dell'ora è 24 ore UTC (Universal Time Coordinate) e il formato della data è aaaa-mm-gg.</span><span class="sxs-lookup"><span data-stu-id="5860d-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="5860d-126">Fare clic sul segno più per modificare un avviso nell'elenco o sul simbolo del cestino per eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="5860d-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="5860d-127">Avvisi di fatturazione per i clienti con contratto Enterprise (EA, Enterprise Agreement)</span><span class="sxs-lookup"><span data-stu-id="5860d-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="5860d-128">Nell'ambito di una registrazione i clienti EA possono usufruire di avvisi per ogni reparto, impostando le quote di spesa.</span><span class="sxs-lookup"><span data-stu-id="5860d-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="5860d-129">Per iniziare, vedere [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) (Quote di spesa per reparto) nel portale EA.</span><span class="sxs-lookup"><span data-stu-id="5860d-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="5860d-130">Altre informazioni sulla gestione dei costi in Azure</span><span class="sxs-lookup"><span data-stu-id="5860d-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="5860d-131">Stimare i costi usando il [calcolatore dei prezzi](https://azure.microsoft.com/pricing/calculator/), il [calcolatore del costo totale di proprietà](https://aka.ms/azure-tco-calculator) e quando si aggiunge un servizio.</span><span class="sxs-lookup"><span data-stu-id="5860d-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="5860d-132">[Verificare regolarmente uso e costi nel portale di Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="5860d-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="5860d-133">Attivare i [consigli di Azure Advisor sui costi](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="5860d-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="5860d-134">Per altre informazioni, vedere [Introduzione alla gestione dei costi e alla fatturazione di Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5860d-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
