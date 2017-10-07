---
title: aaaAzure fatturazione API Enterprise - bilanciamento e riepilogo | Documenti Microsoft
description: Informazioni sull'utilizzo di fatturazione di Azure e APIs RateCard, che sono utilizzati tooprovide approfondite consumo delle risorse di Azure e le tendenze.
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="058b6-103">API di creazione report per clienti Enterprise - Saldi e riepilogo</span><span class="sxs-lookup"><span data-stu-id="058b6-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="058b6-104">Hello bilanciamento e API riepilogo offre un riepilogo di informazioni sulle saldi nuovi acquisti, Azure Marketplace spese, regolazioni e spese eccedenza mensile.</span><span class="sxs-lookup"><span data-stu-id="058b6-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="058b6-105">Richiesta</span><span class="sxs-lookup"><span data-stu-id="058b6-105">Request</span></span> 
<span data-ttu-id="058b6-106">Sono specificate proprietà di intestazione comuni che richiedono toobe aggiunto [qui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="058b6-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="058b6-107">Se non viene specificato un periodo di fatturazione, dati di fatturazione corrente hello periodo viene quindi restituiti.</span><span class="sxs-lookup"><span data-stu-id="058b6-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="058b6-108">Metodo</span><span class="sxs-lookup"><span data-stu-id="058b6-108">Method</span></span> | <span data-ttu-id="058b6-109">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="058b6-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="058b6-110">GET</span><span class="sxs-lookup"><span data-stu-id="058b6-110">GET</span></span>| <span data-ttu-id="058b6-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="058b6-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="058b6-112">GET</span><span class="sxs-lookup"><span data-stu-id="058b6-112">GET</span></span>| <span data-ttu-id="058b6-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="058b6-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="058b6-114">versione di anteprima hello toouse dell'API, sostituire v2 con v1 in hello sopra URL.</span><span class="sxs-lookup"><span data-stu-id="058b6-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="058b6-115">Response</span><span class="sxs-lookup"><span data-stu-id="058b6-115">Response</span></span>

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


<span data-ttu-id="058b6-116">**Definizioni delle proprietà di risposta**</span><span class="sxs-lookup"><span data-stu-id="058b6-116">**Response property definitions**</span></span>

|<span data-ttu-id="058b6-117">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="058b6-117">Property Name</span></span>| <span data-ttu-id="058b6-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="058b6-118">Type</span></span>| <span data-ttu-id="058b6-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="058b6-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="058b6-120">id</span><span class="sxs-lookup"><span data-stu-id="058b6-120">id</span></span>|<span data-ttu-id="058b6-121">string</span><span class="sxs-lookup"><span data-stu-id="058b6-121">string</span></span>|<span data-ttu-id="058b6-122">Hello Id univoco per un determinato periodo di fatturazione e la registrazione</span><span class="sxs-lookup"><span data-stu-id="058b6-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="058b6-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="058b6-123">billingPeriodId</span></span>|<span data-ttu-id="058b6-124">string</span><span class="sxs-lookup"><span data-stu-id="058b6-124">string</span></span> |<span data-ttu-id="058b6-125">ID del periodo di fatturazione Hello</span><span class="sxs-lookup"><span data-stu-id="058b6-125">hello billing period Id</span></span>|
|<span data-ttu-id="058b6-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="058b6-126">currencyCode</span></span>|<span data-ttu-id="058b6-127">string</span><span class="sxs-lookup"><span data-stu-id="058b6-127">string</span></span> |<span data-ttu-id="058b6-128">codice di valuta Hello</span><span class="sxs-lookup"><span data-stu-id="058b6-128">hello currency code</span></span>|
|<span data-ttu-id="058b6-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="058b6-129">beginningBalance</span></span>|<span data-ttu-id="058b6-130">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-130">decimal</span></span>| <span data-ttu-id="058b6-131">Saldo iniziale Hello per periodo di fatturazione hello</span><span class="sxs-lookup"><span data-stu-id="058b6-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="058b6-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="058b6-132">endingBalance</span></span>|<span data-ttu-id="058b6-133">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-133">decimal</span></span>| <span data-ttu-id="058b6-134">Hello saldo finale per periodo di fatturazione hello (per periodi di aprire che questo verrà aggiornato quotidianamente)</span><span class="sxs-lookup"><span data-stu-id="058b6-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="058b6-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="058b6-135">newPurchases</span></span>|<span data-ttu-id="058b6-136">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-136">decimal</span></span>| <span data-ttu-id="058b6-137">Totale nuovo importo di acquisto</span><span class="sxs-lookup"><span data-stu-id="058b6-137">Total new purchase amount</span></span>|
|<span data-ttu-id="058b6-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="058b6-138">adjustments</span></span>|<span data-ttu-id="058b6-139">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-139">decimal</span></span>| <span data-ttu-id="058b6-140">Quantità totale rettificata</span><span class="sxs-lookup"><span data-stu-id="058b6-140">Total adjustment amount</span></span>|
|<span data-ttu-id="058b6-141">utilized</span><span class="sxs-lookup"><span data-stu-id="058b6-141">utilized</span></span>|<span data-ttu-id="058b6-142">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-142">decimal</span></span>| <span data-ttu-id="058b6-143">Uso totale dell'impegno</span><span class="sxs-lookup"><span data-stu-id="058b6-143">Total Commitment usage</span></span>|
|<span data-ttu-id="058b6-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="058b6-144">serviceOverage</span></span>|<span data-ttu-id="058b6-145">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-145">decimal</span></span>| <span data-ttu-id="058b6-146">Eccedenza per i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="058b6-146">Overage for Azure services</span></span>|
|<span data-ttu-id="058b6-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="058b6-147">chargesBilledSeparately</span></span>|<span data-ttu-id="058b6-148">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-148">decimal</span></span>| <span data-ttu-id="058b6-149">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="058b6-149">Charges Billed separately</span></span>|
|<span data-ttu-id="058b6-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="058b6-150">totalOverage</span></span>|<span data-ttu-id="058b6-151">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-151">decimal</span></span>| <span data-ttu-id="058b6-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="058b6-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="058b6-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="058b6-153">totalUsage</span></span>|<span data-ttu-id="058b6-154">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-154">decimal</span></span>| <span data-ttu-id="058b6-155">Eccedenza totale + impegno servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="058b6-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="058b6-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="058b6-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="058b6-157">decimal</span><span class="sxs-lookup"><span data-stu-id="058b6-157">decimal</span></span>| <span data-ttu-id="058b6-158">Spese totali per Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="058b6-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="058b6-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="058b6-159">newPurchasesDetails</span></span>|<span data-ttu-id="058b6-160">Matrice di stringhe JSON di coppie nome-valore</span><span class="sxs-lookup"><span data-stu-id="058b6-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="058b6-161">Elenco di nuovi acquisti</span><span class="sxs-lookup"><span data-stu-id="058b6-161">List of new purchases</span></span>|
|<span data-ttu-id="058b6-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="058b6-162">adjustmentDetails</span></span>|<span data-ttu-id="058b6-163">Matrice di stringhe JSON di coppie nome-valore</span><span class="sxs-lookup"><span data-stu-id="058b6-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="058b6-164">Elenco di modifiche (credito promo, credito SIE e così via)</span><span class="sxs-lookup"><span data-stu-id="058b6-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="058b6-165">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="058b6-165">See also</span></span>

* [<span data-ttu-id="058b6-166">API per periodi di fatturazione</span><span class="sxs-lookup"><span data-stu-id="058b6-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="058b6-167">API per dettagli sull'uso</span><span class="sxs-lookup"><span data-stu-id="058b6-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="058b6-168">API per spese per il Marketplace Store</span><span class="sxs-lookup"><span data-stu-id="058b6-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="058b6-169">API per l'elenco prezzi</span><span class="sxs-lookup"><span data-stu-id="058b6-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)