---
title: aaaAzure API Enterprise fatturazione - spese Marketplace | Documenti Microsoft
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="b2124-103">API di creazione report per clienti Enterprise - Spese per il Marketplace Store</span><span class="sxs-lookup"><span data-stu-id="b2124-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="b2124-104">Hello Marketplace archivio addebito API restituisce hello basata sull'utilizzo di marketplace addebiti suddivisione giorno per hello specificato il periodo di fatturazione o date di inizio e fine (non sono inclusi i costi di una volta).</span><span class="sxs-lookup"><span data-stu-id="b2124-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="b2124-105">Richiesta</span><span class="sxs-lookup"><span data-stu-id="b2124-105">Request</span></span> 
<span data-ttu-id="b2124-106">Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="b2124-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="b2124-107">Se non viene specificato un periodo di fatturazione, dati di fatturazione corrente hello periodo viene quindi restituiti.</span><span class="sxs-lookup"><span data-stu-id="b2124-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="b2124-108">Gli intervalli di tempo personalizzato possono essere specificati con inizio hello e terminano i parametri di data che sono in fase di hello formato AAAA-MM-GG, hello massimo supportato è compreso tra 36 mesi.</span><span class="sxs-lookup"><span data-stu-id="b2124-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="b2124-109">Metodo</span><span class="sxs-lookup"><span data-stu-id="b2124-109">Method</span></span> | <span data-ttu-id="b2124-110">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="b2124-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="b2124-111">GET</span><span class="sxs-lookup"><span data-stu-id="b2124-111">GET</span></span>|<span data-ttu-id="b2124-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="b2124-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="b2124-113">GET</span><span class="sxs-lookup"><span data-stu-id="b2124-113">GET</span></span>|<span data-ttu-id="b2124-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="b2124-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="b2124-115">GET</span><span class="sxs-lookup"><span data-stu-id="b2124-115">GET</span></span>|<span data-ttu-id="b2124-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span><span class="sxs-lookup"><span data-stu-id="b2124-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="b2124-117">versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.</span><span class="sxs-lookup"><span data-stu-id="b2124-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="b2124-118">Response</span><span class="sxs-lookup"><span data-stu-id="b2124-118">Response</span></span>
 
    
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
    

<span data-ttu-id="b2124-119">**Definizioni delle proprietà di risposta**</span><span class="sxs-lookup"><span data-stu-id="b2124-119">**Response property definitions**</span></span>

