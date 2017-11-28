---
title: aaaHow tooscale ambiente Azure ora serie Insights | Documenti Microsoft
description: Questa esercitazione sono trattati come tooscale l'ambiente Azure ora serie Insights
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
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="2483f-103">Come tooscale ambiente ora serie Insights</span><span class="sxs-lookup"><span data-stu-id="2483f-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="2483f-104">Questa esercitazione sono trattati come tooscale ambiente ora serie Insights.</span><span class="sxs-lookup"><span data-stu-id="2483f-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="2483f-105">La scalabilità verticale tra i tipi di SKU non è consentita.</span><span class="sxs-lookup"><span data-stu-id="2483f-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="2483f-106">Un ambiente con uno SKU S1 non può essere convertito in un ambiente S2.</span><span class="sxs-lookup"><span data-stu-id="2483f-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="2483f-107">Capacità e velocità di ingresso dello SKU S1</span><span class="sxs-lookup"><span data-stu-id="2483f-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="2483f-108">Capacità SKU S1</span><span class="sxs-lookup"><span data-stu-id="2483f-108">S1 SKU Capacity</span></span> | <span data-ttu-id="2483f-109">Velocità in ingresso</span><span class="sxs-lookup"><span data-stu-id="2483f-109">Ingress Rate</span></span> | <span data-ttu-id="2483f-110">Capacità massima di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2483f-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="2483f-111">1</span><span class="sxs-lookup"><span data-stu-id="2483f-111">1</span></span> | <span data-ttu-id="2483f-112">1 GB (1 milione di eventi)</span><span class="sxs-lookup"><span data-stu-id="2483f-112">1 GB (1 million events)</span></span> | <span data-ttu-id="2483f-113">30 GB (30 milioni di eventi) al mese</span><span class="sxs-lookup"><span data-stu-id="2483f-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="2483f-114">10</span><span class="sxs-lookup"><span data-stu-id="2483f-114">10</span></span> | <span data-ttu-id="2483f-115">10 GB (10 milioni di eventi)</span><span class="sxs-lookup"><span data-stu-id="2483f-115">10 GB (10 million events)</span></span> | <span data-ttu-id="2483f-116">300 GB (300 milioni di eventi) al mese</span><span class="sxs-lookup"><span data-stu-id="2483f-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="2483f-117">Capacità e velocità di ingresso dello SKU S2</span><span class="sxs-lookup"><span data-stu-id="2483f-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="2483f-118">Capacità SKU S2</span><span class="sxs-lookup"><span data-stu-id="2483f-118">S2 SKU Capacity</span></span> | <span data-ttu-id="2483f-119">Velocità in ingresso</span><span class="sxs-lookup"><span data-stu-id="2483f-119">Ingress Rate</span></span> | <span data-ttu-id="2483f-120">Capacità massima di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2483f-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="2483f-121">1</span><span class="sxs-lookup"><span data-stu-id="2483f-121">1</span></span> | <span data-ttu-id="2483f-122">10 GB (10 milioni di eventi)</span><span class="sxs-lookup"><span data-stu-id="2483f-122">10 GB (10 million events)</span></span> | <span data-ttu-id="2483f-123">300 GB (300 milioni di eventi) al mese</span><span class="sxs-lookup"><span data-stu-id="2483f-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="2483f-124">10</span><span class="sxs-lookup"><span data-stu-id="2483f-124">10</span></span> | <span data-ttu-id="2483f-125">100 GB (100 milioni di eventi)</span><span class="sxs-lookup"><span data-stu-id="2483f-125">100 GB (100 million events)</span></span> | <span data-ttu-id="2483f-126">3 TB (3 miliardi di eventi) al mese</span><span class="sxs-lookup"><span data-stu-id="2483f-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="2483f-127">La capacità ha una scalabilità lineare, pertanto uno SKU S1 con capacità 2 supporta una velocità in ingresso di 2 GB (2 milioni) di eventi al giorno e 60 GB (60 milioni) di eventi al mese.</span><span class="sxs-lookup"><span data-stu-id="2483f-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="2483f-128">Capacità di hello dell'ambiente di modifica</span><span class="sxs-lookup"><span data-stu-id="2483f-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="2483f-129">Nel portale di Azure hello, selezionare hello ambiente la cui capacità desiderate toochange.</span><span class="sxs-lookup"><span data-stu-id="2483f-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="2483f-130">In Impostazioni fare clic su Configura.</span><span class="sxs-lookup"><span data-stu-id="2483f-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="2483f-131">Utilizzare hello capacità dispositivo di scorrimento tooselect hello capacità che soddisfa i requisiti di hello per le tariffe in ingresso e la capacità di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2483f-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2483f-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2483f-132">Next steps</span></span>

* <span data-ttu-id="2483f-133">Verificare che sia sufficiente nuova capacità di hello tooprevent la limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="2483f-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="2483f-134">Per ulteriori informazioni, vedere hello *ambiente potrebbe essere recupero limitata* sezione [qui](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="2483f-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
