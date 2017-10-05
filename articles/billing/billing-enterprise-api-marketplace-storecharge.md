---
title: API per clienti Enterprise per la fatturazione di Azure - Spese per il Marketplace | Microsoft Docs
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
ms.openlocfilehash: 5539623f7ae35e14b6dafe6fdf9efe4bcaba4fd3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="cab33-103">API di creazione report per clienti Enterprise - Spese per il Marketplace Store</span><span class="sxs-lookup"><span data-stu-id="cab33-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="cab33-104">L'API per spese per il Marketplace Store restituisce le spese giornaliere dettagliate in base all'uso correlate al Marketplace per il periodo di fatturazione specificato o per le date di inizio e fine indicate (le spese una tantum non sono incluse).</span><span class="sxs-lookup"><span data-stu-id="cab33-104">The Marketplace Store Charge API returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="cab33-105">Richiesta</span><span class="sxs-lookup"><span data-stu-id="cab33-105">Request</span></span> 
<span data-ttu-id="cab33-106">Le proprietà di intestazione comuni che devono essere aggiunte vengono specificate [qui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="cab33-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="cab33-107">Se non viene specificato alcun periodo di fatturazione, vengono restituiti i dati per il periodo di fatturazione corrente.</span><span class="sxs-lookup"><span data-stu-id="cab33-107">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="cab33-108">Gli intervalli di tempo personalizzati possono essere specificati con i parametri di data di inizio di fine nel formato aaaa-MM-gg e l'intervallo di tempo massimo supportato è 36 mesi.</span><span class="sxs-lookup"><span data-stu-id="cab33-108">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd, the maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="cab33-109">Metodo</span><span class="sxs-lookup"><span data-stu-id="cab33-109">Method</span></span> | <span data-ttu-id="cab33-110">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="cab33-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="cab33-111">GET</span><span class="sxs-lookup"><span data-stu-id="cab33-111">GET</span></span>|<span data-ttu-id="cab33-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="cab33-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="cab33-113">GET</span><span class="sxs-lookup"><span data-stu-id="cab33-113">GET</span></span>|<span data-ttu-id="cab33-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="cab33-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="cab33-115">GET</span><span class="sxs-lookup"><span data-stu-id="cab33-115">GET</span></span>|<span data-ttu-id="cab33-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="cab33-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="cab33-117">Per usare la versione di anteprima dell'API, sostituire v2 con v1 nell'URL precedente.</span><span class="sxs-lookup"><span data-stu-id="cab33-117">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="cab33-118">Response</span><span class="sxs-lookup"><span data-stu-id="cab33-118">Response</span></span>
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

<span data-ttu-id="cab33-119">**Definizioni delle proprietà di risposta**</span><span class="sxs-lookup"><span data-stu-id="cab33-119">**Response property definitions**</span></span>

|<span data-ttu-id="cab33-120">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="cab33-120">Property Name</span></span>| <span data-ttu-id="cab33-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="cab33-121">Type</span></span>| <span data-ttu-id="cab33-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cab33-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="cab33-123">id</span><span class="sxs-lookup"><span data-stu-id="cab33-123">id</span></span>|<span data-ttu-id="cab33-124">string</span><span class="sxs-lookup"><span data-stu-id="cab33-124">string</span></span>|<span data-ttu-id="cab33-125">ID univoco per la voce di spese per il Marketplace</span><span class="sxs-lookup"><span data-stu-id="cab33-125">Unique Id for the marketplace charge item</span></span>|
|<span data-ttu-id="cab33-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="cab33-126">subscriptionGuid</span></span>|<span data-ttu-id="cab33-127">Guid</span><span class="sxs-lookup"><span data-stu-id="cab33-127">Guid</span></span>|<span data-ttu-id="cab33-128">GUID della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="cab33-128">The Subscription Guid</span></span>|
|<span data-ttu-id="cab33-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="cab33-129">subscriptionName</span></span>|<span data-ttu-id="cab33-130">string</span><span class="sxs-lookup"><span data-stu-id="cab33-130">string</span></span>|<span data-ttu-id="cab33-131">Nome della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="cab33-131">The Subscription Name</span></span>|
|<span data-ttu-id="cab33-132">meterId</span><span class="sxs-lookup"><span data-stu-id="cab33-132">meterId</span></span>|<span data-ttu-id="cab33-133">string</span><span class="sxs-lookup"><span data-stu-id="cab33-133">string</span></span>|<span data-ttu-id="cab33-134">ID per il contatore generato</span><span class="sxs-lookup"><span data-stu-id="cab33-134">Id for the emitted Meter</span></span>|
|<span data-ttu-id="cab33-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="cab33-135">usageStartDate</span></span>|<span data-ttu-id="cab33-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="cab33-136">DateTime</span></span>|<span data-ttu-id="cab33-137">Ora di inizio per il record di uso</span><span class="sxs-lookup"><span data-stu-id="cab33-137">Start time for the usage record</span></span>|
|<span data-ttu-id="cab33-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="cab33-138">usageEndDate</span></span>|<span data-ttu-id="cab33-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="cab33-139">DateTime</span></span>|<span data-ttu-id="cab33-140">Ora di fine per il record di uso</span><span class="sxs-lookup"><span data-stu-id="cab33-140">End time for the usage record</span></span>|
|<span data-ttu-id="cab33-141">offerName</span><span class="sxs-lookup"><span data-stu-id="cab33-141">offerName</span></span>|<span data-ttu-id="cab33-142">string</span><span class="sxs-lookup"><span data-stu-id="cab33-142">string</span></span>|<span data-ttu-id="cab33-143">Nome dell'offerta</span><span class="sxs-lookup"><span data-stu-id="cab33-143">The Offer name</span></span>|
|<span data-ttu-id="cab33-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="cab33-144">resourceGroup</span></span>|<span data-ttu-id="cab33-145">string</span><span class="sxs-lookup"><span data-stu-id="cab33-145">string</span></span>|<span data-ttu-id="cab33-146">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="cab33-146">The resource Group</span></span>|
|<span data-ttu-id="cab33-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="cab33-147">instanceId</span></span>|<span data-ttu-id="cab33-148">string</span><span class="sxs-lookup"><span data-stu-id="cab33-148">string</span></span>|<span data-ttu-id="cab33-149">ID istanza</span><span class="sxs-lookup"><span data-stu-id="cab33-149">Instance Id</span></span>|
|<span data-ttu-id="cab33-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="cab33-150">additionalInfo</span></span>|<span data-ttu-id="cab33-151">string</span><span class="sxs-lookup"><span data-stu-id="cab33-151">string</span></span>|<span data-ttu-id="cab33-152">Stringa JSON per informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cab33-152">Additional info JSON string</span></span>|
|<span data-ttu-id="cab33-153">tags</span><span class="sxs-lookup"><span data-stu-id="cab33-153">tags</span></span>|<span data-ttu-id="cab33-154">string</span><span class="sxs-lookup"><span data-stu-id="cab33-154">string</span></span>|<span data-ttu-id="cab33-155">Stringa JSON di tag</span><span class="sxs-lookup"><span data-stu-id="cab33-155">Tag JSON string</span></span>|
|<span data-ttu-id="cab33-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="cab33-156">orderNumber</span></span>|<span data-ttu-id="cab33-157">string</span><span class="sxs-lookup"><span data-stu-id="cab33-157">string</span></span>|<span data-ttu-id="cab33-158">Numero di ordine</span><span class="sxs-lookup"><span data-stu-id="cab33-158">The order number</span></span>|
|<span data-ttu-id="cab33-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="cab33-159">unitOfMeasure</span></span>|<span data-ttu-id="cab33-160">string</span><span class="sxs-lookup"><span data-stu-id="cab33-160">string</span></span>|<span data-ttu-id="cab33-161">Unità di misura per il contatore</span><span class="sxs-lookup"><span data-stu-id="cab33-161">Unit of measure for the meter</span></span>|
|<span data-ttu-id="cab33-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="cab33-162">costCenter</span></span>|<span data-ttu-id="cab33-163">string</span><span class="sxs-lookup"><span data-stu-id="cab33-163">string</span></span>|<span data-ttu-id="cab33-164">Centro di costo</span><span class="sxs-lookup"><span data-stu-id="cab33-164">The cost center</span></span>|
|<span data-ttu-id="cab33-165">accountId</span><span class="sxs-lookup"><span data-stu-id="cab33-165">accountId</span></span>|<span data-ttu-id="cab33-166">int</span><span class="sxs-lookup"><span data-stu-id="cab33-166">int</span></span>|<span data-ttu-id="cab33-167">ID account</span><span class="sxs-lookup"><span data-stu-id="cab33-167">The account Id</span></span>|
|<span data-ttu-id="cab33-168">accountName</span><span class="sxs-lookup"><span data-stu-id="cab33-168">accountName</span></span>|<span data-ttu-id="cab33-169">string</span><span class="sxs-lookup"><span data-stu-id="cab33-169">string</span></span> |<span data-ttu-id="cab33-170">Nome dell'account</span><span class="sxs-lookup"><span data-stu-id="cab33-170">The Account Name</span></span>|
|<span data-ttu-id="cab33-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="cab33-171">accountOwnerId</span></span>|<span data-ttu-id="cab33-172">string</span><span class="sxs-lookup"><span data-stu-id="cab33-172">string</span></span>|<span data-ttu-id="cab33-173">ID del proprietario dell'account</span><span class="sxs-lookup"><span data-stu-id="cab33-173">The Account Owner Id</span></span>|
|<span data-ttu-id="cab33-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="cab33-174">departmentId</span></span>|<span data-ttu-id="cab33-175">int</span><span class="sxs-lookup"><span data-stu-id="cab33-175">int</span></span>|<span data-ttu-id="cab33-176">ID reparto</span><span class="sxs-lookup"><span data-stu-id="cab33-176">The department Id</span></span>|
|<span data-ttu-id="cab33-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="cab33-177">departmentName</span></span>|<span data-ttu-id="cab33-178">string</span><span class="sxs-lookup"><span data-stu-id="cab33-178">string</span></span>|<span data-ttu-id="cab33-179">Nome del reparto</span><span class="sxs-lookup"><span data-stu-id="cab33-179">The department name</span></span>|
|<span data-ttu-id="cab33-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="cab33-180">publisherName</span></span>|<span data-ttu-id="cab33-181">string</span><span class="sxs-lookup"><span data-stu-id="cab33-181">string</span></span>|<span data-ttu-id="cab33-182">Nome del nome dell'autore</span><span class="sxs-lookup"><span data-stu-id="cab33-182">The publisher name</span></span>|
|<span data-ttu-id="cab33-183">planName</span><span class="sxs-lookup"><span data-stu-id="cab33-183">planName</span></span>|<span data-ttu-id="cab33-184">string</span><span class="sxs-lookup"><span data-stu-id="cab33-184">string</span></span>|<span data-ttu-id="cab33-185">Nome del piano</span><span class="sxs-lookup"><span data-stu-id="cab33-185">The Plan name</span></span>|
|<span data-ttu-id="cab33-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="cab33-186">consumedQuantity</span></span>|<span data-ttu-id="cab33-187">decimal</span><span class="sxs-lookup"><span data-stu-id="cab33-187">decimal</span></span>|<span data-ttu-id="cab33-188">Quantità consumata durante il periodo di tempo</span><span class="sxs-lookup"><span data-stu-id="cab33-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="cab33-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="cab33-189">resourceRate</span></span>|<span data-ttu-id="cab33-190">decimal</span><span class="sxs-lookup"><span data-stu-id="cab33-190">decimal</span></span>|<span data-ttu-id="cab33-191">Prezzo unitario per il contatore</span><span class="sxs-lookup"><span data-stu-id="cab33-191">Unit price for the meter</span></span>|
|<span data-ttu-id="cab33-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="cab33-192">extendedCost</span></span>|<span data-ttu-id="cab33-193">decimal</span><span class="sxs-lookup"><span data-stu-id="cab33-193">decimal</span></span>|<span data-ttu-id="cab33-194">Spesa prevista in base alla quantità usata e al costo esteso</span><span class="sxs-lookup"><span data-stu-id="cab33-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="cab33-195">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cab33-195">See also</span></span>

* [<span data-ttu-id="cab33-196">API per periodi di fatturazione</span><span class="sxs-lookup"><span data-stu-id="cab33-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="cab33-197">API per dettagli sull'uso</span><span class="sxs-lookup"><span data-stu-id="cab33-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="cab33-198">API per saldi e riepilogo</span><span class="sxs-lookup"><span data-stu-id="cab33-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="cab33-199">API per l'elenco prezzi</span><span class="sxs-lookup"><span data-stu-id="cab33-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)