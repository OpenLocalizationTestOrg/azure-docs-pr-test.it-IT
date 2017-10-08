---
title: un ambiente di Azure ora serie Insights tooyour origine evento aaaAdd | Documenti Microsoft
description: In questa esercitazione, si connette un ambiente di tempo serie Insights tooyour origine evento
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="fd0e9-103">Creare un'origine evento per l'ambiente di tempo serie Insights utilizzando portale Ibiza hello</span><span class="sxs-lookup"><span data-stu-id="fd0e9-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="fd0e9-104">Un'origine evento di Time Series Insights deriva da un gestore eventi, ad esempio Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="fd0e9-105">Tempo serie Insights si connette direttamente origini tooEvent, l'inserimento di flusso di dati hello senza richiedere agli utenti toowrite una singola riga di codice.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="fd0e9-106">Time Series Insights supporta attualmente gli hub eventi di Azure e gli hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="fd0e9-107">In futuro hello, verranno aggiunte altre origini di eventi.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="fd0e9-108">Passaggi tooadd un ambiente di tooyour origine evento</span><span class="sxs-lookup"><span data-stu-id="fd0e9-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="fd0e9-109">Accedi toohello [portale Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd0e9-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="fd0e9-110">Fare clic su "Tutte le risorse" nel menu hello sul lato sinistro di hello del portale Ibiza hello.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="fd0e9-111">Selezionare l'ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-111">Select your Time Series Insights environment.</span></span>

  ![Creare origine evento di hello ora serie Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="fd0e9-113">Selezionare "Origini evento" e fare clic su "+ Aggiungi".</span><span class="sxs-lookup"><span data-stu-id="fd0e9-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Creare origine evento di Insights serie ora hello - dettagli](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="fd0e9-115">Specificare il nome di hello dell'origine evento hello.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="fd0e9-116">Questo nome viene associato a tutti gli eventi provenienti dall'origine evento ed è disponibile in fase di query.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="fd0e9-117">Selezionare un hub eventi hello elenco di risorse Hub eventi nella sottoscrizione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="fd0e9-118">In caso contrario scegliere l'opzione di importazione "le impostazioni dell'Hub di eventi di fornire manualmente" toospecify un hub di eventi in un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="fd0e9-119">Gli eventi devono essere pubblicati in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="fd0e9-120">Selezionare i criteri che dispone dell'autorizzazione in hub eventi hello lettura.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="fd0e9-121">Specificare il gruppo di consumer dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="fd0e9-122">Verificare che questo gruppo di consumer non venga usato da altri servizi, ad esempio un processo di Analisi di flusso o un altro ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="fd0e9-123">Se il gruppo di consumer viene utilizzato da altri servizi, leggere influisce negativamente l'operazione per questo ambiente e hello altri servizi.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="fd0e9-124">Se si utilizza "$Default" come gruppo di consumer hello, può causare il riutilizzo toopotential dagli altri reader.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="fd0e9-125">Fare clic su "Crea".</span><span class="sxs-lookup"><span data-stu-id="fd0e9-125">Click “Create.”</span></span>

<span data-ttu-id="fd0e9-126">Dopo la creazione dell'origine evento hello, ora serie Insights verrà automaticamente avviato il flusso di dati nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="fd0e9-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd0e9-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd0e9-127">Next steps</span></span>

* <span data-ttu-id="fd0e9-128">[Invio di eventi](time-series-insights-send-events.md) origine evento toohello</span><span class="sxs-lookup"><span data-stu-id="fd0e9-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="fd0e9-129">Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="fd0e9-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
