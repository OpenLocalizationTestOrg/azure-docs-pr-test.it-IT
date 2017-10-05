---
title: API per clienti Enterprise per la fatturazione di Azure - Saldi e riepilogo | Microsoft Docs
description: Informazioni sull'utilizzo dell'API di fatturazione e dell'API RestCard di Azure, utilizzate per offrire informazioni sul consumo di risorse e sulle tendenze di Azure.
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
ms.openlocfilehash: f6b149f0e656d2263705048aa5b644f5bb4a5712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="8f778-103">API di creazione report per clienti Enterprise - Saldi e riepilogo</span><span class="sxs-lookup"><span data-stu-id="8f778-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="8f778-104">L'API per saldi e riepilogo offre un riepilogo mensile delle informazioni su saldi, nuovi acquisti, addebiti per il servizio Azure Marketplace e spese per modifiche e da pagare in eccedenza.</span><span class="sxs-lookup"><span data-stu-id="8f778-104">The Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="8f778-105">Richiesta</span><span class="sxs-lookup"><span data-stu-id="8f778-105">Request</span></span> 
<span data-ttu-id="8f778-106">Le proprietà di intestazione comuni che devono essere aggiunte vengono specificate [qui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="8f778-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="8f778-107">Se non viene specificato alcun periodo di fatturazione, vengono restituiti i dati per il periodo di fatturazione corrente.</span><span class="sxs-lookup"><span data-stu-id="8f778-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="8f778-108">Metodo</span><span class="sxs-lookup"><span data-stu-id="8f778-108">Method</span></span> | <span data-ttu-id="8f778-109">URI della richiesta</span><span class="sxs-lookup"><span data-stu-id="8f778-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="8f778-110">GET</span><span class="sxs-lookup"><span data-stu-id="8f778-110">GET</span></span>| <span data-ttu-id="8f778-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="8f778-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="8f778-112">GET</span><span class="sxs-lookup"><span data-stu-id="8f778-112">GET</span></span>| <span data-ttu-id="8f778-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span><span class="sxs-lookup"><span data-stu-id="8f778-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="8f778-114">Per usare la versione di anteprima dell'API, sostituire v2 con v1 nell'URL precedente.</span><span class="sxs-lookup"><span data-stu-id="8f778-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="8f778-115">Response</span><span class="sxs-lookup"><span data-stu-id="8f778-115">Response</span></span>

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


<span data-ttu-id="8f778-116">**Definizioni delle proprietà di risposta**</span><span class="sxs-lookup"><span data-stu-id="8f778-116">**Response property definitions**</span></span>

|<span data-ttu-id="8f778-117">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="8f778-117">Property Name</span></span>| <span data-ttu-id="8f778-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="8f778-118">Type</span></span>| <span data-ttu-id="8f778-119">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8f778-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="8f778-120">id</span><span class="sxs-lookup"><span data-stu-id="8f778-120">id</span></span>|<span data-ttu-id="8f778-121">string</span><span class="sxs-lookup"><span data-stu-id="8f778-121">string</span></span>|<span data-ttu-id="8f778-122">ID univoco per un periodo di fatturazione e per una registrazione specifici</span><span class="sxs-lookup"><span data-stu-id="8f778-122">The unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="8f778-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="8f778-123">billingPeriodId</span></span>|<span data-ttu-id="8f778-124">string</span><span class="sxs-lookup"><span data-stu-id="8f778-124">string</span></span> |<span data-ttu-id="8f778-125">ID periodo di fatturazione</span><span class="sxs-lookup"><span data-stu-id="8f778-125">The billing period Id</span></span>|
|<span data-ttu-id="8f778-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="8f778-126">currencyCode</span></span>|<span data-ttu-id="8f778-127">string</span><span class="sxs-lookup"><span data-stu-id="8f778-127">string</span></span> |<span data-ttu-id="8f778-128">Codice della valuta</span><span class="sxs-lookup"><span data-stu-id="8f778-128">The currency code</span></span>|
|<span data-ttu-id="8f778-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="8f778-129">beginningBalance</span></span>|<span data-ttu-id="8f778-130">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-130">decimal</span></span>| <span data-ttu-id="8f778-131">Saldo iniziale per il periodo di fatturazione</span><span class="sxs-lookup"><span data-stu-id="8f778-131">The beginning balance for the billing period</span></span>|
|<span data-ttu-id="8f778-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="8f778-132">endingBalance</span></span>|<span data-ttu-id="8f778-133">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-133">decimal</span></span>| <span data-ttu-id="8f778-134">Saldo finale per il periodo di fatturazione (viene aggiornato quotidianamente per i periodi aperti)</span><span class="sxs-lookup"><span data-stu-id="8f778-134">The ending balance for the billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="8f778-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="8f778-135">newPurchases</span></span>|<span data-ttu-id="8f778-136">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-136">decimal</span></span>| <span data-ttu-id="8f778-137">Totale nuovo importo di acquisto</span><span class="sxs-lookup"><span data-stu-id="8f778-137">Total new purchase amount</span></span>|
|<span data-ttu-id="8f778-138">adjustments</span><span class="sxs-lookup"><span data-stu-id="8f778-138">adjustments</span></span>|<span data-ttu-id="8f778-139">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-139">decimal</span></span>| <span data-ttu-id="8f778-140">Quantità totale rettificata</span><span class="sxs-lookup"><span data-stu-id="8f778-140">Total adjustment amount</span></span>|
|<span data-ttu-id="8f778-141">utilized</span><span class="sxs-lookup"><span data-stu-id="8f778-141">utilized</span></span>|<span data-ttu-id="8f778-142">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-142">decimal</span></span>| <span data-ttu-id="8f778-143">Uso totale dell'impegno</span><span class="sxs-lookup"><span data-stu-id="8f778-143">Total Commitment usage</span></span>|
|<span data-ttu-id="8f778-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="8f778-144">serviceOverage</span></span>|<span data-ttu-id="8f778-145">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-145">decimal</span></span>| <span data-ttu-id="8f778-146">Eccedenza per i servizi di Azure</span><span class="sxs-lookup"><span data-stu-id="8f778-146">Overage for Azure services</span></span>|
|<span data-ttu-id="8f778-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="8f778-147">chargesBilledSeparately</span></span>|<span data-ttu-id="8f778-148">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-148">decimal</span></span>| <span data-ttu-id="8f778-149">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="8f778-149">Charges Billed separately</span></span>|
|<span data-ttu-id="8f778-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="8f778-150">totalOverage</span></span>|<span data-ttu-id="8f778-151">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-151">decimal</span></span>| <span data-ttu-id="8f778-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="8f778-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="8f778-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="8f778-153">totalUsage</span></span>|<span data-ttu-id="8f778-154">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-154">decimal</span></span>| <span data-ttu-id="8f778-155">Eccedenza totale + impegno servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="8f778-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="8f778-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="8f778-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="8f778-157">decimal</span><span class="sxs-lookup"><span data-stu-id="8f778-157">decimal</span></span>| <span data-ttu-id="8f778-158">Spese totali per Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8f778-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="8f778-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="8f778-159">newPurchasesDetails</span></span>|<span data-ttu-id="8f778-160">Matrice di stringhe JSON di coppie nome-valore</span><span class="sxs-lookup"><span data-stu-id="8f778-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="8f778-161">Elenco di nuovi acquisti</span><span class="sxs-lookup"><span data-stu-id="8f778-161">List of new purchases</span></span>|
|<span data-ttu-id="8f778-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="8f778-162">adjustmentDetails</span></span>|<span data-ttu-id="8f778-163">Matrice di stringhe JSON di coppie nome-valore</span><span class="sxs-lookup"><span data-stu-id="8f778-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="8f778-164">Elenco di modifiche (credito promo, credito SIE e così via)</span><span class="sxs-lookup"><span data-stu-id="8f778-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="8f778-165">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8f778-165">See also</span></span>

* [<span data-ttu-id="8f778-166">API per periodi di fatturazione</span><span class="sxs-lookup"><span data-stu-id="8f778-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="8f778-167">API per dettagli sull'uso</span><span class="sxs-lookup"><span data-stu-id="8f778-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="8f778-168">API per spese per il Marketplace Store</span><span class="sxs-lookup"><span data-stu-id="8f778-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="8f778-169">API per l'elenco prezzi</span><span class="sxs-lookup"><span data-stu-id="8f778-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)