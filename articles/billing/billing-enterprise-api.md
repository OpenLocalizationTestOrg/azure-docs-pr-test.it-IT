---
title: API per clienti Enterprise per la fatturazione di Azure | Microsoft Docs
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
ms.openlocfilehash: e3a5f9bcd6b54a51c29df649f1ae8ac185b153a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="d5bb8-103">Panoramica delle API di creazione di report per i clienti Enterprise</span><span class="sxs-lookup"><span data-stu-id="d5bb8-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="d5bb8-104">Le API di creazione di report consentono ai clienti Enterprise di Azure di estrarre i dati di fatturazione e sull'uso a livello di codice per inserirli negli strumenti di analisi preferiti.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-104">The Reporting APIs enable Enterprise Azure customers to programmatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-to-the-api"></a><span data-ttu-id="d5bb8-105">Abilitazione dell'API per l'accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="d5bb8-105">Enabling data access to the API</span></span>
* <span data-ttu-id="d5bb8-106">**Generare o recuperare la chiave API**: accedere a Enterprise Portal e seguire l'esercitazione disponibile nella sezione della Guida relativa alle API di creazione di report.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-106">**Generate or retrieve the API key** - Log in to the Enterprise portal and follow the tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="d5bb8-107">La prima sezione in tale articolo illustra come generare o recuperare la chiave API per la registrazione specificata.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-107">The first section under this help article explains how to generate or retrieve the API key for the specified enrollment.</span></span>
* <span data-ttu-id="d5bb8-108">**Passare le chiavi nell'API** - La chiave API deve essere passata per ogni chiamata per l'autenticazione e l'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-108">**Passing keys in the API** - The API key needs to be passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="d5bb8-109">La proprietà seguente deve essere passata alle intestazioni HTTP:</span><span class="sxs-lookup"><span data-stu-id="d5bb8-109">The following property needs to be to the HTTP headers</span></span>

