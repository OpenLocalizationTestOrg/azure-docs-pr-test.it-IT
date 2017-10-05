---
title: Consigli di Azure Advisor sulla sicurezza | Microsoft Docs
description: Usare Azure Advisor per aumentare la sicurezza delle distribuzioni di Azure.
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="2d6c3-103">Consigli di Advisor sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="2d6c3-103">Advisor Security recommendations</span></span>

<span data-ttu-id="2d6c3-104">Azure Advisor fornisce una visualizzazione coerente e consolidata dei consigli per tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="2d6c3-105">Si integra con il Centro sicurezza di Azure per offrire consigli relativi alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="2d6c3-106">È possibile ottenere consigli sulla sicurezza nella scheda **Sicurezza** del dashboard di Advisor.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![Pulsante Sicurezza di Advisor](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="2d6c3-108">Il Centro sicurezza impedisce, rileva e risponde alle minacce mediante visibilità e controllo avanzati della sicurezza delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="2d6c3-109">Analizza periodicamente lo stato di sicurezza delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="2d6c3-110">Quando identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="2d6c3-111">Questi consigli illustrano in dettaglio il processo di configurazione dei controlli necessari.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Scheda Sicurezza di Advisor](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="2d6c3-113">Per altre informazioni sui consigli di sicurezza, vedere [Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="2d6c3-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="2d6c3-114">Come accedere ai consigli sulla sicurezza in Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="2d6c3-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="2d6c3-115">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2d6c3-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2d6c3-116">Nel riquadro sinistro selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="2d6c3-117">Nel riquadro del menu del servizio in **Monitoraggio e gestione** fare clic su **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="2d6c3-118">Verrà visualizzato il dashboard di Advisor.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="2d6c3-119">Nel dashboard di Advisor fare clic sulla scheda **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="2d6c3-120">Selezionare la sottoscrizione per cui si desidera ricevere consigli e quindi fare clic su **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="2d6c3-121">Per accedere ai consigli di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="2d6c3-122">Una sottoscrizione viene registrata quando il *proprietario della sottoscrizione* avvia il dashboard di Advisor e fa clic sul pulsante **Ottieni raccomandazioni**.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="2d6c3-123">Si tratta di un'*operazione una tantum*.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-123">This is a *one-time operation*.</span></span> <span data-ttu-id="2d6c3-124">Dopo aver registrato una sottoscrizione, è possibile accedere ai consigli di Advisor come *Proprietario*, *Collaboratore* o *Lettore* di una sottoscrizione, di un gruppo di risorse o di una risorsa specifica.</span><span class="sxs-lookup"><span data-stu-id="2d6c3-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d6c3-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d6c3-125">Next steps</span></span>

<span data-ttu-id="2d6c3-126">Per altre informazioni sui consigli di Advisor, vedere:</span><span class="sxs-lookup"><span data-stu-id="2d6c3-126">To learn more about Advisor recommendations, see:</span></span>
* <span data-ttu-id="2d6c3-127">[Introduction to Advisor](advisor-overview.md) (Presentazione di Azure Advisor)</span><span class="sxs-lookup"><span data-stu-id="2d6c3-127">[Introduction to Advisor](advisor-overview.md)</span></span>
* <span data-ttu-id="2d6c3-128">[Get started with Advisor](advisor-get-started.md) (Introduzione ad Advisor)</span><span class="sxs-lookup"><span data-stu-id="2d6c3-128">[Get started with Advisor](advisor-get-started.md)</span></span>
* <span data-ttu-id="2d6c3-129">[Advisor Cost recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sui costi)</span><span class="sxs-lookup"><span data-stu-id="2d6c3-129">[Advisor Cost recommendations](advisor-performance-recommendations.md)</span></span>
* <span data-ttu-id="2d6c3-130">[Advisor Performance recommendations](advisor-performance-recommendations.md) (Consigli di Advisor sulle prestazioni)</span><span class="sxs-lookup"><span data-stu-id="2d6c3-130">[Advisor Performance recommendations](advisor-performance-recommendations.md)</span></span>
* <span data-ttu-id="2d6c3-131">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)</span><span class="sxs-lookup"><span data-stu-id="2d6c3-131">[Advisor High Availability recommendations](advisor-high-availability-recommendations.md)</span></span>


 
