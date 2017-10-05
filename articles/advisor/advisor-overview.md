---
title: Presentazione di Azure Advisor | Microsoft Docs
description: Usare Azure Advisor per ottimizzare le distribuzioni di Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 35678142550f9f887562f311a5e7d9516495cf53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="1de01-103">Presentazione di Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="1de01-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="1de01-104">Informazioni su Azure Advisor, sulle sue funzionalità chiave e sulle domande più frequenti.</span><span class="sxs-lookup"><span data-stu-id="1de01-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="1de01-105">Cos'è Advisor?</span><span class="sxs-lookup"><span data-stu-id="1de01-105">What is Advisor?</span></span>
<span data-ttu-id="1de01-106">Advisor è un consulente cloud personalizzato che illustra come seguire le procedure consigliate per ottimizzare le distribuzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="1de01-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="1de01-107">Analizza i dati di telemetria dell'uso e della configurazione delle risorse e consiglia soluzioni che consentono di migliorare l'efficienza dei costi, le prestazioni, la disponibilità elevata e la sicurezza delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="1de01-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="1de01-108">Con Advisor, è possibile:</span><span class="sxs-lookup"><span data-stu-id="1de01-108">With Advisor, you can:</span></span>
* <span data-ttu-id="1de01-109">Ottenere consigli personalizzati, attuabili e proattivi sulle procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="1de01-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="1de01-110">Migliorare le prestazioni, la sicurezza e la disponibilità elevata delle risorse, cercando le opportunità per ridurre la spesa complessiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="1de01-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="1de01-111">Ricevere consigli con azioni proposte incorporate.</span><span class="sxs-lookup"><span data-stu-id="1de01-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="1de01-112">È possibile accedere ad Advisor attraverso il [portale di Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="1de01-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="1de01-113">Accedere al [portale](https://portal.azure.com), selezionare **Sfoglia** e quindi scorrere fino ad **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="1de01-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="1de01-114">Nel dashboard di Advisor vengono visualizzati consigli personalizzati per la sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="1de01-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="1de01-115">I consigli sono suddivisi in quattro categorie.</span><span class="sxs-lookup"><span data-stu-id="1de01-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="1de01-116">**Disponibilità elevata**: per garantire e migliorare la continuità delle applicazioni aziendali critiche.</span><span class="sxs-lookup"><span data-stu-id="1de01-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="1de01-117">Per altre informazioni, vedere [Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata).</span><span class="sxs-lookup"><span data-stu-id="1de01-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="1de01-118">**Sicurezza**: per rilevare le minacce e le vulnerabilità che potrebbero portare a potenziali violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1de01-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="1de01-119">Per altre informazioni, vedere [Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza).</span><span class="sxs-lookup"><span data-stu-id="1de01-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="1de01-120">**Prestazioni**: per aumentare la velocità delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1de01-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="1de01-121">Per altre informazioni, vedere [Advisor Performance recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sulle prestazioni).</span><span class="sxs-lookup"><span data-stu-id="1de01-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="1de01-122">**Costo**: per ottimizzare e ridurre la spesa complessiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="1de01-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="1de01-123">Per altre informazioni, vedere [Advisor Cost recommendations](advisor-cost-recommendations.md) (Consigli di Azure sui costi).</span><span class="sxs-lookup"><span data-stu-id="1de01-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![Tipi di consigli di Advisor](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="1de01-125">Per accedere ai consigli di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="1de01-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="1de01-126">Una sottoscrizione viene registrata quando il *proprietario della sottoscrizione* avvia il dashboard di Advisor e fa clic sul pulsante **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="1de01-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="1de01-127">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="1de01-127">This is a *one-time operation*.</span></span> <span data-ttu-id="1de01-128">Dopo aver registrato una sottoscrizione, è possibile accedere ai consigli di Advisor come *Proprietario*, *Collaboratore* o *Lettore* di una sottoscrizione, di un gruppo di risorse o di una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="1de01-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="1de01-129">È possibile fare clic su un consiglio per scoprire altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="1de01-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="1de01-130">È inoltre possibile trovare informazioni sulle azioni che è possibile eseguire per sfruttare un'opportunità o risolvere un problema.</span><span class="sxs-lookup"><span data-stu-id="1de01-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="1de01-131">Advisor offre consigli con azioni incorporate o collegamenti alla documentazione.</span><span class="sxs-lookup"><span data-stu-id="1de01-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="1de01-132">Facendo clic su un'azione incorporata, si passa a una procedura guidata per implementarla.</span><span class="sxs-lookup"><span data-stu-id="1de01-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="1de01-133">Facendo clic su un collegamento alla documentazione, si viene condotti alla documentazione che descrive come è possibile implementare manualmente l'operazione.</span><span class="sxs-lookup"><span data-stu-id="1de01-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="1de01-134">Advisor aggiorna i consigli ogni ora.</span><span class="sxs-lookup"><span data-stu-id="1de01-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="1de01-135">Se non si prevede di eseguire un'azione immediata in base a un consiglio, è possibile posporlo per un periodo di tempo oppure ignorarlo.</span><span class="sxs-lookup"><span data-stu-id="1de01-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="1de01-136">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="1de01-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="1de01-137">Come si accede ad Advisor?</span><span class="sxs-lookup"><span data-stu-id="1de01-137">How do I access Advisor?</span></span>
<span data-ttu-id="1de01-138">È possibile accedere ad Advisor attraverso il [portale di Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="1de01-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="1de01-139">Accedere al [portale](https://portal.azure.com), selezionare **Sfoglia** e quindi scorrere fino ad **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="1de01-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="1de01-140">Nel dashboard di Advisor vengono visualizzati consigli personalizzati per la sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="1de01-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="1de01-141">È possibile visualizzare i consigli di Advisor anche attraverso il pannello delle risorse delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1de01-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="1de01-142">Scegliere una macchina virtuale, quindi scorrere fino ai consigli di Advisor nel menu.</span><span class="sxs-lookup"><span data-stu-id="1de01-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="1de01-143">Quali autorizzazioni sono necessarie per accedere ad Advisor?</span><span class="sxs-lookup"><span data-stu-id="1de01-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="1de01-144">Per accedere ai consigli di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="1de01-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="1de01-145">Una sottoscrizione viene registrata quando il *proprietario della sottoscrizione* avvia il dashboard di Advisor e fa clic sul pulsante **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="1de01-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="1de01-146">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="1de01-146">This is a *one-time operation*.</span></span> <span data-ttu-id="1de01-147">Dopo aver registrato una sottoscrizione, è possibile accedere ai consigli di Advisor come *Proprietario*, *Collaboratore* o *Lettore* di una sottoscrizione, di un gruppo di risorse o di una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="1de01-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="1de01-148">Con che frequenza vengono aggiornati i consigli di Advisor?</span><span class="sxs-lookup"><span data-stu-id="1de01-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="1de01-149">I consigli di Advisor vengono aggiornati ogni ora.</span><span class="sxs-lookup"><span data-stu-id="1de01-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="1de01-150">Per quali risorse fornisce consigli Advisor?</span><span class="sxs-lookup"><span data-stu-id="1de01-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="1de01-151">Advisor fornisce consigli per macchine virtuali, set di disponibilità, gateway applicazione, Servizi app, SQL Server, database SQL e Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="1de01-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="1de01-152">È possibile posporre o ignorare un consiglio?</span><span class="sxs-lookup"><span data-stu-id="1de01-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="1de01-153">Per posporre o ignorare un consiglio, fare clic sul pulsante o sul collegamento **Posponi**.</span><span class="sxs-lookup"><span data-stu-id="1de01-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="1de01-154">È possibile specificare fino a quando posporre oppure selezionare **Mai** per ignorare il consiglio.</span><span class="sxs-lookup"><span data-stu-id="1de01-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1de01-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1de01-155">Next steps</span></span>

<span data-ttu-id="1de01-156">Per altre informazioni sui consigli di Advisor, vedere:</span><span class="sxs-lookup"><span data-stu-id="1de01-156">To learn more about Advisor recommendations, see:</span></span>

* <span data-ttu-id="1de01-157">[Get started with Advisor](advisor-get-started.md) (Introduzione ad Advisor)</span><span class="sxs-lookup"><span data-stu-id="1de01-157">[Get started with Advisor](advisor-get-started.md)</span></span>
* <span data-ttu-id="1de01-158">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)</span><span class="sxs-lookup"><span data-stu-id="1de01-158">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md)</span></span>
* <span data-ttu-id="1de01-159">[Advisor Security recommendations](advisor-security-recommendations.md) (Consigli di Advisor sulla sicurezza)</span><span class="sxs-lookup"><span data-stu-id="1de01-159">[Advisor Security recommendations](advisor-security-recommendations.md)</span></span>
* <span data-ttu-id="1de01-160">[Advisor Performance recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sulle prestazioni)</span><span class="sxs-lookup"><span data-stu-id="1de01-160">[Advisor Performance recommendations](advisor-performance-recommendations.md)</span></span>
* <span data-ttu-id="1de01-161">[Advisor Cost recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sui costi)</span><span class="sxs-lookup"><span data-stu-id="1de01-161">[Advisor Cost recommendations](advisor-cost-recommendations.md)</span></span>
