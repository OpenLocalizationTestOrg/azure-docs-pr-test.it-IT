---
title: Come scalare l'ambiente Time Series Insights di Azure | Microsoft Docs
description: Questa esercitazione illustra come scalare l'ambiente Time Series Insights
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 8f6c66ea2173c98179ec899d6626c2ab6f7ec4b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-your-time-series-insights-environment"></a><span data-ttu-id="6ada2-103">Come scalare l'ambiente Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="6ada2-103">How to scale your Time Series Insights environment</span></span>

<span data-ttu-id="6ada2-104">Questa esercitazione illustra come scalare l'ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="6ada2-104">This tutorial covers how to scale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="6ada2-105">La scalabilità verticale tra i tipi di SKU non è consentita.</span><span class="sxs-lookup"><span data-stu-id="6ada2-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="6ada2-106">Un ambiente con uno SKU S1 non può essere convertito in un ambiente S2.</span><span class="sxs-lookup"><span data-stu-id="6ada2-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="6ada2-107">Capacità e velocità di ingresso dello SKU S1</span><span class="sxs-lookup"><span data-stu-id="6ada2-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="6ada2-108">Capacità SKU S1</span><span class="sxs-lookup"><span data-stu-id="6ada2-108">S1 SKU Capacity</span></span> | <span data-ttu-id="6ada2-109">Velocità in ingresso</span><span class="sxs-lookup"><span data-stu-id="6ada2-109">Ingress Rate</span></span> | <span data-ttu-id="6ada2-110">Capacità massima di archiviazione</span><span class="sxs-lookup"><span data-stu-id="6ada2-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="6ada2-111">1</span><span class="sxs-lookup"><span data-stu-id="6ada2-111">1</span></span> | <span data-ttu-id="6ada2-112">1 GB (1 milione di eventi)</span><span class="sxs-lookup"><span data-stu-id="6ada2-112">1 GB (1 million events)</span></span> | <span data-ttu-id="6ada2-113">30 GB (30 milioni di eventi) al mese</span><span class="sxs-lookup"><span data-stu-id="6ada2-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="6ada2-114">10</span><span class="sxs-lookup"><span data-stu-id="6ada2-114">10</span></span> | <span data-ttu-id="6ada2-115">10 GB (10 milioni di eventi)</span><span class="sxs-lookup"><span data-stu-id="6ada2-115">10 GB (10 million events)</span></span> | <span data-ttu-id="6ada2-116">300 GB (300 milioni di eventi) al mese</span><span class="sxs-lookup"><span data-stu-id="6ada2-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="6ada2-117">Capacità e velocità di ingresso dello SKU S2</span><span class="sxs-lookup"><span data-stu-id="6ada2-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="6ada2-118">Capacità SKU S2</span><span class="sxs-lookup"><span data-stu-id="6ada2-118">S2 SKU Capacity</span></span> | <span data-ttu-id="6ada2-119">Velocità in ingresso</span><span class="sxs-lookup"><span data-stu-id="6ada2-119">Ingress Rate</span></span> | <span data-ttu-id="6ada2-120">Capacità massima di archiviazione</span><span class="sxs-lookup"><span data-stu-id="6ada2-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="6ada2-121">1</span><span class="sxs-lookup"><span data-stu-id="6ada2-121">1</span></span> | <span data-ttu-id="6ada2-122">10 GB (10 milioni di eventi)</span><span class="sxs-lookup"><span data-stu-id="6ada2-122">10 GB (10 million events)</span></span> | <span data-ttu-id="6ada2-123">300 GB (300 milioni di eventi) al mese</span><span class="sxs-lookup"><span data-stu-id="6ada2-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="6ada2-124">10</span><span class="sxs-lookup"><span data-stu-id="6ada2-124">10</span></span> | <span data-ttu-id="6ada2-125">100 GB (100 milioni di eventi)</span><span class="sxs-lookup"><span data-stu-id="6ada2-125">100 GB (100 million events)</span></span> | <span data-ttu-id="6ada2-126">3 TB (3 miliardi di eventi) al mese</span><span class="sxs-lookup"><span data-stu-id="6ada2-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="6ada2-127">La capacità ha una scalabilità lineare, pertanto uno SKU S1 con capacità 2 supporta una velocità in ingresso di 2 GB (2 milioni) di eventi al giorno e 60 GB (60 milioni) di eventi al mese.</span><span class="sxs-lookup"><span data-stu-id="6ada2-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-the-capacity-of-your-environment"></a><span data-ttu-id="6ada2-128">Modifica della capacità dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="6ada2-128">Changing the capacity of your environment</span></span>

1. <span data-ttu-id="6ada2-129">Nel portale di Azure selezionare l'ambiente di cui si intende modificare la capacità.</span><span class="sxs-lookup"><span data-stu-id="6ada2-129">In the Azure portal, select the environment whose capacity you want to change.</span></span>
1. <span data-ttu-id="6ada2-130">In Impostazioni fare clic su Configura.</span><span class="sxs-lookup"><span data-stu-id="6ada2-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="6ada2-131">Usare l'apposito dispositivo di scorrimento per selezionare la capacità che soddisfi i requisiti per la velocità in ingresso e la capacità di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6ada2-131">Use the Capacity slider to select the capacity that meets the requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ada2-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6ada2-132">Next steps</span></span>

* <span data-ttu-id="6ada2-133">Verificare che la nuova capacità sia sufficiente a impedire la limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="6ada2-133">Verify that the new capacity is sufficient to prevent throttling.</span></span> <span data-ttu-id="6ada2-134">Per altre informazioni, vedere la sezione *Your environment might be getting throttled* (L'ambiente potrebbe essere soggetto a limitazione delle richieste) [qui](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="6ada2-134">For more details, see the *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>