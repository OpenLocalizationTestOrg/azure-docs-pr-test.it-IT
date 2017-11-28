---
title: aaaAzure fatturazione API Enterprise - periodi di fatturazione | Documenti Microsoft
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="9b295-103">API di creazione report per clienti Enterprise - Periodi di fatturazione</span><span class="sxs-lookup"><span data-stu-id="9b295-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="9b295-104">API di periodi di fatturazione Hello restituisce un elenco di fatturazione periodi che dispongono di dati di utilizzo per hello specificato registrazione in ordine cronologico inverso.</span><span class="sxs-lookup"><span data-stu-id="9b295-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="9b295-105">Ogni periodo contiene una proprietà che punta route API toohello per quattro set di dati - BalanceSummary, UsageDetails, gli addebiti Marktplace e PriceSheet di hello.</span><span class="sxs-lookup"><span data-stu-id="9b295-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="9b295-106">Se il periodo di hello non dispone di dati, la proprietà corrispondente hello è null.</span><span class="sxs-lookup"><span data-stu-id="9b295-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="9b295-107">Richiesta</span><span class="sxs-lookup"><span data-stu-id="9b295-107">Request</span></span> 
<span data-ttu-id="9b295-108">Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="9b295-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="9b295-109">Metodo</span><span class="sxs-lookup"><span data-stu-id="9b295-109">Method</span></span> | <span data-ttu-id="9b295-110">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="9b295-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="9b295-111">GET</span><span class="sxs-lookup"><span data-stu-id="9b295-111">GET</span></span>| <span data-ttu-id="9b295-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span><span class="sxs-lookup"><span data-stu-id="9b295-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="9b295-113">versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.</span><span class="sxs-lookup"><span data-stu-id="9b295-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="9b295-114">Response</span><span class="sxs-lookup"><span data-stu-id="9b295-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="9b295-115">**Definizioni delle proprietà di risposta**</span><span class="sxs-lookup"><span data-stu-id="9b295-115">**Response property definitions**</span></span>

|<span data-ttu-id="9b295-116">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="9b295-116">Property Name</span></span>| <span data-ttu-id="9b295-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="9b295-117">Type</span></span>| <span data-ttu-id="9b295-118">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9b295-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="9b295-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="9b295-119">billingPeriodId</span></span>| <span data-ttu-id="9b295-120">string</span><span class="sxs-lookup"><span data-stu-id="9b295-120">string</span></span>| <span data-ttu-id="9b295-121">Hello Id univoco che rappresenta un determinato periodo di fatturazione</span><span class="sxs-lookup"><span data-stu-id="9b295-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="9b295-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="9b295-122">billingStart</span></span>| <span data-ttu-id="9b295-123">datetime</span><span class="sxs-lookup"><span data-stu-id="9b295-123">datetime</span></span>| <span data-ttu-id="9b295-124">Stringa ISO 8601 che rappresenta la data di inizio periodo hello</span><span class="sxs-lookup"><span data-stu-id="9b295-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="9b295-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="9b295-125">billingEnd</span></span>| <span data-ttu-id="9b295-126">datetime</span><span class="sxs-lookup"><span data-stu-id="9b295-126">datetime</span></span>| <span data-ttu-id="9b295-127">Stringa ISO 8601 che rappresenta la data di fine periodo hello</span><span class="sxs-lookup"><span data-stu-id="9b295-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="9b295-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="9b295-128">balanceSummary</span></span>| <span data-ttu-id="9b295-129">string</span><span class="sxs-lookup"><span data-stu-id="9b295-129">string</span></span>| <span data-ttu-id="9b295-130">percorso URL Hello che indirizza i dati di riepilogo saldi toohello per questo periodo</span><span class="sxs-lookup"><span data-stu-id="9b295-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="9b295-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="9b295-131">usageDetails</span></span>| <span data-ttu-id="9b295-132">string</span><span class="sxs-lookup"><span data-stu-id="9b295-132">string</span></span>| <span data-ttu-id="9b295-133">percorso URL Hello che indirizza i dati di utilizzo dettagli toohello per questo periodo</span><span class="sxs-lookup"><span data-stu-id="9b295-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="9b295-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="9b295-134">marketplaceCharges</span></span>| <span data-ttu-id="9b295-135">string</span><span class="sxs-lookup"><span data-stu-id="9b295-135">string</span></span>| <span data-ttu-id="9b295-136">percorso URL Hello che indirizza i dati di Marketplace addebiti toohello per questo periodo</span><span class="sxs-lookup"><span data-stu-id="9b295-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="9b295-137">priceSheet</span><span class="sxs-lookup"><span data-stu-id="9b295-137">priceSheet</span></span>| <span data-ttu-id="9b295-138">string</span><span class="sxs-lookup"><span data-stu-id="9b295-138">string</span></span>| <span data-ttu-id="9b295-139">percorso URL Hello che indirizza i dati di PriceSheet toohello per questo periodo</span><span class="sxs-lookup"><span data-stu-id="9b295-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="9b295-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9b295-140">See also</span></span>

* [<span data-ttu-id="9b295-141">API per saldi e riepilogo</span><span class="sxs-lookup"><span data-stu-id="9b295-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="9b295-142">API per dettagli sull'uso</span><span class="sxs-lookup"><span data-stu-id="9b295-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="9b295-143">API per spese per il Marketplace Store</span><span class="sxs-lookup"><span data-stu-id="9b295-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="9b295-144">API per l'elenco prezzi</span><span class="sxs-lookup"><span data-stu-id="9b295-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)