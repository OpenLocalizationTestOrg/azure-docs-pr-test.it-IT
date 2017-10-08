---
title: un ambiente Azure ora serie Insights aaaCreate | Documenti Microsoft
description: "In questa esercitazione si apprenderà come toocreate ambiente serie, connetterlo origine evento tooan e pronto tooanalyze i dati degli eventi in pochi minuti."
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="90e0c-103">Creare un nuovo ambiente di tempo serie Insights in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="90e0c-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="90e0c-104">L'ambiente Time Series Insights è una risorsa di Azure con capacità di inserimento e archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90e0c-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="90e0c-105">I clienti di effettuare il provisioning ambienti tramite hello portale di Azure con capacità di hello necessario.</span><span class="sxs-lookup"><span data-stu-id="90e0c-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="90e0c-106">Ambiente di hello toocreate passaggi</span><span class="sxs-lookup"><span data-stu-id="90e0c-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="90e0c-107">Seguire questi passaggi toocreate l'ambiente:</span><span class="sxs-lookup"><span data-stu-id="90e0c-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="90e0c-108">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90e0c-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="90e0c-109">Fare clic su hello sul segno più ("+") hello nell'angolo superiore sinistro.</span><span class="sxs-lookup"><span data-stu-id="90e0c-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="90e0c-110">Cercare "Approfondite serie ora" nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="90e0c-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Creare hello ora serie Insights ambiente](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="90e0c-112">Selezionare "Time Series Insights" e fare clic su "Crea".</span><span class="sxs-lookup"><span data-stu-id="90e0c-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Crea gruppo di risorse Insights serie ora hello](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="90e0c-114">Specificare il nome dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="90e0c-114">Specify environment name.</span></span> <span data-ttu-id="90e0c-115">Questo nome rappresenta ambiente hello in [explorer serie tempo](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90e0c-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="90e0c-116">Selezionare una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="90e0c-116">Select a subscription.</span></span> <span data-ttu-id="90e0c-117">Sceglierne una contenente l'origine evento.</span><span class="sxs-lookup"><span data-stu-id="90e0c-117">Choose one that contains your event source.</span></span> <span data-ttu-id="90e0c-118">Tempo serie Insights può rilevare automaticamente IoT Hub di Azure e hello di risorse Hub eventi esistente nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="90e0c-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="90e0c-119">Selezionare o creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="90e0c-119">Select or create a resource group.</span></span> <span data-ttu-id="90e0c-120">Un gruppo di risorse è una raccolta di risorse di Azure usate insieme.</span><span class="sxs-lookup"><span data-stu-id="90e0c-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="90e0c-121">Selezionare un percorso di hosting.</span><span class="sxs-lookup"><span data-stu-id="90e0c-121">Select a hosting location.</span></span> <span data-ttu-id="90e0c-122">tooavoid lo spostamento dei dati tra data center, scegliere la posizione che contiene l'origine evento.</span><span class="sxs-lookup"><span data-stu-id="90e0c-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="90e0c-123">Selezione di un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="90e0c-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="90e0c-124">Selezionare la capacità.</span><span class="sxs-lookup"><span data-stu-id="90e0c-124">Select capacity.</span></span> <span data-ttu-id="90e0c-125">È possibile modificare la capacità di un ambiente dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="90e0c-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="90e0c-126">Creare l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="90e0c-126">Create your environment.</span></span> <span data-ttu-id="90e0c-127">È anche possibile aggiungere il dashboard di toohello di ambiente per facilitare l'accesso ogni volta che accedi.</span><span class="sxs-lookup"><span data-stu-id="90e0c-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Creare hello ora serie Insights pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="90e0c-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90e0c-129">Next steps</span></span>

* <span data-ttu-id="90e0c-130">[Definire i criteri di accesso dati](time-series-insights-data-access.md) tooaccess l'ambiente in [ora serie Insights portale](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="90e0c-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="90e0c-131">Creare un'origine evento</span><span class="sxs-lookup"><span data-stu-id="90e0c-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="90e0c-132">[Invio di eventi](time-series-insights-send-events.md) origine evento toohello</span><span class="sxs-lookup"><span data-stu-id="90e0c-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
