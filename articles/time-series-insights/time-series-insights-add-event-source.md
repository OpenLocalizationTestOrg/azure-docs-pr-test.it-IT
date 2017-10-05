---
title: Aggiungere un'origine evento a un ambiente Azure Time Series Insights | Microsoft Docs
description: In questa esercitazione si connette un'origine evento a un ambiente Time Series Insights
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
ms.openlocfilehash: ffa2eaf3680e68ac14aabf49b6308caeb173fd43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="ba4aa-103">Creare un'origine evento per un ambiente Time Series Insights con il portale di Ibiza</span><span class="sxs-lookup"><span data-stu-id="ba4aa-103">Create an event source for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="ba4aa-104">Un'origine evento di Time Series Insights deriva da un gestore eventi, ad esempio Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="ba4aa-105">Time Series Insights si connette direttamente alle origini evento, inserendo il flusso di dati senza che gli utenti debbano scrivere neppure una riga di codice.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span></span> <span data-ttu-id="ba4aa-106">Time Series Insights supporta attualmente gli hub eventi di Azure e gli hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="ba4aa-107">In futuro verranno aggiunte altre origini evento.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-107">In the future, more Event Sources will be added.</span></span>

## <a name="steps-to-add-an-event-source-to-your-environment"></a><span data-ttu-id="ba4aa-108">Procedura per aggiungere un'origine evento all'ambiente</span><span class="sxs-lookup"><span data-stu-id="ba4aa-108">Steps to add an event source to your environment</span></span>

1.  <span data-ttu-id="ba4aa-109">Accedere al [portale di Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba4aa-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="ba4aa-110">Fare clic su "Tutte le risorse" nel menu sul lato sinistro del portale di Ibiza.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3.  <span data-ttu-id="ba4aa-111">Selezionare l'ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-111">Select your Time Series Insights environment.</span></span>

  ![Creare l'origine evento di Time Series Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="ba4aa-113">Selezionare "Origini evento" e fare clic su "+ Aggiungi".</span><span class="sxs-lookup"><span data-stu-id="ba4aa-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Creare l'origine evento di Time Series Insights: dettagli](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="ba4aa-115">Specificare il nome dell'origine evento.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-115">Specify the name of the event source.</span></span> <span data-ttu-id="ba4aa-116">Questo nome viene associato a tutti gli eventi provenienti dall'origine evento ed è disponibile in fase di query.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="ba4aa-117">Selezionare un hub eventi dall'elenco di risorse di Hub eventi nella sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-117">Select an event hub from the list of Event Hub resources in the current subscription.</span></span> <span data-ttu-id="ba4aa-118">In alternativa scegliere l'opzione di importazione "Specificare le impostazioni dell'hub eventi manualmente" per specificare l'hub eventi di un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-118">Otherwise choose import option "Provide Event Hub settings manually” to specify an event hub in another subscription.</span></span> <span data-ttu-id="ba4aa-119">Gli eventi devono essere pubblicati in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="ba4aa-120">Selezionare i criteri con autorizzazione di lettura nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-120">Select policy that has read permission in the event hub.</span></span>
8.  <span data-ttu-id="ba4aa-121">Specificare il gruppo di consumer dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ba4aa-122">Verificare che questo gruppo di consumer non venga usato da altri servizi, ad esempio un processo di Analisi di flusso o un altro ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="ba4aa-123">Se il gruppo di consumer viene usato da altri servizi, l'operazione di lettura viene compromessa per questo ambiente e per gli altri servizi.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-123">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="ba4aa-124">Se si usa "$Default" come gruppo di consumer, è probabile che venga usato anche da altri lettori.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-124">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

9.  <span data-ttu-id="ba4aa-125">Fare clic su "Crea".</span><span class="sxs-lookup"><span data-stu-id="ba4aa-125">Click “Create.”</span></span>

<span data-ttu-id="ba4aa-126">Dopo la creazione dell'origine evento, Time Series Insights inizierà automaticamente a trasmettere i dati nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="ba4aa-126">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba4aa-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba4aa-127">Next steps</span></span>

* <span data-ttu-id="ba4aa-128">[Inviare eventi](time-series-insights-send-events.md) all'origine evento</span><span class="sxs-lookup"><span data-stu-id="ba4aa-128">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="ba4aa-129">Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ba4aa-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
