---
title: Scaricare la fattura e i dati di uso giornalieri di Azure | Microsoft Docs
description: L'articolo descrive come scaricare o visualizzare la fatturazione e dati di uso giornalieri di Azure.
keywords: fatturazione, scaricare la fatture, fattura di Azure, uso di Azure
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c63d9523555f47b4e5c0f3766f3ba080f76ac19e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a><span data-ttu-id="80ae9-104">Scaricare o visualizzare la fattura e i dati di uso giornalieri di Azure</span><span class="sxs-lookup"><span data-stu-id="80ae9-104">Download or view your Azure billing invoice and daily usage data</span></span>
<span data-ttu-id="80ae9-105">La fattura può essere scaricata dal [Portale di Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) o inviata via email.</span><span class="sxs-lookup"><span data-stu-id="80ae9-105">You can download your invoice from the [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) or have it sent in email.</span></span> <span data-ttu-id="80ae9-106">Per scaricare l'uso giornaliero, accedere al [Centro account di Azure](https://account.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="80ae9-106">To download your daily usage, go to the [Azure Account Center](https://account.windowsazure.com).</span></span> <span data-ttu-id="80ae9-107">Solo determinati ruoli dispongono dell'autorizzazione per ottenere informazioni sull'uso e sulla fatturazione, ad esempio l'amministratore account.</span><span class="sxs-lookup"><span data-stu-id="80ae9-107">Only certain roles have permission to get billing invoice and usage information, like the Account Administrator.</span></span> <span data-ttu-id="80ae9-108">Per altre informazioni sull'accesso alle informazioni di fatturazione, vedere [Manage access to Azure billing using roles](billing-manage-access.md) (Gestire l'accesso alla fatturazione di Azure usando i ruoli).</span><span class="sxs-lookup"><span data-stu-id="80ae9-108">To learn more about getting access to billing information, see [Manage access to Azure billing using roles](billing-manage-access.md).</span></span>

## <a name="get-your-invoice-in-email-pdf"></a><span data-ttu-id="80ae9-109">Ottenere la fattura tramite posta elettronica (formato PDF)</span><span class="sxs-lookup"><span data-stu-id="80ae9-109">Get your invoice in email (.pdf)</span></span>
<span data-ttu-id="80ae9-110">Per ricevere una fattura di Azure tramite posta elettronica, è possibile fornire il consenso esplicito e configurare altri destinatari.</span><span class="sxs-lookup"><span data-stu-id="80ae9-110">You can opt in and configure additional recipients to receive your Azure invoice in an email.</span></span> <span data-ttu-id="80ae9-111">Questa funzionalità potrebbe non essere disponibile per alcune sottoscrizioni, ad esempio offerte di supporto, contratti Enterprise o Azure in Open.</span><span class="sxs-lookup"><span data-stu-id="80ae9-111">This feature may not be available for certain subscriptions such as support offers, Enterprise Agreements, or Azure in Open.</span></span>

