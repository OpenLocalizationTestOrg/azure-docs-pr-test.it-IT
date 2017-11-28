---
title: aaaAzure fatturazione Enterprise API | Documenti Microsoft
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="defa3-103">Panoramica delle API di creazione di report per i clienti Enterprise</span><span class="sxs-lookup"><span data-stu-id="defa3-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="defa3-104">Hello Reporting API abilitare Azure Enterprise clienti tooprogrammatically pull consumo e dati di fatturazione in strumenti di analisi di dati preferito.</span><span class="sxs-lookup"><span data-stu-id="defa3-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="defa3-105">L'abilitazione delle API toohello di accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="defa3-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="defa3-106">**Generare o recuperare la chiave API hello** - Log in toohello Enterprise portal e seguire hello esercitazione nella Guida in linea - API di Reporting.</span><span class="sxs-lookup"><span data-stu-id="defa3-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="defa3-107">Hello prima sezione in questo articolo illustra come toogenerate o recuperare chiave hello API hello specificato registrazione.</span><span class="sxs-lookup"><span data-stu-id="defa3-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="defa3-108">**Passando le chiavi API hello** -chiave hello API deve toobe passato per ogni chiamata per l'autenticazione e autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="defa3-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="defa3-109">le proprietà seguenti Hello deve intestazioni HTTP toohello toobe</span><span class="sxs-lookup"><span data-stu-id="defa3-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="defa3-110">Chiave intestazione necessaria</span><span class="sxs-lookup"><span data-stu-id="defa3-110">Request Header Key</span></span> | <span data-ttu-id="defa3-111">Valore</span><span class="sxs-lookup"><span data-stu-id="defa3-111">Value</span></span>|
|-|-|
|<span data-ttu-id="defa3-112">Authorization</span><span class="sxs-lookup"><span data-stu-id="defa3-112">Authorization</span></span>| <span data-ttu-id="defa3-113">Specificare il valore di hello nel formato: **bearer {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="defa3-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="defa3-114">Esempio: bearer eyr....09</span><span class="sxs-lookup"><span data-stu-id="defa3-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="defa3-115">API per l'uso</span><span class="sxs-lookup"><span data-stu-id="defa3-115">Consumption APIs</span></span>
<span data-ttu-id="defa3-116">È disponibile un endpoint Swagger [qui](https://consumption.azure.com/swagger/ui/index) per hello API descritte sotto delle quali deve abilitare introspezione semplice di hello API e SDK per applicazioni client toogenerate possibilità di hello utilizzando [AutoRest](https://github.com/Azure/AutoRest) o [ Swagger CodeGen](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="defa3-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="defa3-117">I dati a partire dal 1° maggio 2014 sono disponibili tramite questa API.</span><span class="sxs-lookup"><span data-stu-id="defa3-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="defa3-118">**Saldo e riepilogo** : hello [bilanciamento e API riepilogo](billing-enterprise-api-balance-summary.md) offre un riepilogo di informazioni sulle saldi, nuovi acquisti, spese di servizio di Azure Marketplace, regolazioni e spese eccedenza mensile.</span><span class="sxs-lookup"><span data-stu-id="defa3-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="defa3-119">**Dettagli utilizzo** : hello [API dettagli utilizzo](billing-enterprise-api-usage-detail.md) offre una suddivisione giornaliera delle quantità consumate e spese stimate da una registrazione.</span><span class="sxs-lookup"><span data-stu-id="defa3-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="defa3-120">risultato Hello include anche informazioni sulle istanze, misuratori e reparti.</span><span class="sxs-lookup"><span data-stu-id="defa3-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="defa3-121">Hello API può essere determinata in base al periodo di fatturazione o da un inizio specificato e la data di fine.</span><span class="sxs-lookup"><span data-stu-id="defa3-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="defa3-122">**Archivio Marketplace addebito** : hello [Marketplace archivio addebito API](billing-enterprise-api-marketplace-storecharge.md) restituisce suddivisione spese marketplace basata sull'utilizzo di hello al giorno per hello specificato il periodo di fatturazione o date di inizio e fine (non sono inclusi i costi di una volta) .</span><span class="sxs-lookup"><span data-stu-id="defa3-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="defa3-123">**Prezzi** : hello [prezzo foglio API](billing-enterprise-api-pricesheet.md) fornisce tasso hello per ogni misuratore di hello dato periodo di fatturazione e di registrazione.</span><span class="sxs-lookup"><span data-stu-id="defa3-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="defa3-124">API di supporto</span><span class="sxs-lookup"><span data-stu-id="defa3-124">Helper APIs</span></span>
 <span data-ttu-id="defa3-125">**Elenco di periodi di fatturazione** : hello [API periodi di fatturazione](billing-enterprise-api-billing-periods.md) restituisce un elenco di fatturazione periodi che dispongono di dati di utilizzo per hello specificato registrazione in ordine cronologico inverso.</span><span class="sxs-lookup"><span data-stu-id="defa3-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="defa3-126">Ogni periodo contiene una proprietà che punta route API toohello per quattro set di dati - BalanceSummary, UsageDetails, Marketplace costi e prezzi di hello.</span><span class="sxs-lookup"><span data-stu-id="defa3-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="defa3-127">Codici di risposta dell'API</span><span class="sxs-lookup"><span data-stu-id="defa3-127">API Response Codes</span></span>  
|<span data-ttu-id="defa3-128">Codice di stato della risposta</span><span class="sxs-lookup"><span data-stu-id="defa3-128">Response Status Code</span></span>|<span data-ttu-id="defa3-129">Message</span><span class="sxs-lookup"><span data-stu-id="defa3-129">Message</span></span>|<span data-ttu-id="defa3-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="defa3-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="defa3-131">200</span><span class="sxs-lookup"><span data-stu-id="defa3-131">200</span></span>| <span data-ttu-id="defa3-132">OK</span><span class="sxs-lookup"><span data-stu-id="defa3-132">OK</span></span>|<span data-ttu-id="defa3-133">Nessun errore</span><span class="sxs-lookup"><span data-stu-id="defa3-133">No error</span></span>|
|<span data-ttu-id="defa3-134">401</span><span class="sxs-lookup"><span data-stu-id="defa3-134">401</span></span>| <span data-ttu-id="defa3-135">Non autorizzata</span><span class="sxs-lookup"><span data-stu-id="defa3-135">Unauthorized</span></span>| <span data-ttu-id="defa3-136">Chiave API non trovata, non valida, scaduta e così via</span><span class="sxs-lookup"><span data-stu-id="defa3-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="defa3-137">404</span><span class="sxs-lookup"><span data-stu-id="defa3-137">404</span></span>| <span data-ttu-id="defa3-138">Non disponibile</span><span class="sxs-lookup"><span data-stu-id="defa3-138">Unavailable</span></span>| <span data-ttu-id="defa3-139">Endpoint del report non trovato</span><span class="sxs-lookup"><span data-stu-id="defa3-139">Report endpoint not found</span></span>|
|<span data-ttu-id="defa3-140">400</span><span class="sxs-lookup"><span data-stu-id="defa3-140">400</span></span>| <span data-ttu-id="defa3-141">Bad Request</span><span class="sxs-lookup"><span data-stu-id="defa3-141">Bad Request</span></span>| <span data-ttu-id="defa3-142">Parametri non validi (intervalli di date, numeri EA e così via)</span><span class="sxs-lookup"><span data-stu-id="defa3-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="defa3-143">500</span><span class="sxs-lookup"><span data-stu-id="defa3-143">500</span></span>| <span data-ttu-id="defa3-144">Errore del server</span><span class="sxs-lookup"><span data-stu-id="defa3-144">Server Error</span></span>| <span data-ttu-id="defa3-145">Errore imprevisto nell'elaborazione della richiesta</span><span class="sxs-lookup"><span data-stu-id="defa3-145">Unexoected error processing request</span></span>| 









