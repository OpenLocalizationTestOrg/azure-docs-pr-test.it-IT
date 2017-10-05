---
title: Annullare la sottoscrizione di Azure | Microsoft Docs
description: Descrive come annullare la sottoscrizione di Azure, ad esempio la sottoscrizione di valutazione gratuita
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: c415fada30aa0b0bd9b9d1e416bc37ef30653f68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="cancel-your-subscription-for-azure"></a><span data-ttu-id="bd48e-103">Annullare la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="bd48e-103">Cancel your subscription for Azure</span></span>

<span data-ttu-id="bd48e-104">Come [amministratore account](billing-subscription-transfer.md#whoisaa), è possibile annullare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bd48e-104">You can cancel your Azure subscription as the [Account Administrator](billing-subscription-transfer.md#whoisaa).</span></span> <span data-ttu-id="bd48e-105">Dopo aver annullato la sottoscrizione, l'accesso alle risorse e ai servizi di Azure non sarà più possibile.</span><span class="sxs-lookup"><span data-stu-id="bd48e-105">After you cancel the subscription, your access to Azure services and resources ends.</span></span>

<span data-ttu-id="bd48e-106">Prima di annullare la sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="bd48e-106">Before you cancel your subscription:</span></span>

* <span data-ttu-id="bd48e-107">Eseguire il backup dei dati.</span><span class="sxs-lookup"><span data-stu-id="bd48e-107">Back up your data.</span></span> <span data-ttu-id="bd48e-108">Se ad esempio si archiviano i dati in Archiviazione di Azure o SQL, scaricare una copia.</span><span class="sxs-lookup"><span data-stu-id="bd48e-108">For example, if you're storing data in Azure storage or SQL, download a copy.</span></span> <span data-ttu-id="bd48e-109">Se si ha una macchina virtuale, salvare un'immagine in locale.</span><span class="sxs-lookup"><span data-stu-id="bd48e-109">If you have a virtual machine, save an image of it locally.</span></span>
* <span data-ttu-id="bd48e-110">Arrestare i servizi.</span><span class="sxs-lookup"><span data-stu-id="bd48e-110">Shut down your services.</span></span> <span data-ttu-id="bd48e-111">Passare alla [pagina delle risorse nel portale di gestione](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources) e **arrestare** qualsiasi macchina virtuale, applicazione o altri servizi.</span><span class="sxs-lookup"><span data-stu-id="bd48e-111">Go to the [resources page in the management portal](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), and **Stop** any running virtual machines, applications, or other services.</span></span>
* <span data-ttu-id="bd48e-112">Prendere in considerazione la migrazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="bd48e-112">Consider migrating your data.</span></span> <span data-ttu-id="bd48e-113">Vedere [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md) (Spostare le risorse in un nuovo gruppo o sottoscrizione).</span><span class="sxs-lookup"><span data-stu-id="bd48e-113">See [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="bd48e-114">Se si annulla un [piano di supporto di Azure](https://azure.microsoft.com/support/plans/) a pagamento, verrà comunque emessa una fattura mensile per il resto del semestre.</span><span class="sxs-lookup"><span data-stu-id="bd48e-114">If you cancel a paid [Azure Support plan](https://azure.microsoft.com/support/plans/), you are still billed monthly for the rest of the 6-months term.</span></span>

## <a name="cancel-subscription-using-the-azure-portal"></a><span data-ttu-id="bd48e-115">Annullare la sottoscrizione usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bd48e-115">Cancel subscription using the Azure portal</span></span>

1. <span data-ttu-id="bd48e-116">Selezionare la sottoscrizione nella [pagina delle sottoscrizioni](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="bd48e-116">Select your subscription from the [Subscriptions page](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

1. <span data-ttu-id="bd48e-117">Selezionare la sottoscrizione da annullare e fare clic su **Annulla sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="bd48e-117">Select the subscription that you want to cancel and click **Cancel subscription**.</span></span>

    ![Screenshot che mostra il pulsante Annulla](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. <span data-ttu-id="bd48e-119">Seguire le istruzioni e completare la procedura di annullamento.</span><span class="sxs-lookup"><span data-stu-id="bd48e-119">Follow prompts and finish cancellation.</span></span>

## <a name="cancel-subscription-using-the-azure-account-center"></a><span data-ttu-id="bd48e-120">Annullare la sottoscrizione usando il Centro account di Azure</span><span class="sxs-lookup"><span data-stu-id="bd48e-120">Cancel subscription using the Azure Account Center</span></span>

1. <span data-ttu-id="bd48e-121">Accedere al [Centro account di Azure](https://account.windowsazure.com/subscriptions) come Amministratore account.</span><span class="sxs-lookup"><span data-stu-id="bd48e-121">Sign in to the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.</span></span>

1. <span data-ttu-id="bd48e-122">In **Fare clic su una sottoscrizione per visualizzare i dettagli e l'utilizzo**selezionare la sottoscrizione che si vuole annullare.</span><span class="sxs-lookup"><span data-stu-id="bd48e-122">Under **Click a subscription to view details and usage**, select the subscription that you want to cancel.</span></span>

    ![Screenshot che mostra un esempio di sottoscrizione selezionata](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. <span data-ttu-id="bd48e-124">Sul lato destro della pagina selezionare **Annulla sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="bd48e-124">On the right side of the page, select **Cancel Subscription**.</span></span>

    ![Screenshot che mostra il pulsante Annulla sottoscrizione](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. <span data-ttu-id="bd48e-126">Selezionare **Sì, annulla la sottoscrizione**.</span><span class="sxs-lookup"><span data-stu-id="bd48e-126">Select **Yes, cancel my subscription**.</span></span>

    ![Screenshot che mostra la finestra di dialogo Annulla](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. <span data-ttu-id="bd48e-128">Fare clic su </span><span class="sxs-lookup"><span data-stu-id="bd48e-128">Click</span></span> ![pulsante con segno di spunta](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) <span data-ttu-id="bd48e-130">per chiudere la finestra di dialogo e tornare alla pagina di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bd48e-130">to close the dialog window and return to your subscription page.</span></span>

## <a name="what-happens-after-i-cancel-my-subscription"></a><span data-ttu-id="bd48e-131">Cosa accade quando si annulla la sottoscrizione?</span><span class="sxs-lookup"><span data-stu-id="bd48e-131">What happens after I cancel my subscription?</span></span>

<span data-ttu-id="bd48e-132">Nel momento in cui viene annullata, la fatturazione viene interrotta immediatamente.</span><span class="sxs-lookup"><span data-stu-id="bd48e-132">Once you cancel, billing is stopped immediately.</span></span> <span data-ttu-id="bd48e-133">Per essere visualizzata sul portale, tuttavia, è possibile che siano necessari fino a 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="bd48e-133">However, it can take up to 10 minutes for the cancellation show in the portal.</span></span>

<span data-ttu-id="bd48e-134">Dopo questo intervallo, i servizi vengono disabilitati.</span><span class="sxs-lookup"><span data-stu-id="bd48e-134">After that, your services are disabled.</span></span> <span data-ttu-id="bd48e-135">Le macchine virtuali vengono quindi deallocate e gli indirizzi IP temporanei liberati e la risorsa di archiviazione diventa di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="bd48e-135">That means your virtual machines are deallocated, temporary IP addresses are freed, and storage is read-only.</span></span>

<span data-ttu-id="bd48e-136">A meno che non si stia usando una versione di valutazione gratuita o non si abbiano crediti disponibili, verrà addebitato l'importo corrispondente all'uso della sottoscrizione intercorso tra l'ultimo ciclo di fatturazione e la data di annullamento.</span><span class="sxs-lookup"><span data-stu-id="bd48e-136">Unless you’re on a Free Trial or have credits available, you’re billed for any outstanding usage charges generated between your last billing cycle and the cancellation date.</span></span> <span data-ttu-id="bd48e-137">Al termine del ciclo di fatturazione è possibile richiedere l'ultima fattura.</span><span class="sxs-lookup"><span data-stu-id="bd48e-137">You get your last bill at the end of the billing cycle.</span></span>

<span data-ttu-id="bd48e-138">Dopo aver annullato la sottoscrizione, Microsoft attenderà 90 giorni prima di eliminare definitivamente i dati, nel caso in cui fosse necessario accedervi o si cambiasse idea.</span><span class="sxs-lookup"><span data-stu-id="bd48e-138">After you cancel your subscription, we wait 90 days before permanently deleting your data in case you need to access it or you change your mind.</span></span> <span data-ttu-id="bd48e-139">Non verrà comunque addebitato alcun costo per questo servizio di conservazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="bd48e-139">We don't charge you for retaining the data.</span></span> <span data-ttu-id="bd48e-140">Per altre informazioni, vedere [Microsoft Trust Center - Come vengono gestiti i dati](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="bd48e-140">To learn more, see [Microsoft Trust Center - How we manage your data](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).</span></span>

## <a name="reactivate-subscription"></a><span data-ttu-id="bd48e-141">Riattivare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="bd48e-141">Reactivate subscription</span></span>

<span data-ttu-id="bd48e-142">Se la sottoscrizione con pagamento in base al consumo viene annullata erroneamente, è possibile [riattivarla nel Centro account](billing-subscription-become-disable.md).</span><span class="sxs-lookup"><span data-stu-id="bd48e-142">If you cancel your Pay-As-You-Go subscription accidentally, you can [reactivate it in the Accounts Center](billing-subscription-become-disable.md).</span></span>

<span data-ttu-id="bd48e-143">Se la sottoscrizione non è con pagamento in base al consumo, contattare il supporto tecnico entro 90 giorni dall'annullamento per riattivare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bd48e-143">If your subscription is not Pay-As-You-Go, contact support within 90 days of cancellation to reactivate your subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="bd48e-144">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="bd48e-144">Need help?</span></span> <span data-ttu-id="bd48e-145">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="bd48e-145">Contact support.</span></span>

<span data-ttu-id="bd48e-146">Per eventuali domande, è possibile [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="bd48e-146">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