|<span data-ttu-id="b2124-120">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="b2124-120">Property Name</span></span>| <span data-ttu-id="b2124-121">Tipo</span><span class="sxs-lookup"><span data-stu-id="b2124-121">Type</span></span>| <span data-ttu-id="b2124-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b2124-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="b2124-123">id</span><span class="sxs-lookup"><span data-stu-id="b2124-123">id</span></span>|<span data-ttu-id="b2124-124">string</span><span class="sxs-lookup"><span data-stu-id="b2124-124">string</span></span>|<span data-ttu-id="b2124-125">Id univoco per l'elemento di addebito hello marketplace</span><span class="sxs-lookup"><span data-stu-id="b2124-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="b2124-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="b2124-126">subscriptionGuid</span></span>|<span data-ttu-id="b2124-127">Guid</span><span class="sxs-lookup"><span data-stu-id="b2124-127">Guid</span></span>|<span data-ttu-id="b2124-128">Hello Guid della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="b2124-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="b2124-129">subscriptionName</span><span class="sxs-lookup"><span data-stu-id="b2124-129">subscriptionName</span></span>|<span data-ttu-id="b2124-130">string</span><span class="sxs-lookup"><span data-stu-id="b2124-130">string</span></span>|<span data-ttu-id="b2124-131">Nome della sottoscrizione Hello</span><span class="sxs-lookup"><span data-stu-id="b2124-131">hello Subscription Name</span></span>|
|<span data-ttu-id="b2124-132">meterId</span><span class="sxs-lookup"><span data-stu-id="b2124-132">meterId</span></span>|<span data-ttu-id="b2124-133">string</span><span class="sxs-lookup"><span data-stu-id="b2124-133">string</span></span>|<span data-ttu-id="b2124-134">ID per hello generato misuratore</span><span class="sxs-lookup"><span data-stu-id="b2124-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="b2124-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="b2124-135">usageStartDate</span></span>|<span data-ttu-id="b2124-136">DateTime</span><span class="sxs-lookup"><span data-stu-id="b2124-136">DateTime</span></span>|<span data-ttu-id="b2124-137">Ora di inizio per i record di utilizzo hello</span><span class="sxs-lookup"><span data-stu-id="b2124-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="b2124-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="b2124-138">usageEndDate</span></span>|<span data-ttu-id="b2124-139">DateTime</span><span class="sxs-lookup"><span data-stu-id="b2124-139">DateTime</span></span>|<span data-ttu-id="b2124-140">Ora di fine per il record di utilizzo hello</span><span class="sxs-lookup"><span data-stu-id="b2124-140">End time for hello usage record</span></span>|
|<span data-ttu-id="b2124-141">offerName</span><span class="sxs-lookup"><span data-stu-id="b2124-141">offerName</span></span>|<span data-ttu-id="b2124-142">string</span><span class="sxs-lookup"><span data-stu-id="b2124-142">string</span></span>|<span data-ttu-id="b2124-143">nome dell'offerta Hello</span><span class="sxs-lookup"><span data-stu-id="b2124-143">hello Offer name</span></span>|
|<span data-ttu-id="b2124-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="b2124-144">resourceGroup</span></span>|<span data-ttu-id="b2124-145">string</span><span class="sxs-lookup"><span data-stu-id="b2124-145">string</span></span>|<span data-ttu-id="b2124-146">risorsa Hello gruppo</span><span class="sxs-lookup"><span data-stu-id="b2124-146">hello resource Group</span></span>|
|<span data-ttu-id="b2124-147">instanceId</span><span class="sxs-lookup"><span data-stu-id="b2124-147">instanceId</span></span>|<span data-ttu-id="b2124-148">string</span><span class="sxs-lookup"><span data-stu-id="b2124-148">string</span></span>|<span data-ttu-id="b2124-149">ID istanza</span><span class="sxs-lookup"><span data-stu-id="b2124-149">Instance Id</span></span>|
|<span data-ttu-id="b2124-150">additionalInfo</span><span class="sxs-lookup"><span data-stu-id="b2124-150">additionalInfo</span></span>|<span data-ttu-id="b2124-151">string</span><span class="sxs-lookup"><span data-stu-id="b2124-151">string</span></span>|<span data-ttu-id="b2124-152">Stringa JSON per informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b2124-152">Additional info JSON string</span></span>|
|<span data-ttu-id="b2124-153">tags</span><span class="sxs-lookup"><span data-stu-id="b2124-153">tags</span></span>|<span data-ttu-id="b2124-154">string</span><span class="sxs-lookup"><span data-stu-id="b2124-154">string</span></span>|<span data-ttu-id="b2124-155">Stringa JSON di tag</span><span class="sxs-lookup"><span data-stu-id="b2124-155">Tag JSON string</span></span>|
|<span data-ttu-id="b2124-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="b2124-156">orderNumber</span></span>|<span data-ttu-id="b2124-157">string</span><span class="sxs-lookup"><span data-stu-id="b2124-157">string</span></span>|<span data-ttu-id="b2124-158">numero di ordine Hello</span><span class="sxs-lookup"><span data-stu-id="b2124-158">hello order number</span></span>|
|<span data-ttu-id="b2124-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="b2124-159">unitOfMeasure</span></span>|<span data-ttu-id="b2124-160">string</span><span class="sxs-lookup"><span data-stu-id="b2124-160">string</span></span>|<span data-ttu-id="b2124-161">Unità di misura del misuratore hello</span><span class="sxs-lookup"><span data-stu-id="b2124-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="b2124-162">costCenter</span><span class="sxs-lookup"><span data-stu-id="b2124-162">costCenter</span></span>|<span data-ttu-id="b2124-163">string</span><span class="sxs-lookup"><span data-stu-id="b2124-163">string</span></span>|<span data-ttu-id="b2124-164">centro di costo Hello</span><span class="sxs-lookup"><span data-stu-id="b2124-164">hello cost center</span></span>|
|<span data-ttu-id="b2124-165">accountId</span><span class="sxs-lookup"><span data-stu-id="b2124-165">accountId</span></span>|<span data-ttu-id="b2124-166">int</span><span class="sxs-lookup"><span data-stu-id="b2124-166">int</span></span>|<span data-ttu-id="b2124-167">account Hello Id</span><span class="sxs-lookup"><span data-stu-id="b2124-167">hello account Id</span></span>|
|<span data-ttu-id="b2124-168">accountName</span><span class="sxs-lookup"><span data-stu-id="b2124-168">accountName</span></span>|<span data-ttu-id="b2124-169">string</span><span class="sxs-lookup"><span data-stu-id="b2124-169">string</span></span> |<span data-ttu-id="b2124-170">Nome dell'Account Hello</span><span class="sxs-lookup"><span data-stu-id="b2124-170">hello Account Name</span></span>|
|<span data-ttu-id="b2124-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="b2124-171">accountOwnerId</span></span>|<span data-ttu-id="b2124-172">string</span><span class="sxs-lookup"><span data-stu-id="b2124-172">string</span></span>|<span data-ttu-id="b2124-173">Hello Id proprietario di Account</span><span class="sxs-lookup"><span data-stu-id="b2124-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="b2124-174">departmentId</span><span class="sxs-lookup"><span data-stu-id="b2124-174">departmentId</span></span>|<span data-ttu-id="b2124-175">int</span><span class="sxs-lookup"><span data-stu-id="b2124-175">int</span></span>|<span data-ttu-id="b2124-176">reparto di Hello Id</span><span class="sxs-lookup"><span data-stu-id="b2124-176">hello department Id</span></span>|
|<span data-ttu-id="b2124-177">departmentName</span><span class="sxs-lookup"><span data-stu-id="b2124-177">departmentName</span></span>|<span data-ttu-id="b2124-178">string</span><span class="sxs-lookup"><span data-stu-id="b2124-178">string</span></span>|<span data-ttu-id="b2124-179">nome del reparto Hello</span><span class="sxs-lookup"><span data-stu-id="b2124-179">hello department name</span></span>|
|<span data-ttu-id="b2124-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="b2124-180">publisherName</span></span>|<span data-ttu-id="b2124-181">string</span><span class="sxs-lookup"><span data-stu-id="b2124-181">string</span></span>|<span data-ttu-id="b2124-182">nome dell'autore Hello</span><span class="sxs-lookup"><span data-stu-id="b2124-182">hello publisher name</span></span>|
|<span data-ttu-id="b2124-183">planName</span><span class="sxs-lookup"><span data-stu-id="b2124-183">planName</span></span>|<span data-ttu-id="b2124-184">string</span><span class="sxs-lookup"><span data-stu-id="b2124-184">string</span></span>|<span data-ttu-id="b2124-185">nome del piano di Hello</span><span class="sxs-lookup"><span data-stu-id="b2124-185">hello Plan name</span></span>|
|<span data-ttu-id="b2124-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="b2124-186">consumedQuantity</span></span>|<span data-ttu-id="b2124-187">decimal</span><span class="sxs-lookup"><span data-stu-id="b2124-187">decimal</span></span>|<span data-ttu-id="b2124-188">Quantità consumata durante il periodo di tempo</span><span class="sxs-lookup"><span data-stu-id="b2124-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="b2124-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="b2124-189">resourceRate</span></span>|<span data-ttu-id="b2124-190">decimal</span><span class="sxs-lookup"><span data-stu-id="b2124-190">decimal</span></span>|<span data-ttu-id="b2124-191">Prezzo unitario per metro hello</span><span class="sxs-lookup"><span data-stu-id="b2124-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="b2124-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="b2124-192">extendedCost</span></span>|<span data-ttu-id="b2124-193">decimal</span><span class="sxs-lookup"><span data-stu-id="b2124-193">decimal</span></span>|<span data-ttu-id="b2124-194">Spesa prevista in base alla quantità usata e al costo esteso</span><span class="sxs-lookup"><span data-stu-id="b2124-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="b2124-195">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b2124-195">See also</span></span>

* [<span data-ttu-id="b2124-196">API per periodi di fatturazione</span><span class="sxs-lookup"><span data-stu-id="b2124-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="b2124-197">API per dettagli sull'uso</span><span class="sxs-lookup"><span data-stu-id="b2124-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="b2124-198">API per saldi e riepilogo</span><span class="sxs-lookup"><span data-stu-id="b2124-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="b2124-199">API per l'elenco prezzi</span><span class="sxs-lookup"><span data-stu-id="b2124-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)