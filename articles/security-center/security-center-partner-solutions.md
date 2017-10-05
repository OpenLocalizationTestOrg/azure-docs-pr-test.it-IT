---
title: Gestione delle soluzioni dei partner nel Centro sicurezza di Azure | Microsoft Docs
description: "Questo documento descrive in modo dettagliato il modo in cui il Centro sicurezza di Azure permette di monitorare in modo immediato lo stato di integrità delle soluzioni dei partner integrate nella sottoscrizione di Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: 2ebb930e877c5027f4d7b0a316a7f5ebe84471b1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="9beba-103">Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="9beba-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="9beba-104">Questo documento contiene informazioni dettagliate su come monitorare lo stato di integrità delle soluzioni dei partner nel Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="9beba-104">This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="9beba-105">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="9beba-105">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="9beba-106">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="9beba-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="9beba-107">Monitoraggio delle soluzioni dei partner</span><span class="sxs-lookup"><span data-stu-id="9beba-107">Monitoring partner solutions</span></span>
<span data-ttu-id="9beba-108">Il riquadro **Soluzioni partner** nel pannello **Centro sicurezza** permette di monitorare in modo immediato lo stato di integrità delle soluzioni dei partner integrate nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9beba-108">The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Riquadro Soluzioni partner][1]

<span data-ttu-id="9beba-110">Il riquadro **Soluzioni partner** mostra il numero di soluzioni dei partner integrate con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9beba-110">The **Partner solutions** tile displays the number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="9beba-111">Se non sono presenti soluzioni integrate, il riquadro visualizza il numero zero.</span><span class="sxs-lookup"><span data-stu-id="9beba-111">If there are no solutions integrated, the tile displays the number zero.</span></span>

<span data-ttu-id="9beba-112">Per visualizzare l'integrità delle soluzioni dei partner:</span><span class="sxs-lookup"><span data-stu-id="9beba-112">To view the health of your partner solutions:</span></span>

1. <span data-ttu-id="9beba-113">Selezionare il riquadro **Soluzioni partner** .</span><span class="sxs-lookup"><span data-stu-id="9beba-113">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="9beba-114">Viene visualizzato il pannello **Soluzioni partner** con un elenco di soluzioni dei partner connesse al Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9beba-114">The **Partner solutions** blade opens displaying a list of your partner solutions connected to Security Center.</span></span>

   ![Soluzioni partner][3]

   <span data-ttu-id="9beba-116">Una soluzione partner può avere uno degli stati seguenti:</span><span class="sxs-lookup"><span data-stu-id="9beba-116">The status of a partner solution can be:</span></span>

   * <span data-ttu-id="9beba-117">Protetto (verde): nessun problema di integrità.</span><span class="sxs-lookup"><span data-stu-id="9beba-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="9beba-118">Danneggiato (rosso): è presente un problema di integrità che richiede attenzione immediata.</span><span class="sxs-lookup"><span data-stu-id="9beba-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="9beba-119">Segnalazione arrestata (arancione): la soluzione ha arrestato la segnalazione dello stato di integrità.</span><span class="sxs-lookup"><span data-stu-id="9beba-119">Stopped reporting (orange) - the solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="9beba-120">Sconosciuto (arancione): l'integrità della soluzione è attualmente sconosciuta, a causa di un processo di aggiunta di una nuova risorsa alla soluzione esistente non riuscito.</span><span class="sxs-lookup"><span data-stu-id="9beba-120">Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.</span></span>
   * <span data-ttu-id="9beba-121">Non segnalato (grigio): la soluzione non ha ancora inviato alcuna segnalazione. Lo stato di una soluzione può non essere segnalato se la soluzione è stata connessa recentemente ed è ancora in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9beba-121">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="9beba-122">Selezionare una soluzione dei partner.</span><span class="sxs-lookup"><span data-stu-id="9beba-122">Select a partner solution.</span></span> <span data-ttu-id="9beba-123">In questo esempio viene selezionata la soluzione **Qualys**.</span><span class="sxs-lookup"><span data-stu-id="9beba-123">In this example, lets select the **Qualys** solution.</span></span>  <span data-ttu-id="9beba-124">Viene visualizzato un pannello che mostra che lo stato della soluzione partner e le risorse associate alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="9beba-124">A blade opens showing you the status of the partner solution and the solution's associated resources.</span></span> <span data-ttu-id="9beba-125">Selezionare **Console della soluzione** per aprire l'esperienza di gestione dei partner per questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="9beba-125">Select **Solution console** to open the partner management experience for this solution.</span></span>

   ![Dettagli della soluzione di un partner][4]
3. <span data-ttu-id="9beba-127">Tornare al pannello **Qualys** e selezionare **Collega la macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="9beba-127">Go back to the **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="9beba-128">Verrà visualizzato il pannello **Collega applicazioni** .</span><span class="sxs-lookup"><span data-stu-id="9beba-128">The **Link Applications** blade opens.</span></span> <span data-ttu-id="9beba-129">In questo pannello è possibile connettere risorse alla soluzione del partner.</span><span class="sxs-lookup"><span data-stu-id="9beba-129">Here you can connect resources to the partner solution.</span></span>

   ![Collegare risorse alla soluzione di un partner][5]

## <a name="next-steps"></a><span data-ttu-id="9beba-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9beba-131">Next steps</span></span>
<span data-ttu-id="9beba-132">Questo documento ha presentato il riquadro **Soluzioni partner** del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9beba-132">In this document, you were introduced to the **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="9beba-133">Per altre informazioni sul Centro sicurezza, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="9beba-133">To learn more about Security Center, see the following articles:</span></span>

* <span data-ttu-id="9beba-134">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9beba-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9beba-135">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni facilitano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9beba-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9beba-136">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9beba-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="9beba-137">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9beba-137">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="9beba-138">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="9beba-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9beba-139">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="9beba-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
