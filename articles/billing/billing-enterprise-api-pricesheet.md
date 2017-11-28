---
title: aaaAzure fatturazione API Enterprise - PriceSheet | Documenti Microsoft
description: Informazioni sulle API di creazione di report che consentono di dati relativi al consumo toopull clienti Azure Enterprise a livello di codice hello.
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="ec18a-103">API di creazione di report per clienti Enterprise - Elenco prezzi</span><span class="sxs-lookup"><span data-stu-id="ec18a-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="ec18a-104">Hello prezzo foglio API fornisce tasso hello per ogni misuratore di hello dato periodo di fatturazione e di registrazione.</span><span class="sxs-lookup"><span data-stu-id="ec18a-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="ec18a-105">Richiesta</span><span class="sxs-lookup"><span data-stu-id="ec18a-105">Request</span></span>
<span data-ttu-id="ec18a-106">Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="ec18a-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="ec18a-107">Se non viene specificato un periodo di fatturazione, dati di fatturazione corrente hello periodo viene quindi restituiti.</span><span class="sxs-lookup"><span data-stu-id="ec18a-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="ec18a-108">Metodo</span><span class="sxs-lookup"><span data-stu-id="ec18a-108">Method</span></span> | <span data-ttu-id="ec18a-109">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="ec18a-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="ec18a-110">GET</span><span class="sxs-lookup"><span data-stu-id="ec18a-110">GET</span></span>|<span data-ttu-id="ec18a-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="ec18a-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="ec18a-112">GET</span><span class="sxs-lookup"><span data-stu-id="ec18a-112">GET</span></span>|<span data-ttu-id="ec18a-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span><span class="sxs-lookup"><span data-stu-id="ec18a-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="ec18a-114">versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.</span><span class="sxs-lookup"><span data-stu-id="ec18a-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="ec18a-115">Response</span><span class="sxs-lookup"><span data-stu-id="ec18a-115">Response</span></span>

    
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
><span data-ttu-id="ec18a-116">Se si utilizza hello anteprima API, il campo ID misuratore non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="ec18a-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="ec18a-117">**Definizioni delle proprietà di risposta**</span><span class="sxs-lookup"><span data-stu-id="ec18a-117">**Response property definitions**</span></span>

|<span data-ttu-id="ec18a-118">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="ec18a-118">Property Name</span></span>| <span data-ttu-id="ec18a-119">Tipo</span><span class="sxs-lookup"><span data-stu-id="ec18a-119">Type</span></span>| <span data-ttu-id="ec18a-120">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ec18a-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="ec18a-121">id</span><span class="sxs-lookup"><span data-stu-id="ec18a-121">id</span></span>| <span data-ttu-id="ec18a-122">string</span><span class="sxs-lookup"><span data-stu-id="ec18a-122">string</span></span>| <span data-ttu-id="ec18a-123">Hello Id univoco che rappresenta un particolare elemento PriceSheet (misuratore dal periodo di fatturazione)</span><span class="sxs-lookup"><span data-stu-id="ec18a-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="ec18a-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="ec18a-124">billingPeriodId</span></span>| <span data-ttu-id="ec18a-125">string</span><span class="sxs-lookup"><span data-stu-id="ec18a-125">string</span></span>| <span data-ttu-id="ec18a-126">Hello Id univoco che rappresenta un determinato periodo di fatturazione</span><span class="sxs-lookup"><span data-stu-id="ec18a-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="ec18a-127">meterId</span><span class="sxs-lookup"><span data-stu-id="ec18a-127">meterId</span></span>| <span data-ttu-id="ec18a-128">string</span><span class="sxs-lookup"><span data-stu-id="ec18a-128">string</span></span>| <span data-ttu-id="ec18a-129">Identificatore Hello misuratore hello.</span><span class="sxs-lookup"><span data-stu-id="ec18a-129">hello identifier for hello meter.</span></span> <span data-ttu-id="ec18a-130">Può essere mappato toohello ID misuratore di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="ec18a-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="ec18a-131">meterName</span><span class="sxs-lookup"><span data-stu-id="ec18a-131">meterName</span></span>| <span data-ttu-id="ec18a-132">string</span><span class="sxs-lookup"><span data-stu-id="ec18a-132">string</span></span>| <span data-ttu-id="ec18a-133">nome del misuratore Hello</span><span class="sxs-lookup"><span data-stu-id="ec18a-133">hello meter name</span></span>|
|<span data-ttu-id="ec18a-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="ec18a-134">unitOfMeasure</span></span>| <span data-ttu-id="ec18a-135">string</span><span class="sxs-lookup"><span data-stu-id="ec18a-135">string</span></span>| <span data-ttu-id="ec18a-136">Hello unità di misura per la misurazione servizio hello</span><span class="sxs-lookup"><span data-stu-id="ec18a-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="ec18a-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="ec18a-137">includedQuantity</span></span>| <span data-ttu-id="ec18a-138">decimal</span><span class="sxs-lookup"><span data-stu-id="ec18a-138">decimal</span></span>| <span data-ttu-id="ec18a-139">Quantità inclusa</span><span class="sxs-lookup"><span data-stu-id="ec18a-139">Quantity that is included</span></span> |
|<span data-ttu-id="ec18a-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="ec18a-140">partNumber</span></span>| <span data-ttu-id="ec18a-141">string</span><span class="sxs-lookup"><span data-stu-id="ec18a-141">string</span></span>| <span data-ttu-id="ec18a-142">numero di parte Hello associato hello misuratore</span><span class="sxs-lookup"><span data-stu-id="ec18a-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="ec18a-143">unitPrice</span><span class="sxs-lookup"><span data-stu-id="ec18a-143">unitPrice</span></span>| <span data-ttu-id="ec18a-144">decimal</span><span class="sxs-lookup"><span data-stu-id="ec18a-144">decimal</span></span>| <span data-ttu-id="ec18a-145">prezzo unitario Hello per metro hello</span><span class="sxs-lookup"><span data-stu-id="ec18a-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="ec18a-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="ec18a-146">currencyCode</span></span>| <span data-ttu-id="ec18a-147">string</span><span class="sxs-lookup"><span data-stu-id="ec18a-147">string</span></span>| <span data-ttu-id="ec18a-148">codice di valuta Hello per unitPrice hello</span><span class="sxs-lookup"><span data-stu-id="ec18a-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="ec18a-149">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ec18a-149">See also</span></span>

* [<span data-ttu-id="ec18a-150">API per periodi di fatturazione</span><span class="sxs-lookup"><span data-stu-id="ec18a-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="ec18a-151">API per dettagli sull'uso</span><span class="sxs-lookup"><span data-stu-id="ec18a-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="ec18a-152">API per saldi e riepilogo</span><span class="sxs-lookup"><span data-stu-id="ec18a-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="ec18a-153">API per spese per il Marketplace Store</span><span class="sxs-lookup"><span data-stu-id="ec18a-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
