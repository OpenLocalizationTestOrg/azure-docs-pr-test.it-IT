---
title: "Monitorare l'integrità delle risorse della rete CDN di Azure | Documentazione Microsoft"
description: "Informazioni su come monitorare l'integrità delle risorse della rete CDN di Azure con Integrità risorse di Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="bf060-103">Monitorare l'integrità delle risorse della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="bf060-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="bf060-104">L'integrità delle risorse della rete CDN di Azure costituisce un sottoinsieme di [Integrità risorse di Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf060-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="bf060-105">È possibile usare Integrità risorse di Azure per monitorare l'integrità delle risorse della rete CDN e ricevere indicazioni pratiche per risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="bf060-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="bf060-106">L'integrità delle risorse della rete CDN di Azure attualmente riguarda solo l'integrità delle funzionalità API e di distribuzione della rete CDN globale.</span><span class="sxs-lookup"><span data-stu-id="bf060-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="bf060-107">Non vengono verificati i singoli endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="bf060-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="bf060-108">I segnali che indicano l'integrità delle risorse della rete CDN di Azure possono presentare ritardi fino a 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="bf060-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="bf060-109">Come trovare l'integrità delle risorse della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="bf060-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="bf060-110">Nel [portale di Azure](https://portal.azure.com) passare al profilo CDN.</span><span class="sxs-lookup"><span data-stu-id="bf060-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="bf060-111">Fare clic sul pulsante **Settings** .</span><span class="sxs-lookup"><span data-stu-id="bf060-111">Click the **Settings** button.</span></span>

    ![Pulsante Impostazioni](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="bf060-113">In *Supporto e risoluzione dei problemi* fare clic su **Integrità risorsa**.</span><span class="sxs-lookup"><span data-stu-id="bf060-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Integrità delle risorse della rete CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="bf060-115">Le risorse della rete CDN sono elencate anche nel riquadro *Integrità risorsa* del pannello *Guida e supporto*.</span><span class="sxs-lookup"><span data-stu-id="bf060-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="bf060-116">È possibile accedere rapidamente a *Guida e supporto* facendo clic sul punto interrogativo (**?**) cerchiato</span><span class="sxs-lookup"><span data-stu-id="bf060-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="bf060-117">nell'angolo superiore destro del portale.</span><span class="sxs-lookup"><span data-stu-id="bf060-117">in the upper right corner of the portal.</span></span>
>
> ![Guida e supporto](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="bf060-119">Messaggi specifici della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="bf060-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="bf060-120">Di seguito sono riportati gli stati correlati all'integrità delle risorse della rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="bf060-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="bf060-121">Messaggio</span><span class="sxs-lookup"><span data-stu-id="bf060-121">Message</span></span> | <span data-ttu-id="bf060-122">Azione consigliata</span><span class="sxs-lookup"><span data-stu-id="bf060-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="bf060-123">Uno o più endpoint di rete CDN potrebbero essere stati arrestati, rimossi o configurati in modo non corretto</span><span class="sxs-lookup"><span data-stu-id="bf060-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="bf060-124">Uno o più endpoint di rete CDN potrebbero essere stati arrestati, rimossi o configurati in modo non corretto.</span><span class="sxs-lookup"><span data-stu-id="bf060-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="bf060-125">Il servizio di gestione della rete CDN non è attualmente disponibile</span><span class="sxs-lookup"><span data-stu-id="bf060-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="bf060-126">Visualizzare di nuovo questa pagina per eventuali aggiornamenti dello stato. Se il problema persiste anche dopo l'ora di risoluzione prevista, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="bf060-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="bf060-127">Gli endpoint di rete CDN potrebbero essere interessati dai problemi in corso con alcuni provider di servizi di rete CDN</span><span class="sxs-lookup"><span data-stu-id="bf060-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="bf060-128">Visualizzare di nuovo questa pagina per eventuali aggiornamenti dello stato. Usare lo strumento per la risoluzione dei problemi per informazioni su come testare l'origine e l'endpoint di rete CDN. Se il problema persiste anche dopo l'ora di risoluzione prevista, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="bf060-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="bf060-129">Sono stati riscontrati ritardi di propagazione delle modifiche di configurazione agli endpoint di rete CDN</span><span class="sxs-lookup"><span data-stu-id="bf060-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="bf060-130">Visualizzare di nuovo questa pagina per eventuali aggiornamenti dello stato. Se le modifiche di configurazione non vengono propagate completamente entro il tempo previsto, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="bf060-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="bf060-131">Sono stati riscontrati problemi durante il caricamento del portale supplementare</span><span class="sxs-lookup"><span data-stu-id="bf060-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="bf060-132">Visualizzare di nuovo questa pagina per eventuali aggiornamenti dello stato. Se il problema persiste anche dopo l'ora di risoluzione prevista, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="bf060-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="bf060-133">Sono stati riscontrati problemi con alcuni provider di servizi di rete CDN</span><span class="sxs-lookup"><span data-stu-id="bf060-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="bf060-134">Visualizzare di nuovo questa pagina per eventuali aggiornamenti dello stato. Se il problema persiste anche dopo l'ora di risoluzione prevista, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="bf060-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bf060-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf060-135">Next steps</span></span>

- [<span data-ttu-id="bf060-136">Panoramica su Integrità risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="bf060-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="bf060-137">Risolvere i problemi di compressione della rete CDN</span><span class="sxs-lookup"><span data-stu-id="bf060-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="bf060-138">Risolvere i problemi relativi a errori 404</span><span class="sxs-lookup"><span data-stu-id="bf060-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)