1. <span data-ttu-id="80ae9-112">Selezionare la sottoscrizione nel [pannello delle sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="80ae9-112">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span> <span data-ttu-id="80ae9-113">Dare il consenso esplicito per ogni sottoscrizione posseduta.</span><span class="sxs-lookup"><span data-stu-id="80ae9-113">Opt-in for each subscription you own.</span></span> <span data-ttu-id="80ae9-114">Fare clic su **Invoices** (Fatture) quindi su **Email my invoice** (Invia fattura tramite posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="80ae9-114">Click **Invoices** then **Email my invoice**.</span></span> 

    ![Schermata che mostra il flusso per il consenso esplicito](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. <span data-ttu-id="80ae9-116">Fare clic su **Acconsenti esplicitamente** e accettare i termini.</span><span class="sxs-lookup"><span data-stu-id="80ae9-116">Click **Opt in** and accept the terms.</span></span>

    ![Schermata che mostra il flusso per il consenso esplicito](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. <span data-ttu-id="80ae9-118">Dopo l'accettazione del contratto, sarà possibile configurare altri destinatari.</span><span class="sxs-lookup"><span data-stu-id="80ae9-118">Once you've accepted the agreement, you can configure additional recipients.</span></span>

    ![Schermata che mostra il flusso per il consenso esplicito](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
<span data-ttu-id="80ae9-120">Se non si riceve un'email dopo aver eseguito i passaggi seguenti, assicurarsi che l'indirizzo email sia corretto nelle [preferenze di comunicazione del proprio profilo](https://account.windowsazure.com/profile).</span><span class="sxs-lookup"><span data-stu-id="80ae9-120">If you don't get an email after following the steps, make sure your email address is correct in the [communication preferences on your profile](https://account.windowsazure.com/profile).</span></span>

## <a name="download-invoice-from-azure-portal-pdf"></a><span data-ttu-id="80ae9-121">Scaricare la fattura dal portale di Azure (PDF)</span><span class="sxs-lookup"><span data-stu-id="80ae9-121">Download invoice from Azure portal (.pdf)</span></span>

1. <span data-ttu-id="80ae9-122">Selezionare la sottoscrizione nel [pannello delle sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) nel portale di Azure come [un utente con accesso alle fatture](billing-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="80ae9-122">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal as [an user with access to invoices](billing-manage-access.md).</span></span>

2. <span data-ttu-id="80ae9-123">Selezionare **Fatture**.</span><span class="sxs-lookup"><span data-stu-id="80ae9-123">Select **Invoices**.</span></span> 

    ![Schermata che mostra l'opzione Fatturazione e utilizzo](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. <span data-ttu-id="80ae9-125">Fare clic su **Scarica fattura** per visualizzare una copia della fattura in formato PDF.</span><span class="sxs-lookup"><span data-stu-id="80ae9-125">Click **Download Invoice** to view a copy of your PDF invoice.</span></span> <span data-ttu-id="80ae9-126">Se l'indicazione è **Non disponibile**, vedere [Perché non viene visualizzata una fattura per l'ultimo periodo di fatturazione?](#noinvoice)</span><span class="sxs-lookup"><span data-stu-id="80ae9-126">If it says **Not available**, see [Why don't I see an invoice for the last billing period?](#noinvoice)</span></span>

    ![Schermata che mostra i periodi di fatturazione, l'opzione per il download e gli addebiti totali per ogni periodo di fatturazione](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. <span data-ttu-id="80ae9-128">Per visualizzare l'uso giornaliero, fare clic sul periodo di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="80ae9-128">You can also view your daily usage by clicking the billing period.</span></span> 

<span data-ttu-id="80ae9-129">Per altre informazioni sulla fattura, vedere [Comprendere la fattura per Microsoft Azure](billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="80ae9-129">For more information about your invoice, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span> <span data-ttu-id="80ae9-130">Per informazioni sulla gestione dei costi, vedere [Evitare costi aggiuntivi con la gestione dei costi e la fatturazione di Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="80ae9-130">For help managing costs, see [Prevent unexpected costs with Azure billing and cost management](billing-getting-started.md).</span></span>

## <a name="download-usage-from-the-account-center-csv"></a><span data-ttu-id="80ae9-131">Scaricare i dati di utilizzo dal Centro account (CSV)</span><span class="sxs-lookup"><span data-stu-id="80ae9-131">Download usage from the Account Center (.csv)</span></span>

1. <span data-ttu-id="80ae9-132">Accedere al [Centro account di Azure](https://account.windowsazure.com/subscriptions) come amministratore account.</span><span class="sxs-lookup"><span data-stu-id="80ae9-132">Sign into the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.</span></span>

2. <span data-ttu-id="80ae9-133">Selezionare la sottoscrizione per cui si desiderano le informazioni delle fatture e degli utilizzi.</span><span class="sxs-lookup"><span data-stu-id="80ae9-133">Select the subscription for which you want the invoice and usage information.</span></span>

3. <span data-ttu-id="80ae9-134">Selezionare **Cronologia di fatturazione**.</span><span class="sxs-lookup"><span data-stu-id="80ae9-134">Select **BILLING HISTORY**.</span></span> 

    ![Schermata che mostra l'opzione Cronologia di fatturazione](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. <span data-ttu-id="80ae9-136">Vengono elencati i rendiconti per gli ultimi sei periodi di fatturazione e il periodo corrente non ancora fatturato.</span><span class="sxs-lookup"><span data-stu-id="80ae9-136">You can see your statements for the last six billing periods and the current unbilled period.</span></span> 

    ![Schermata che mostra i periodi di fatturazione, le opzioni per il download della fattura e dei dati di utilizzo giornalieri e gli addebiti totali per ogni periodo di fatturazione](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. <span data-ttu-id="80ae9-138">Selezionare **Visualizza estratto conto corrente** per visualizzare una stima degli addebiti fino al momento in cui è stata generata la stima.</span><span class="sxs-lookup"><span data-stu-id="80ae9-138">Select **View Current Statement** to see an estimate of your charges at the time the estimate was generated.</span></span> <span data-ttu-id="80ae9-139">Queste informazioni vengono aggiornate solo una volta al giorno e potrebbero non includere tutti gli utilizzi effettuati.</span><span class="sxs-lookup"><span data-stu-id="80ae9-139">This information is only updated daily and may not include all your usage.</span></span> <span data-ttu-id="80ae9-140">È possibile che la fattura mensile non corrisponda a questa stima.</span><span class="sxs-lookup"><span data-stu-id="80ae9-140">Your monthly invoice may differ from this estimate.</span></span>

    ![Schermata che mostra l'opzione Visualizza estratto conto corrente](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Schermata che mostra la stima degli addebiti correnti](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. <span data-ttu-id="80ae9-143">Selezionare **Scarica utilizzo** per scaricare i dati di utilizzo giornalieri come file CSV.</span><span class="sxs-lookup"><span data-stu-id="80ae9-143">Select **Download Usage** to download the daily usage data as a CSV file.</span></span> <span data-ttu-id="80ae9-144">Se vengono visualizzate due versioni disponibili, scaricare la versione 2.</span><span class="sxs-lookup"><span data-stu-id="80ae9-144">If you see two versions available, download version 2.</span></span>

    ![Schermata che mostra l'opzione Scarica utilizzo](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

<span data-ttu-id="80ae9-146">Solo l'amministratore account può accedere al Centro account di Azure.</span><span class="sxs-lookup"><span data-stu-id="80ae9-146">Only the Account Administrator can access the Azure Account Center.</span></span> <span data-ttu-id="80ae9-147">Gli altri amministratori della fatturazione, ad esempio il proprietario, possono ottenere le informazioni sull'uso tramite le [API di fatturazione](billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="80ae9-147">Other billing admins, such as an Owner, can get usage information using the [Billing APIs](billing-usage-rate-card-overview.md).</span></span>

<span data-ttu-id="80ae9-148">Per altre informazioni sui dati di utilizzo giornalieri, vedere [Comprendere la fattura per Microsoft Azure](billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="80ae9-148">For more information about your daily usage, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span> <span data-ttu-id="80ae9-149">Per informazioni sulla gestione dei costi, vedere [Evitare costi aggiuntivi con la gestione dei costi e la fatturazione di Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="80ae9-149">For help managing costs, see [Prevent unexpected costs with Azure billing and cost management](billing-getting-started.md).</span></span>

## <span data-ttu-id="80ae9-150"><a name="noinvoice"></a> Perché non viene visualizzata una fattura per l'ultimo periodo di fatturazione?</span><span class="sxs-lookup"><span data-stu-id="80ae9-150"><a name="noinvoice"></a> Why don't I see an invoice for the last billing period?</span></span>

<span data-ttu-id="80ae9-151">Potrebbero esserci diversi motivi per cui non è visualizzata alcuna fattura:</span><span class="sxs-lookup"><span data-stu-id="80ae9-151">There could be several reasons that you don't see an invoice:</span></span>

- <span data-ttu-id="80ae9-152">Si dispone di un credito mensile per la sottoscrizione che non è stato superato oppure si sta usando una versione di prova gratuita.</span><span class="sxs-lookup"><span data-stu-id="80ae9-152">You have a monthly credit amount with your subscription that you didn't exceed or you have a Free Trial.</span></span> <span data-ttu-id="80ae9-153">La fattura viene generata solo quando si possiede del denaro.</span><span class="sxs-lookup"><span data-stu-id="80ae9-153">An invoice is only generated when you owe money.</span></span>

- <span data-ttu-id="80ae9-154">Sono passati meno di trenta giorni dalla data della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="80ae9-154">It's less than 30 days from the day you subscribed to Azure.</span></span>

- <span data-ttu-id="80ae9-155">La fattura non è stata ancora generata.</span><span class="sxs-lookup"><span data-stu-id="80ae9-155">The invoice isn't generated yet.</span></span> <span data-ttu-id="80ae9-156">Attendere la fine del periodo di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="80ae9-156">Wait until the end of the billing period.</span></span>

- <span data-ttu-id="80ae9-157">Se non si è l'amministratore account, le fatture precedenti potrebbero non essere disponibili.</span><span class="sxs-lookup"><span data-stu-id="80ae9-157">If you're not the Account Administrator, older invoices may not be avaialbe to you.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="80ae9-158">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="80ae9-158">Need help?</span></span> <span data-ttu-id="80ae9-159">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="80ae9-159">Contact support.</span></span>
<span data-ttu-id="80ae9-160">Per altre domande, è possibile [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="80ae9-160">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

