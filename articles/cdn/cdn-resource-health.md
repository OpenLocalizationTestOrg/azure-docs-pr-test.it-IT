---
title: "integrità hello aaaMonitor delle risorse di rete CDN di Azure | Documenti Microsoft"
description: "Informazioni su come toomonitor hello integrità delle risorse di rete CDN di Azure utilizzando l'integrità delle risorse di Azure."
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
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="09697-103">Monitoraggio integrità hello delle risorse di rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="09697-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="09697-104">L'integrità delle risorse della rete CDN di Azure costituisce un sottoinsieme di [Integrità risorse di Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="09697-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="09697-105">È possibile utilizzare risorse di Azure toomonitor hello dell'integrità delle risorse di rete CDN e ricevere problemi tootroubleshoot Guida.</span><span class="sxs-lookup"><span data-stu-id="09697-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="09697-106">Integrità delle risorse della rete CDN di Azure attualmente solo account per l'integrità di hello di recapito della rete CDN globale e delle funzionalità dell'API.</span><span class="sxs-lookup"><span data-stu-id="09697-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="09697-107">Non vengono verificati i singoli endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="09697-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="09697-108">Segnala Hello che feed integrità delle risorse di rete CDN di Azure può essere up too15 minuti di ritardo.</span><span class="sxs-lookup"><span data-stu-id="09697-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="09697-109">Come toofind integrità delle risorse di rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="09697-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="09697-110">In hello [portale di Azure](https://portal.azure.com), selezionare il profilo CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="09697-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="09697-111">Fare clic su hello **impostazioni** pulsante.</span><span class="sxs-lookup"><span data-stu-id="09697-111">Click hello **Settings** button.</span></span>

    ![Pulsante Impostazioni](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="09697-113">In *Supporto e risoluzione dei problemi* fare clic su **Integrità risorsa**.</span><span class="sxs-lookup"><span data-stu-id="09697-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Integrità delle risorse della rete CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="09697-115">È anche possibile trovare le risorse di rete CDN nell'hello *integrità delle risorse* riquadro in hello *Guida e supporto* blade.</span><span class="sxs-lookup"><span data-stu-id="09697-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="09697-116">È possibile ottenere rapidamente troppo*Guida e supporto* facendo hello cerchiato **?**</span><span class="sxs-lookup"><span data-stu-id="09697-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="09697-117">in hello alto a destra del portale hello.</span><span class="sxs-lookup"><span data-stu-id="09697-117">in hello upper right corner of hello portal.</span></span>
>
> ![Guida e supporto tecnico](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="09697-119">Messaggi specifici della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="09697-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="09697-120">Integrità delle risorse della rete CDN tooAzure correlati stati può trovarsi sotto.</span><span class="sxs-lookup"><span data-stu-id="09697-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="09697-121">Message</span><span class="sxs-lookup"><span data-stu-id="09697-121">Message</span></span> | <span data-ttu-id="09697-122">Azione consigliata</span><span class="sxs-lookup"><span data-stu-id="09697-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="09697-123">Uno o più endpoint di rete CDN potrebbero essere stati arrestati, rimossi o configurati in modo non corretto</span><span class="sxs-lookup"><span data-stu-id="09697-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="09697-124">Uno o più endpoint di rete CDN potrebbero essere stati arrestati, rimossi o configurati in modo non corretto.</span><span class="sxs-lookup"><span data-stu-id="09697-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="09697-125">Siamo spiacenti, non è attualmente disponibile hello servizio di gestione della rete CDN</span><span class="sxs-lookup"><span data-stu-id="09697-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="09697-126">Fare nuovamente clic qui per gli aggiornamenti di stato. Se il problema persiste dopo hello prevede tempi di risoluzione, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="09697-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="09697-127">Gli endpoint di rete CDN potrebbero essere interessati dai problemi in corso con alcuni provider di servizi di rete CDN</span><span class="sxs-lookup"><span data-stu-id="09697-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="09697-128">Fare nuovamente clic qui per gli aggiornamenti di stato. Utilizzare la modalità toolearn strumento di risoluzione dei problemi hello tootest l'origine e l'endpoint rete CDN. Se il problema persiste dopo hello prevede tempi di risoluzione, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="09697-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="09697-129">Sono stati riscontrati ritardi di propagazione delle modifiche di configurazione agli endpoint di rete CDN</span><span class="sxs-lookup"><span data-stu-id="09697-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="09697-130">Fare nuovamente clic qui per gli aggiornamenti di stato. Se le modifiche di configurazione non vengono propagate completamente nel tempo previsto di hello, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="09697-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="09697-131">Siamo spiacenti, che si sono verificati problemi durante il caricamento portale supplementare hello</span><span class="sxs-lookup"><span data-stu-id="09697-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="09697-132">Fare nuovamente clic qui per gli aggiornamenti di stato. Se il problema persiste dopo hello prevede tempi di risoluzione, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="09697-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="09697-133">Sono stati riscontrati problemi con alcuni provider di servizi di rete CDN</span><span class="sxs-lookup"><span data-stu-id="09697-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="09697-134">Fare nuovamente clic qui per gli aggiornamenti di stato. Se il problema persiste dopo hello prevede tempi di risoluzione, contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="09697-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="09697-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09697-135">Next steps</span></span>

- [<span data-ttu-id="09697-136">Panoramica su Integrità risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="09697-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="09697-137">Risolvere i problemi di compressione della rete CDN</span><span class="sxs-lookup"><span data-stu-id="09697-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="09697-138">Risolvere i problemi relativi a errori 404</span><span class="sxs-lookup"><span data-stu-id="09697-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)