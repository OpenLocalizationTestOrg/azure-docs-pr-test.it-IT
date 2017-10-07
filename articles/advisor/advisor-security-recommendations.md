---
title: consigli sulla sicurezza Advisor aaaAzure | Documenti Microsoft
description: Utilizzare Advisor Azure toohelp migliorare la sicurezza hello delle distribuzioni di Azure.
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
ms.openlocfilehash: e01ac29eb6e02bff0b1e846e320e7c36f85c7343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="9e123-103">Consigli di Advisor sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="9e123-103">Advisor Security recommendations</span></span>

<span data-ttu-id="9e123-104">Azure Advisor fornisce una visualizzazione coerente e consolidata dei consigli per tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e123-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="9e123-105">Si integra con toobring Centro sicurezza di Azure è consigli relativi alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9e123-105">It integrates with Azure Security Center toobring you security recommendations.</span></span> <span data-ttu-id="9e123-106">È possibile ottenere indicazioni relative alla sicurezza da hello **sicurezza** scheda nel dashboard di Advisor hello.</span><span class="sxs-lookup"><span data-stu-id="9e123-106">You can get security recommendations from hello **Security** tab on hello Advisor dashboard.</span></span>

![pulsante Advisor sicurezza Hello](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="9e123-108">Centro sicurezza PC consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sulla protezione hello delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e123-108">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="9e123-109">Analizza periodicamente lo stato di sicurezza hello delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e123-109">It periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="9e123-110">Quando identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="9e123-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="9e123-111">indicazioni Hello semplificato il processo di hello di configurazione dei controlli di hello che è necessario.</span><span class="sxs-lookup"><span data-stu-id="9e123-111">hello recommendations guide you through hello process of configuring hello controls you need.</span></span> 

![scheda sicurezza Advisor Hello](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="9e123-113">Per altre informazioni sui consigli di sicurezza, vedere [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="9e123-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-tooaccess-security-recommendations-in-azure-advisor"></a><span data-ttu-id="9e123-114">Come tooaccess consigli sulla sicurezza in preparazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9e123-114">How tooaccess Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="9e123-115">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e123-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9e123-116">Nel riquadro di sinistra hello, fare clic su **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="9e123-116">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="9e123-117">Hello servizio dei menu, in **monitoraggio e gestione**, fare clic su **Advisor Azure**.</span><span class="sxs-lookup"><span data-stu-id="9e123-117">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="9e123-118">Hello Advisor dashboard viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="9e123-118">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="9e123-119">Nel dashboard di Advisor hello, fare clic su hello **sicurezza** scheda.</span><span class="sxs-lookup"><span data-stu-id="9e123-119">On hello Advisor dashboard, click hello **Security** tab.</span></span>

5. <span data-ttu-id="9e123-120">Selezionare hello sottoscrizione per il quale desidera tooreceive indicazioni e quindi fare clic su **consigli**.</span><span class="sxs-lookup"><span data-stu-id="9e123-120">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="9e123-121">tooaccess raccomandazioni di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="9e123-121">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="9e123-122">Una sottoscrizione viene registrata quando un *sottoscrizione proprietario* avvia hello hello di dashboard e fa clic su Advisor **consigli** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9e123-122">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="9e123-123">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="9e123-123">This is a *one-time operation*.</span></span> <span data-ttu-id="9e123-124">Dopo la sottoscrizione hello è registrata, è possibile accedere raccomandazioni di Advisor come *proprietario*, *collaboratore*, o *lettore* per una sottoscrizione, un gruppo di risorse, o risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="9e123-124">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e123-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e123-125">Next steps</span></span>

<span data-ttu-id="9e123-126">toolearn sulle raccomandazioni di Advisor, vedere:</span><span class="sxs-lookup"><span data-stu-id="9e123-126">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="9e123-127">Introduzione tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="9e123-127">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="9e123-128">Introduzione ad Advisor</span><span class="sxs-lookup"><span data-stu-id="9e123-128">Get started with Advisor</span></span>](advisor-get-started.md)
* <span data-ttu-id="9e123-129">[Advisor Cost recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sui costi)</span><span class="sxs-lookup"><span data-stu-id="9e123-129">[Advisor Cost recommendations](advisor-performance-recommendations.md)</span></span>
* <span data-ttu-id="9e123-130">[Advisor Performance recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sulle prestazioni)</span><span class="sxs-lookup"><span data-stu-id="9e123-130">[Advisor Performance recommendations](advisor-performance-recommendations.md)</span></span>
* <span data-ttu-id="9e123-131">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)</span><span class="sxs-lookup"><span data-stu-id="9e123-131">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md)</span></span>


 
