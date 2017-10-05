---
title: API per clienti Enterprise per la fatturazione di Azure - Elenco prezzi | Microsoft Docs
description: Informazioni sulle API di creazione di report che consentono ai clienti Enterprise di Azure di estrarre i dati sull'uso a livello di codice.
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 2e7d6e883abe4cee13bc5f684baf2a1ea9c6c397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="168fe-103">API di creazione di report per clienti Enterprise - Elenco prezzi</span><span class="sxs-lookup"><span data-stu-id="168fe-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="168fe-104">L'API elenco prezzi offre la tariffa applicabile per ogni contatore per la registrazione e il periodo di fatturazione specificati.</span><span class="sxs-lookup"><span data-stu-id="168fe-104">The Price Sheet API provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="168fe-105">Richiesta</span><span class="sxs-lookup"><span data-stu-id="168fe-105">Request</span></span>
<span data-ttu-id="168fe-106">Le proprietà di intestazione comuni che devono essere aggiunte vengono specificate [qui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="168fe-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="168fe-107">Se non viene specificato alcun periodo di fatturazione, vengono restituiti i dati per il periodo di fatturazione corrente.</span><span class="sxs-lookup"><span data-stu-id="168fe-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="168fe-108">Metodo</span><span class="sxs-lookup"><span data-stu-id="168fe-108">Method</span></span> | <span data-ttu-id="168fe-109">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="168fe-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="168fe-110">GET</span><span class="sxs-lookup"><span data-stu-id="168fe-110">GET</span></span>|<span data-ttu-id="168fe-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="168fe-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="168fe-112">GET</span><span class="sxs-lookup"><span data-stu-id="168fe-112">GET</span></span>|<span data-ttu-id="168fe-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="168fe-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="168fe-114">Per usare la versione di anteprima dell'API, sostituire v2 con v1 nell'URL precedente.</span><span class="sxs-lookup"><span data-stu-id="168fe-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="168fe-115">Response</span><span class="sxs-lookup"><span data-stu-id="168fe-115">Response</span></span>

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
><span data-ttu-id="168fe-116">Se si usa la versione di anteprima dell'API, il campo meterId non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="168fe-116">If you are using the Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="168fe-117">**Definizioni delle proprietà di risposta**</span><span class="sxs-lookup"><span data-stu-id="168fe-117">**Response property definitions**</span></span>

|<span data-ttu-id="168fe-118">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="168fe-118">Property Name</span></span>| <span data-ttu-id="168fe-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="168fe-119">Type</span></span>| <span data-ttu-id="168fe-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="168fe-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="168fe-121">id</span><span class="sxs-lookup"><span data-stu-id="168fe-121">id</span></span>| <span data-ttu-id="168fe-122">string</span><span class="sxs-lookup"><span data-stu-id="168fe-122">string</span></span>| <span data-ttu-id="168fe-123">ID univoco che rappresenta un particolare elemento PriceSheet (contatore per periodo di fatturazione)</span><span class="sxs-lookup"><span data-stu-id="168fe-123">The unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="168fe-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="168fe-124">billingPeriodId</span></span>| <span data-ttu-id="168fe-125">string</span><span class="sxs-lookup"><span data-stu-id="168fe-125">string</span></span>| <span data-ttu-id="168fe-126">ID univoco che rappresenta un determinato periodo di fatturazione</span><span class="sxs-lookup"><span data-stu-id="168fe-126">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="168fe-127">meterId</span><span class="sxs-lookup"><span data-stu-id="168fe-127">meterId</span></span>| <span data-ttu-id="168fe-128">string</span><span class="sxs-lookup"><span data-stu-id="168fe-128">string</span></span>| <span data-ttu-id="168fe-129">Identificatore del contatore.</span><span class="sxs-lookup"><span data-stu-id="168fe-129">The identifier for the meter.</span></span> <span data-ttu-id="168fe-130">Può essere mappato al campo meterId.</span><span class="sxs-lookup"><span data-stu-id="168fe-130">It can be mapped to the usage meterId.</span></span>|
|<span data-ttu-id="168fe-131">meterName</span><span class="sxs-lookup"><span data-stu-id="168fe-131">meterName</span></span>| <span data-ttu-id="168fe-132">string</span><span class="sxs-lookup"><span data-stu-id="168fe-132">string</span></span>| <span data-ttu-id="168fe-133">Nome del contatore</span><span class="sxs-lookup"><span data-stu-id="168fe-133">The meter name</span></span>|
|<span data-ttu-id="168fe-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="168fe-134">unitOfMeasure</span></span>| <span data-ttu-id="168fe-135">string</span><span class="sxs-lookup"><span data-stu-id="168fe-135">string</span></span>| <span data-ttu-id="168fe-136">Unità di misura per misurare il servizio</span><span class="sxs-lookup"><span data-stu-id="168fe-136">The Unit of Measure for measuring the service</span></span>|
|<span data-ttu-id="168fe-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="168fe-137">includedQuantity</span></span>| <span data-ttu-id="168fe-138">decimal</span><span class="sxs-lookup"><span data-stu-id="168fe-138">decimal</span></span>| <span data-ttu-id="168fe-139">Quantità inclusa</span><span class="sxs-lookup"><span data-stu-id="168fe-139">Quantity that is included</span></span> |
|<span data-ttu-id="168fe-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="168fe-140">partNumber</span></span>| <span data-ttu-id="168fe-141">string</span><span class="sxs-lookup"><span data-stu-id="168fe-141">string</span></span>| <span data-ttu-id="168fe-142">Numero di parte associato al contatore</span><span class="sxs-lookup"><span data-stu-id="168fe-142">The part number associated with the Meter</span></span>|
|<span data-ttu-id="168fe-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="168fe-143">unitPrice</span></span>| <span data-ttu-id="168fe-144">decimal</span><span class="sxs-lookup"><span data-stu-id="168fe-144">decimal</span></span>| <span data-ttu-id="168fe-145">Prezzo unitario per il contatore</span><span class="sxs-lookup"><span data-stu-id="168fe-145">The unit price for the meter</span></span>|
|<span data-ttu-id="168fe-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="168fe-146">currencyCode</span></span>| <span data-ttu-id="168fe-147">string</span><span class="sxs-lookup"><span data-stu-id="168fe-147">string</span></span>| <span data-ttu-id="168fe-148">Codice della valuta per l'elemento unitPrice</span><span class="sxs-lookup"><span data-stu-id="168fe-148">The currency code for the unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="168fe-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="168fe-149">See also</span></span>

* [<span data-ttu-id="168fe-150">API per periodi di fatturazione</span><span class="sxs-lookup"><span data-stu-id="168fe-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="168fe-151">API per dettagli sull'uso</span><span class="sxs-lookup"><span data-stu-id="168fe-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="168fe-152">API per saldi e riepilogo</span><span class="sxs-lookup"><span data-stu-id="168fe-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="168fe-153">API per spese per il Marketplace Store</span><span class="sxs-lookup"><span data-stu-id="168fe-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
