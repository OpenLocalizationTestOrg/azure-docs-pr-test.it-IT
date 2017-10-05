---
title: API per clienti Enterprise per la fatturazione di Azure - Periodi di fatturazione | Microsoft Docs
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
ms.openlocfilehash: c6880b79189e0683387a7aafbd6fa4805b3b42ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="88265-103">API di creazione report per clienti Enterprise - Periodi di fatturazione</span><span class="sxs-lookup"><span data-stu-id="88265-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="88265-104">L'API per periodi di fatturazione restituisce un elenco di periodi di fatturazione contenente i dati sull'uso per la registrazione specificata in ordine cronologico inverso.</span><span class="sxs-lookup"><span data-stu-id="88265-104">The Billing Periods API returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="88265-105">Ogni periodo contiene una proprietà che punta alla route API per i quattro set di dati, ovvero BalanceSummary, UsageDetails, MarketplaceCharges e PriceSheet.</span><span class="sxs-lookup"><span data-stu-id="88265-105">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="88265-106">Se per il periodo non sono presenti dati, la proprietà corrispondente è null.</span><span class="sxs-lookup"><span data-stu-id="88265-106">If the period does not have data, the corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="88265-107">Richiesta</span><span class="sxs-lookup"><span data-stu-id="88265-107">Request</span></span> 
<span data-ttu-id="88265-108">Le proprietà di intestazione comuni che devono essere aggiunte vengono specificate [qui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="88265-108">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="88265-109">Metodo</span><span class="sxs-lookup"><span data-stu-id="88265-109">Method</span></span> | <span data-ttu-id="88265-110">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="88265-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="88265-111">GET</span><span class="sxs-lookup"><span data-stu-id="88265-111">GET</span></span>| <span data-ttu-id="88265-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="88265-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="88265-113">Per usare la versione di anteprima dell'API, sostituire v2 con v1 nell'URL precedente.</span><span class="sxs-lookup"><span data-stu-id="88265-113">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="88265-114">Response</span><span class="sxs-lookup"><span data-stu-id="88265-114">Response</span></span>
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

<span data-ttu-id="88265-115">**Definizioni delle proprietà di risposta**</span><span class="sxs-lookup"><span data-stu-id="88265-115">**Response property definitions**</span></span>

|<span data-ttu-id="88265-116">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="88265-116">Property Name</span></span>| <span data-ttu-id="88265-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="88265-117">Type</span></span>| <span data-ttu-id="88265-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="88265-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="88265-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="88265-119">billingPeriodId</span></span>| <span data-ttu-id="88265-120">string</span><span class="sxs-lookup"><span data-stu-id="88265-120">string</span></span>| <span data-ttu-id="88265-121">ID univoco che rappresenta un determinato periodo di fatturazione</span><span class="sxs-lookup"><span data-stu-id="88265-121">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="88265-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="88265-122">billingStart</span></span>| <span data-ttu-id="88265-123">datetime</span><span class="sxs-lookup"><span data-stu-id="88265-123">datetime</span></span>| <span data-ttu-id="88265-124">Stringa ISO 8601 che rappresenta la data di inizio del periodo</span><span class="sxs-lookup"><span data-stu-id="88265-124">ISO 8601 string representing the period start date</span></span>|
|<span data-ttu-id="88265-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="88265-125">billingEnd</span></span>| <span data-ttu-id="88265-126">datetime</span><span class="sxs-lookup"><span data-stu-id="88265-126">datetime</span></span>| <span data-ttu-id="88265-127">Stringa ISO 8601 che rappresenta la data di fine del periodo</span><span class="sxs-lookup"><span data-stu-id="88265-127">ISO 8601 string representing the period end date</span></span>|
|<span data-ttu-id="88265-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="88265-128">balanceSummary</span></span>| <span data-ttu-id="88265-129">string</span><span class="sxs-lookup"><span data-stu-id="88265-129">string</span></span>| <span data-ttu-id="88265-130">Percorso dell'URL che punta ai dati di riepilogo saldi per il periodo</span><span class="sxs-lookup"><span data-stu-id="88265-130">The URL path that routes to the Balance Summary data for this period</span></span>|
|<span data-ttu-id="88265-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="88265-131">usageDetails</span></span>| <span data-ttu-id="88265-132">string</span><span class="sxs-lookup"><span data-stu-id="88265-132">string</span></span>| <span data-ttu-id="88265-133">Percorso dell'URL che punta ai dati dei dettagli sull'uso per il periodo</span><span class="sxs-lookup"><span data-stu-id="88265-133">The URL path that routes to the Usage Details data for this period</span></span>|
|<span data-ttu-id="88265-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="88265-134">marketplaceCharges</span></span>| <span data-ttu-id="88265-135">string</span><span class="sxs-lookup"><span data-stu-id="88265-135">string</span></span>| <span data-ttu-id="88265-136">Percorso URL che punta ai dati delle spese per il Marketplace per il periodo</span><span class="sxs-lookup"><span data-stu-id="88265-136">The URL path that routes to the Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="88265-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="88265-137">priceSheet</span></span>| <span data-ttu-id="88265-138">string</span><span class="sxs-lookup"><span data-stu-id="88265-138">string</span></span>| <span data-ttu-id="88265-139">Percorso dell'URL che punta ai dati dell'elenco prezzi per il periodo</span><span class="sxs-lookup"><span data-stu-id="88265-139">The URL path that routes to the PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="88265-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="88265-140">See also</span></span>

* [<span data-ttu-id="88265-141">API per saldi e riepilogo</span><span class="sxs-lookup"><span data-stu-id="88265-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="88265-142">API per dettagli sull'uso</span><span class="sxs-lookup"><span data-stu-id="88265-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="88265-143">API per spese per il Marketplace Store</span><span class="sxs-lookup"><span data-stu-id="88265-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="88265-144">API per l'elenco prezzi</span><span class="sxs-lookup"><span data-stu-id="88265-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)