|<span data-ttu-id="d5bb8-110">Chiave intestazione necessaria</span><span class="sxs-lookup"><span data-stu-id="d5bb8-110">Request Header Key</span></span> | <span data-ttu-id="d5bb8-111">Valore</span><span class="sxs-lookup"><span data-stu-id="d5bb8-111">Value</span></span>|
|-|-|
|<span data-ttu-id="d5bb8-112">Authorization</span><span class="sxs-lookup"><span data-stu-id="d5bb8-112">Authorization</span></span>| <span data-ttu-id="d5bb8-113">Specificare il valore nel formato: **bearer {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="d5bb8-113">Specify the value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="d5bb8-114">Esempio: bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="d5bb8-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="d5bb8-115">API per l'uso</span><span class="sxs-lookup"><span data-stu-id="d5bb8-115">Consumption APIs</span></span>
<span data-ttu-id="d5bb8-116">Per le API descritte di seguito, [qui](https://consumption.azure.com/swagger/ui/index) è disponibile un endpoint Swagger che deve consentire una facile analisi dell'API e la possibilità di generare SDK client tramite [AutoRest](https://github.com/Azure/AutoRest) o [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="d5bb8-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for the APIs described below which should enable easy introspection of the API and the ability to generate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="d5bb8-117">I dati a partire dal 1° maggio 2014 sono disponibili tramite questa API.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="d5bb8-118">**Saldi e riepilogo** - L'[API per saldi e riepilogo](billing-enterprise-api-balance-summary.md) offre un riepilogo mensile delle informazioni su saldi, nuovi acquisti, addebiti per il servizio Azure Marketplace e spese per modifiche e da pagare in eccedenza.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-118">**Balance and Summary** - The [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="d5bb8-119">**Dettagli sull'uso** - L'[API per dettagli sull'uso](billing-enterprise-api-usage-detail.md) offre un'analisi giornaliera dettagliata delle quantità usate e delle spese stimate in relazione a una registrazione.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-119">**Usage Details** - The [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="d5bb8-120">Il risultato include anche informazioni su istanze, contatori e reparti.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-120">The result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="d5bb8-121">Le query sull'API possono essere eseguite in base al periodo di fatturazione oppure in base a un intervallo definito da date di inizio e di fine specificate.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-121">The API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="d5bb8-122">**Spese per Marketplace Store** - L'[API per spese per il Marketplace Store](billing-enterprise-api-marketplace-storecharge.md) restituisce le spese giornaliere dettagliate in base all'uso correlate al Marketplace per il periodo di fatturazione specificato o per le date di inizio e fine indicate (le spese una tantum non sono incluse).</span><span class="sxs-lookup"><span data-stu-id="d5bb8-122">**Marketplace Store Charge** - The [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="d5bb8-123">**Elenco prezzi** - L'[API elenco prezzi](billing-enterprise-api-pricesheet.md) offre la tariffa applicabile per ogni contatore per la registrazione e il periodo di fatturazione specificati.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-123">**Price Sheet** - The [Price Sheet API](billing-enterprise-api-pricesheet.md) provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="d5bb8-124">API di supporto</span><span class="sxs-lookup"><span data-stu-id="d5bb8-124">Helper APIs</span></span>
 <span data-ttu-id="d5bb8-125">**Elenco periodi di fatturazione** - L'[API per periodi di fatturazione](billing-enterprise-api-billing-periods.md) restituisce un elenco di periodi di fatturazione contenente i dati sull'uso per la registrazione specificata in ordine cronologico inverso.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-125">**List Billing Periods** - The [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for the specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="d5bb8-126">Ogni periodo contiene una proprietà che punta alla route API per i quattro set di dati, ovvero BalanceSummary, UsageDetails, MarketplaceCharges e PriceSheet.</span><span class="sxs-lookup"><span data-stu-id="d5bb8-126">Each Period contains a property pointing to the API route for the four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="d5bb8-127">Codici di risposta dell'API</span><span class="sxs-lookup"><span data-stu-id="d5bb8-127">API Response Codes</span></span>  
|<span data-ttu-id="d5bb8-128">Codice di stato della risposta</span><span class="sxs-lookup"><span data-stu-id="d5bb8-128">Response Status Code</span></span>|<span data-ttu-id="d5bb8-129">Message</span><span class="sxs-lookup"><span data-stu-id="d5bb8-129">Message</span></span>|<span data-ttu-id="d5bb8-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5bb8-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="d5bb8-131">200</span><span class="sxs-lookup"><span data-stu-id="d5bb8-131">200</span></span>| <span data-ttu-id="d5bb8-132">OK</span><span class="sxs-lookup"><span data-stu-id="d5bb8-132">OK</span></span>|<span data-ttu-id="d5bb8-133">Nessun errore</span><span class="sxs-lookup"><span data-stu-id="d5bb8-133">No error</span></span>|
|<span data-ttu-id="d5bb8-134">401</span><span class="sxs-lookup"><span data-stu-id="d5bb8-134">401</span></span>| <span data-ttu-id="d5bb8-135">Non autorizzata</span><span class="sxs-lookup"><span data-stu-id="d5bb8-135">Unauthorized</span></span>| <span data-ttu-id="d5bb8-136">Chiave API non trovata, non valida, scaduta e così via</span><span class="sxs-lookup"><span data-stu-id="d5bb8-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="d5bb8-137">404</span><span class="sxs-lookup"><span data-stu-id="d5bb8-137">404</span></span>| <span data-ttu-id="d5bb8-138">Non disponibile</span><span class="sxs-lookup"><span data-stu-id="d5bb8-138">Unavailable</span></span>| <span data-ttu-id="d5bb8-139">Endpoint del report non trovato</span><span class="sxs-lookup"><span data-stu-id="d5bb8-139">Report endpoint not found</span></span>|
|<span data-ttu-id="d5bb8-140">400</span><span class="sxs-lookup"><span data-stu-id="d5bb8-140">400</span></span>| <span data-ttu-id="d5bb8-141">Bad Request</span><span class="sxs-lookup"><span data-stu-id="d5bb8-141">Bad Request</span></span>| <span data-ttu-id="d5bb8-142">Parametri non validi (intervalli di date, numeri EA e così via)</span><span class="sxs-lookup"><span data-stu-id="d5bb8-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="d5bb8-143">500</span><span class="sxs-lookup"><span data-stu-id="d5bb8-143">500</span></span>| <span data-ttu-id="d5bb8-144">Errore del server</span><span class="sxs-lookup"><span data-stu-id="d5bb8-144">Server Error</span></span>| <span data-ttu-id="d5bb8-145">Errore imprevisto nell'elaborazione della richiesta</span><span class="sxs-lookup"><span data-stu-id="d5bb8-145">Unexoected error processing request</span></span>| 









