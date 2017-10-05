---
title: Documentazione relativa all'API Recommendations di Machine Learning | Microsoft Docs
description: Documentazione relativa all'API Recommendations di Azure Machine Learning per un motore di raccomandazione disponibile in Microsoft Azure Marketplace.
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 1fba64d78d779344e2895b0d54419186b7584865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="06e62-103">Documentazione relativa all'API Recommendations di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="06e62-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="06e62-104">È consigliabile iniziare usando l'API Recommendations di Servizi cognitivi invece di questa versione.</span><span class="sxs-lookup"><span data-stu-id="06e62-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="06e62-105">Il Servizio cognitivo di Recommendations sostituirà questo servizio e verranno sviluppate nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="06e62-106">Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.</span><span class="sxs-lookup"><span data-stu-id="06e62-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="06e62-107">Per altre informazioni, vedere [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="06e62-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="06e62-108">Questo documento illustra le API Recommendations di Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="06e62-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="06e62-109">1. Panoramica generale</span><span class="sxs-lookup"><span data-stu-id="06e62-109">1. General overview</span></span>
<span data-ttu-id="06e62-110">Questo è un documento di riferimento dell'API.</span><span class="sxs-lookup"><span data-stu-id="06e62-110">This document is an API reference.</span></span> <span data-ttu-id="06e62-111">È consigliabile iniziare con il documento "Guida introduttiva per l'API Recommendations di Machine Learning".</span><span class="sxs-lookup"><span data-stu-id="06e62-111">You should start with the “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="06e62-112">L'API Recommendations di Azure Machine Learning può essere suddivisa nei seguenti gruppi logici:</span><span class="sxs-lookup"><span data-stu-id="06e62-112">The Azure Machine Learning Recommendations API can be divided into the following logical groups:</span></span>

* <span data-ttu-id="06e62-113"><ins>Limitazioni</ins>: limitazioni dell'API Recommendations.</span><span class="sxs-lookup"><span data-stu-id="06e62-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="06e62-114"><ins>Informazioni generali</ins>: informazioni su autenticazione, URI del servizio e controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="06e62-115"><ins>Modello Basic</ins>: API che consentono di eseguire operazioni di base sul modello, ad esempio creazione, aggiornamento ed eliminazione di un modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-115"><ins>Model Basic</ins> - APIs that enable you to do the basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="06e62-116"><ins>Modello Advanced</ins>: API che consentono di eseguire analisi avanzate sui dati del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-116"><ins>Model Advanced</ins> - APIs that enable you to get advanced data insights on the model.</span></span>
* <span data-ttu-id="06e62-117"><ins>Modello Business Rules</ins>: API che consentono di gestire regole business sui risultati delle raccomandazioni relative al modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-117"><ins>Model Business Rules</ins> - APIs that enable you to manage business rules on the model recommendation results.</span></span>
* <span data-ttu-id="06e62-118"><ins>Catalog</ins>: API che consentono di eseguire operazioni di base sul catalogo di un modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-118"><ins>Catalog</ins> - APIs that enable you to do basic operations on a model catalog.</span></span> <span data-ttu-id="06e62-119">Un catalogo contiene informazioni sui metadati relativi agli elementi dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-119">A catalog contains metadata information on the items of the usage data.</span></span>
* <span data-ttu-id="06e62-120"><ins>Feature</ins>: API che consentono di ottenere approfondimenti sull'elemento nel catalogo e su come usare queste informazioni per creare raccomandazioni migliori.</span><span class="sxs-lookup"><span data-stu-id="06e62-120"><ins>Feature</ins> - APIs that enable to get insights on item into the catalog and how to use this information to build better recommendations.</span></span>
* <span data-ttu-id="06e62-121"><ins>Usage Data</ins>: API che consentono di eseguire operazioni di base sui dati di utilizzo del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-121"><ins>Usage Data</ins> - APIs that enable you to do basic operations on the model usage data.</span></span> <span data-ttu-id="06e62-122">Nel form di base i dati di utilizzo sono costituiti da righe che includono coppie di &#60;userId&#62;,&#60;itemId&#62;.</span><span class="sxs-lookup"><span data-stu-id="06e62-122">Usage data in the basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="06e62-123"><ins>Build</ins>: API che consentono di attivare la compilazione di un modello e di eseguire operazioni di base associate alla compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-123"><ins>Build</ins> - APIs that enable you to trigger a model build and do basic operations that are related to this build.</span></span> <span data-ttu-id="06e62-124">È possibile attivare la compilazione di un modello solo se sono disponibili dati di utilizzo rilevanti.</span><span class="sxs-lookup"><span data-stu-id="06e62-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="06e62-125"><ins>Recommendation</ins>: API che consentono di usare raccomandazioni al termine della compilazione di un modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-125"><ins>Recommendation</ins> - APIs that enable you to consume recommendations once the build of a model ends.</span></span>
* <span data-ttu-id="06e62-126"><ins>User Data</ins>: API che consentono di recuperare informazioni su dati di utilizzo utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-126"><ins>User Data</ins> - APIs that enable you to fetch information on the user usage data.</span></span>
* <span data-ttu-id="06e62-127"><ins>Notifications</ins>: API che consentono di ricevere notifiche per i problemi correlati alle operazioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="06e62-127"><ins>Notifications</ins> - APIs that enable you to receive notifications on problems related to your API operations.</span></span> <span data-ttu-id="06e62-128">Ad esempio, se i dati di utilizzo vengono segnalati mediante acquisizione dei dati e la maggior parte degli eventi di elaborazione non riesce,</span><span class="sxs-lookup"><span data-stu-id="06e62-128">(For example, you are reporting usage data via Data Acquisition and most of the events processing are failing.</span></span> <span data-ttu-id="06e62-129">viene generata una notifica di errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="06e62-130">2. Limitazioni</span><span class="sxs-lookup"><span data-stu-id="06e62-130">2. Limitations</span></span>
* <span data-ttu-id="06e62-131">Il numero massimo di modelli per ogni sottoscrizione è 10.</span><span class="sxs-lookup"><span data-stu-id="06e62-131">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="06e62-132">Il numero massimo di compilazioni per ogni modello è 20.</span><span class="sxs-lookup"><span data-stu-id="06e62-132">The maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="06e62-133">Il numero massimo di elementi che possono essere inclusi nel catalogo è 100.000.</span><span class="sxs-lookup"><span data-stu-id="06e62-133">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="06e62-134">Il numero massimo di punti di utilizzo mantenuti è ~5.000.000.</span><span class="sxs-lookup"><span data-stu-id="06e62-134">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="06e62-135">I meno recenti saranno eliminati se ne vengono caricati o segnalati di nuovi.</span><span class="sxs-lookup"><span data-stu-id="06e62-135">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="06e62-136">Le dimensioni massime dei dati che possono essere inviati in POST (ad esempio, importazione dei dati del catalogo o dei dati di utilizzo) è di 200 MB.</span><span class="sxs-lookup"><span data-stu-id="06e62-136">The maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="06e62-137">Il numero massimo di elementi che è possibile richiedere durante il recupero di raccomandazioni è 150.</span><span class="sxs-lookup"><span data-stu-id="06e62-137">The maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="06e62-138">3. API: informazioni generali</span><span class="sxs-lookup"><span data-stu-id="06e62-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="06e62-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-139">3.1.</span></span> <span data-ttu-id="06e62-140">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="06e62-140">Authentication</span></span>
<span data-ttu-id="06e62-141">Seguire le linee guida di Microsoft Azure Marketplace relative all'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-141">Please follow the Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="06e62-142">Marketplace supporta il metodo di autenticazione di base o OAuth.</span><span class="sxs-lookup"><span data-stu-id="06e62-142">The marketplace supports either the Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="06e62-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-143">3.2.</span></span> <span data-ttu-id="06e62-144">URI del servizio</span><span class="sxs-lookup"><span data-stu-id="06e62-144">Service URI</span></span>
<span data-ttu-id="06e62-145">L'URI radice del servizio per ogni API Recommendations di Azure Machine Learning è disponibile [qui](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="06e62-145">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="06e62-146">L'URI del servizio completo è espresso usando elementi della specifica OData.</span><span class="sxs-lookup"><span data-stu-id="06e62-146">The full service URI is expressed using elements of the OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="06e62-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-147">3.3.</span></span> <span data-ttu-id="06e62-148">Versione dell'API</span><span class="sxs-lookup"><span data-stu-id="06e62-148">API version</span></span>
<span data-ttu-id="06e62-149">Ogni chiamata API terminerà con un parametro di query denominato apiVersion che dovrà essere impostato su 1.0.</span><span class="sxs-lookup"><span data-stu-id="06e62-149">Each API call will have, at the end, a query parameter called apiVersion that should be set to 1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="06e62-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="06e62-150">3.4.</span></span> <span data-ttu-id="06e62-151">Gli ID fanno distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="06e62-151">IDs are case sensitive</span></span>
<span data-ttu-id="06e62-152">Gli ID restituiti da una delle API fanno distinzione tra maiuscole e minuscole e devono essere usati esattamente come sono, quando vengono passati come parametri nelle chiamate API successive.</span><span class="sxs-lookup"><span data-stu-id="06e62-152">IDs, returned by any of the APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="06e62-153">Ad esempio, per gli ID dei modelli e del catalogo viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="06e62-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="06e62-154">4. Qualità delle raccomandazioni ed elementi ignoti</span><span class="sxs-lookup"><span data-stu-id="06e62-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="06e62-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-155">4.1.</span></span> <span data-ttu-id="06e62-156">Qualità delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="06e62-156">Recommendation quality</span></span>
<span data-ttu-id="06e62-157">La creazione di un modello di raccomandazione è in genere sufficiente per consentire al sistema di fornire raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-157">Creating a recommendation model is usually enough to allow the system to provide recommendations.</span></span> <span data-ttu-id="06e62-158">La qualità delle raccomandazioni varia tuttavia in base ai dati di utilizzo elaborati e alla copertura del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-158">Nevertheless, recommendation quality varies based on the usage processed and the coverage of the catalog.</span></span> <span data-ttu-id="06e62-159">Ad esempio, se sono disponibili molti elementi ignoti, ovvero elementi senza utilizzo significativo, il sistema avrà difficoltà a fornire una raccomandazione per tale elemento o a usarlo come elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="06e62-159">For example if you have a lot of cold items (items without significant usage), the system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="06e62-160">Per risolvere il problema degli elementi ignori, il sistema consente l'uso di metadati degli elementi per migliorare la qualità delle raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-160">In order to overcome the cold item problem, the system allows the use of metadata of the items to enhance the recommendations.</span></span> <span data-ttu-id="06e62-161">Questi metadati sono definiti funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-161">This metadata is referred to as features.</span></span> <span data-ttu-id="06e62-162">L'autore di un libro o l'attore di un film è un esempio tipico di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="06e62-163">Le funzionalità vengono fornire tramite il catalogo sotto forma di stringhe chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="06e62-163">Features are provided via the catalog in the form of key/value strings.</span></span> <span data-ttu-id="06e62-164">Per il formato completo del file di catalogo, vedere la sezione [Importare i dati del catalogo](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="06e62-164">For the full format of the catalog file, please refer to the [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="06e62-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-165">4.2.</span></span> <span data-ttu-id="06e62-166">Compilazione della classifica</span><span class="sxs-lookup"><span data-stu-id="06e62-166">Rank build</span></span>
<span data-ttu-id="06e62-167">Le funzionalità possono migliorare il modello di raccomandazione, ma ciò richiede l'uso di funzionalità significative.</span><span class="sxs-lookup"><span data-stu-id="06e62-167">Features can enhance the recommendation model, but to do so requires the use of meaningful features.</span></span> <span data-ttu-id="06e62-168">A questo scopo è stata introdotta una nuova compilazione per la definizione della classifica,</span><span class="sxs-lookup"><span data-stu-id="06e62-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="06e62-169">che consente di classificare l'utilità delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-169">This build will rank the usefulness of features.</span></span> <span data-ttu-id="06e62-170">Una funzionalità significativa presenta un punteggio di classificazione minimo pari a 2.</span><span class="sxs-lookup"><span data-stu-id="06e62-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="06e62-171">Dopo avere individuato le funzionalità significative, attivare una compilazione di raccomandazione con l'elenco, o sottoelenco, delle funzionalità significative.</span><span class="sxs-lookup"><span data-stu-id="06e62-171">After understanding which of the features are meaningful, trigger a recommendation build with the list (or sublist) of meaningful features.</span></span> <span data-ttu-id="06e62-172">È possibile usare queste funzionalità per il miglioramento sia degli elementi noti che di quelli ignoti.</span><span class="sxs-lookup"><span data-stu-id="06e62-172">It is possible to use these feature for the enhancement of both warm items and cold items.</span></span> <span data-ttu-id="06e62-173">Per usarle per gli elementi noti è necessario configurare il parametro di compilazione `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="06e62-173">In order to use them for warm items, the `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="06e62-174">Per usarle per gli elementi ignoti è necessario abilitare il parametro di compilazione `AllowColdItemPlacement`.</span><span class="sxs-lookup"><span data-stu-id="06e62-174">In order to use features for cold items, the `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="06e62-175">Nota: non è possibile abilitare `AllowColdItemPlacement` se non si abilita anche `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="06e62-175">Note: It is not possible to enable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="06e62-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-176">4.3.</span></span> <span data-ttu-id="06e62-177">Motivazione delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="06e62-177">Recommendation reasoning</span></span>
<span data-ttu-id="06e62-178">La motivazione delle raccomandazioni è un altro aspetto dell'utilizzo delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="06e62-179">In effetti, il motore di Azure Machine Learning Recommendations può usare funzionalità per offrire spiegazioni delle raccomandazioni (noto anche come</span><span class="sxs-lookup"><span data-stu-id="06e62-179">Indeed, the Azure Machine Learning Recommendations engine can use features to provide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="06e62-180">motivazione), aumentando il livello di confidenza nell'elemento raccomandato da parte dell'utente della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-180">reasoning), leading to more confidence in the recommended item from the recommendation consumer.</span></span>
<span data-ttu-id="06e62-181">Per abilitare le motivazioni, è necessario configurare i parametri `AllowFeatureCorrelation` e `ReasoningFeatureList` prima di richiedere una compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-181">To enable reasoning, the `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior to requesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="06e62-182">5. Modello Basic</span><span class="sxs-lookup"><span data-stu-id="06e62-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="06e62-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-183">5.1.</span></span> <span data-ttu-id="06e62-184">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="06e62-184">Create Model</span></span>
<span data-ttu-id="06e62-185">Crea una richiesta di tipo "crea modello".</span><span class="sxs-lookup"><span data-stu-id="06e62-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="06e62-186">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-186">HTTP Method</span></span> | <span data-ttu-id="06e62-187">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-188">POST</span><span class="sxs-lookup"><span data-stu-id="06e62-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-189">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-190">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-190">Parameter Name</span></span> | <span data-ttu-id="06e62-191">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-192">modelName</span><span class="sxs-lookup"><span data-stu-id="06e62-192">modelName</span></span> |<span data-ttu-id="06e62-193">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="06e62-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="06e62-194">Lunghezza massima: 20</span><span class="sxs-lookup"><span data-stu-id="06e62-194">Max length: 20</span></span> |
| <span data-ttu-id="06e62-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-195">apiVersion</span></span> |<span data-ttu-id="06e62-196">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-196">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-197">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-197">Request Body</span></span> |<span data-ttu-id="06e62-198">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-198">NONE</span></span> |

<span data-ttu-id="06e62-199">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-199">**Response**:</span></span>

<span data-ttu-id="06e62-200">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="06e62-201">`feed/entry/content/properties/id` : contiene l'ID modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-201">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="06e62-202">**Nota**: l'ID modello fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="06e62-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="06e62-203">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="52-get-model"></a><span data-ttu-id="06e62-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-204">5.2.</span></span> <span data-ttu-id="06e62-205">Ottenere il modello</span><span class="sxs-lookup"><span data-stu-id="06e62-205">Get Model</span></span>
<span data-ttu-id="06e62-206">Crea una richiesta di tipo "ottieni modello":</span><span class="sxs-lookup"><span data-stu-id="06e62-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="06e62-207">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-207">HTTP Method</span></span> | <span data-ttu-id="06e62-208">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-209">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="06e62-210">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-211">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-211">Parameter Name</span></span> | <span data-ttu-id="06e62-212">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-213">id</span><span class="sxs-lookup"><span data-stu-id="06e62-213">id</span></span> |<span data-ttu-id="06e62-214">Identificatore univoco del modello (con distinzione tra maiuscole e minuscole).|</span><span class="sxs-lookup"><span data-stu-id="06e62-214">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="06e62-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-215">apiVersion</span></span> |<span data-ttu-id="06e62-216">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-216">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-217">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-217">Request Body</span></span> |<span data-ttu-id="06e62-218">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-218">NONE</span></span> |

<span data-ttu-id="06e62-219">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-219">**Response**:</span></span>

<span data-ttu-id="06e62-220">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-220">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-221">I dati del modello sono disponibili negli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-221">The model data can be found under the following elements:</span></span>

* <span data-ttu-id="06e62-222">`feed/entry/content/properties/Id` : ID univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="06e62-223">`feed/entry/content/properties/Name` : nome del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="06e62-224">`feed/entry/content/properties/Date` : data di creazione del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="06e62-225">`feed/entry/content/properties/Status` : stato del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="06e62-226">Uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-226">One of the following:</span></span>
  * <span data-ttu-id="06e62-227">Created: il modello viene creato e non contiene dati del catalogo e di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="06e62-228">ReadyForBuild: il modello viene creato e contiene dati del catalogo e di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="06e62-229">`feed/entry/content/properties/HasActiveBuild` : indica se il modello è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06e62-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="06e62-230">`feed/entry/content/properties/BuildId`: ID compilazione attiva del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="06e62-231">`feed/entry/content/properties/Mpr`: classificazione percentile media (MPR, Mean Percentile Ranking) del modello. Vedere ModelInsight per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="06e62-232">`feed/entry/content/properties/UserName`: nome utente interno del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="06e62-233">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="06e62-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-234">5.3.</span></span>    <span data-ttu-id="06e62-235">Ottenere tutti i modelli</span><span class="sxs-lookup"><span data-stu-id="06e62-235">Get All Models</span></span>
<span data-ttu-id="06e62-236">Recupera tutti i modelli dell'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="06e62-236">Retrieves all models of the current user.</span></span>

| <span data-ttu-id="06e62-237">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-237">HTTP Method</span></span> | <span data-ttu-id="06e62-238">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-239">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="06e62-240">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-241">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-241">Parameter Name</span></span> | <span data-ttu-id="06e62-242">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-243">apiVersion</span></span> |<span data-ttu-id="06e62-244">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-244">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-245">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-245">Request Body</span></span> |<span data-ttu-id="06e62-246">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-246">NONE</span></span> |

<span data-ttu-id="06e62-247">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-247">**Response**:</span></span>

<span data-ttu-id="06e62-248">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="06e62-249">`feed/entry/content/properties/Id` : ID univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="06e62-250">`feed/entry/content/properties/Name` : nome del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="06e62-251">`feed/entry/content/properties/Date` : data di creazione del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="06e62-252">`feed/entry/content/properties/Status` : stato del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="06e62-253">Uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-253">One of the following:</span></span>
  * <span data-ttu-id="06e62-254">Created: il modello viene creato e non contiene dati del catalogo e di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="06e62-255">ReadyForBuild: il modello viene creato e contiene dati del catalogo e di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="06e62-256">`feed/entry/content/properties/HasActiveBuild` : indica se il modello è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="06e62-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="06e62-257">`feed/entry/content/properties/BuildId`: ID compilazione attiva del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="06e62-258">`feed/entry/content/properties/Mpr`:MPR del modello. Vedere ModelInsight per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="06e62-259">`feed/entry/content/properties/UserName`: nome utente interno del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="06e62-260">`feed/entry/content/properties/UsageFileNames` : elenco dei file di dati di utilizzo del modello, separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="06e62-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="06e62-261">`feed/entry/content/properties/CatalogId` : ID catalogo del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="06e62-262">`feed/entry/content/properties/Description` : descrizione del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="06e62-263">`feed/entry/content/properties/CatalogFileName` : nome del file di catalogo del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="06e62-264">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="06e62-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="06e62-265">5.4.</span></span>    <span data-ttu-id="06e62-266">Aggiornare il modello</span><span class="sxs-lookup"><span data-stu-id="06e62-266">Update Model</span></span>
<span data-ttu-id="06e62-267">È possibile aggiornare la descrizione del modello o l'ID compilazione attivo.</span><span class="sxs-lookup"><span data-stu-id="06e62-267">You can update the model description or the active build ID.</span></span><br><span data-ttu-id="06e62-268">
<ins>ID compilazione attiva</ins>: la compilazione per ogni modello ha un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="06e62-269">Con il termine ID compilazione attiva si identifica la prima compilazione riuscita di ogni nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-269">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="06e62-270">Se dopo avere ottenuto un ID compilazione attiva si eseguono altre compilazioni per lo stesso modello, è necessario impostarlo in modo esplicito come ID compilazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="06e62-270">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="06e62-271">Quando si usano raccomandazioni, se non si specifica l'ID compilazione da usare, verrà usato automaticamente quello predefinito.</span><span class="sxs-lookup"><span data-stu-id="06e62-271">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span><br>
<span data-ttu-id="06e62-272">Dopo avere implementato un modello di raccomandazione nell'ambiente di produzione, questo meccanismo consente di compilare nuovi modelli e testarli prima di alzarli di livello e passarli in produzione.</span><span class="sxs-lookup"><span data-stu-id="06e62-272">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="06e62-273">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-273">HTTP Method</span></span> | <span data-ttu-id="06e62-274">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-275">PUT</span><span class="sxs-lookup"><span data-stu-id="06e62-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="06e62-276">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-277">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-277">Parameter Name</span></span> | <span data-ttu-id="06e62-278">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-279">id</span><span class="sxs-lookup"><span data-stu-id="06e62-279">id</span></span> |<span data-ttu-id="06e62-280">Identificatore univoco del modello (con distinzione tra maiuscole e minuscole).|</span><span class="sxs-lookup"><span data-stu-id="06e62-280">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="06e62-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-281">apiVersion</span></span> |<span data-ttu-id="06e62-282">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-282">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-283">Request Body</span><span class="sxs-lookup"><span data-stu-id="06e62-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="06e62-284">Si noti che i tag XML Description e ActiveBuildId sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="06e62-284">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="06e62-285">Se non si vuole impostare Description o ActiveBuildId, rimuovere l'intero tag.</span><span class="sxs-lookup"><span data-stu-id="06e62-285">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="06e62-286">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-286">**Response**:</span></span>

<span data-ttu-id="06e62-287">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="06e62-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="06e62-288">5.5.</span></span>    <span data-ttu-id="06e62-289">Eliminare il modello</span><span class="sxs-lookup"><span data-stu-id="06e62-289">Delete Model</span></span>
<span data-ttu-id="06e62-290">Elimina un modello esistente in base all'ID.</span><span class="sxs-lookup"><span data-stu-id="06e62-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="06e62-291">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-291">HTTP Method</span></span> | <span data-ttu-id="06e62-292">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-293">DELETE</span><span class="sxs-lookup"><span data-stu-id="06e62-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="06e62-294">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-295">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-295">Parameter Name</span></span> | <span data-ttu-id="06e62-296">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-297">id</span><span class="sxs-lookup"><span data-stu-id="06e62-297">id</span></span> |<span data-ttu-id="06e62-298">Identificatore univoco del modello (con distinzione tra maiuscole e minuscole).|</span><span class="sxs-lookup"><span data-stu-id="06e62-298">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="06e62-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-299">apiVersion</span></span> |<span data-ttu-id="06e62-300">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-300">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-301">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-301">Request Body</span></span> |<span data-ttu-id="06e62-302">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-302">NONE</span></span> |

<span data-ttu-id="06e62-303">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-303">**Response**:</span></span>

<span data-ttu-id="06e62-304">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-304">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-305">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="06e62-306">6. Modello Advanced</span><span class="sxs-lookup"><span data-stu-id="06e62-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="06e62-307">6.1</span><span class="sxs-lookup"><span data-stu-id="06e62-307">6.1.</span></span>    <span data-ttu-id="06e62-308">Modello Data Insight</span><span class="sxs-lookup"><span data-stu-id="06e62-308">Model Data Insight</span></span>
<span data-ttu-id="06e62-309">Restituisce informazioni statistiche sui dati di utilizzo con cui è stato compilato questo modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-309">Returns statistical data on the usage data that this model was built with.</span></span>

<span data-ttu-id="06e62-310">Disponibile solo per la compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="06e62-311">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-311">HTTP Method</span></span> | <span data-ttu-id="06e62-312">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-313">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="06e62-314">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-315">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-315">Parameter Name</span></span> | <span data-ttu-id="06e62-316">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-317">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-317">modelId</span></span> |<span data-ttu-id="06e62-318">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-318">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-319">apiVersion</span></span> |<span data-ttu-id="06e62-320">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-320">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-321">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-321">Request Body</span></span> |<span data-ttu-id="06e62-322">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-322">NONE</span></span> |

<span data-ttu-id="06e62-323">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-323">**Response**:</span></span>

<span data-ttu-id="06e62-324">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-324">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-325">I dati vengono restituiti come una raccolta di proprietà.</span><span class="sxs-lookup"><span data-stu-id="06e62-325">The data is returned as a collection of properties.</span></span>

* <span data-ttu-id="06e62-326">`feed/entry/id/content/properties/key` : contiene il nome della proprietà.</span><span class="sxs-lookup"><span data-stu-id="06e62-326">`feed/entry/id/content/properties/key` - Holds the property name.</span></span>
* <span data-ttu-id="06e62-327">`feed/entry/id/content/properties/value` : contiene il valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="06e62-327">`feed/entry/id/content/properties/value` - Holds the property value.</span></span>

<span data-ttu-id="06e62-328">La tabella seguente illustra il valore rappresentato da ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="06e62-328">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="06e62-329">Chiave</span><span class="sxs-lookup"><span data-stu-id="06e62-329">Key</span></span> | <span data-ttu-id="06e62-330">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="06e62-331">AvgItemLength</span></span> |<span data-ttu-id="06e62-332">Numero medio di utenti distinti per elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="06e62-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="06e62-333">AvgUserLength</span></span> |<span data-ttu-id="06e62-334">Numero medio di elementi distinti per utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="06e62-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="06e62-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="06e62-336">Numero di elementi dopo l'eliminazione degli elementi che non possono essere modellati.</span><span class="sxs-lookup"><span data-stu-id="06e62-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="06e62-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="06e62-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="06e62-338">Numero di punti di utilizzo dopo l'eliminazione degli utenti e degli elementi che non possono essere modellati.</span><span class="sxs-lookup"><span data-stu-id="06e62-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="06e62-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="06e62-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="06e62-340">Numero di punti di utilizzo dopo l'eliminazione degli utenti e degli elementi che non possono essere modellati.</span><span class="sxs-lookup"><span data-stu-id="06e62-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="06e62-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="06e62-341">MaxItemLength</span></span> |<span data-ttu-id="06e62-342">Numero di utenti distinti per l'elemento più comune.</span><span class="sxs-lookup"><span data-stu-id="06e62-342">Number of distinct users for the most popular item.</span></span> |
| <span data-ttu-id="06e62-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="06e62-343">MaxUserLength</span></span> |<span data-ttu-id="06e62-344">Numero massimo di elementi distinti per un utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="06e62-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="06e62-345">MinItemLength</span></span> |<span data-ttu-id="06e62-346">Numero massimo di utenti distinti per un elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="06e62-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="06e62-347">MinUserLength</span></span> |<span data-ttu-id="06e62-348">Numero minimo di elementi distinti per un utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="06e62-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="06e62-349">RawNumberOfItems</span></span> |<span data-ttu-id="06e62-350">Numero di elementi nei file di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-350">Number of items in the usage files.</span></span> |
| <span data-ttu-id="06e62-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="06e62-351">RawNumberOfUsers</span></span> |<span data-ttu-id="06e62-352">Numero di punti di utilizzo prima di qualsiasi eliminazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="06e62-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="06e62-353">RawNumberOfRecords</span></span> |<span data-ttu-id="06e62-354">Numero di punti di utilizzo prima di qualsiasi eliminazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="06e62-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="06e62-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="06e62-356">N/D</span><span class="sxs-lookup"><span data-stu-id="06e62-356">N/A</span></span> |
| <span data-ttu-id="06e62-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="06e62-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="06e62-358">N/D</span><span class="sxs-lookup"><span data-stu-id="06e62-358">N/A</span></span> |
| <span data-ttu-id="06e62-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="06e62-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="06e62-360">N/D</span><span class="sxs-lookup"><span data-stu-id="06e62-360">N/A</span></span> |

<span data-ttu-id="06e62-361">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="06e62-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-362">6.2.</span></span>    <span data-ttu-id="06e62-363">Modello Insight</span><span class="sxs-lookup"><span data-stu-id="06e62-363">Model Insight</span></span>
<span data-ttu-id="06e62-364">Restituisce informazioni dettagliate sul modello nella compilazione attiva o, se indicata, in una compilazione specifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-364">Returns model insight on the active build or (if given) on a specific build.</span></span>

<span data-ttu-id="06e62-365">Disponibile solo per la compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="06e62-366">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-366">HTTP Method</span></span> | <span data-ttu-id="06e62-367">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-368">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-368">GET</span></span> |<span data-ttu-id="06e62-369">Con l'ID compilazione attiva:</span><span class="sxs-lookup"><span data-stu-id="06e62-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-370">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-371">Con ID compilazione specifica:</span><span class="sxs-lookup"><span data-stu-id="06e62-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-372">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-372">Parameter Name</span></span> | <span data-ttu-id="06e62-373">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-374">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-374">modelId</span></span> |<span data-ttu-id="06e62-375">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-375">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-376">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-376">buildId</span></span> |<span data-ttu-id="06e62-377">Facoltativo: numero che identifica una compilazione completata.</span><span class="sxs-lookup"><span data-stu-id="06e62-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="06e62-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-378">apiVersion</span></span> |<span data-ttu-id="06e62-379">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-379">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-380">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-380">Request Body</span></span> |<span data-ttu-id="06e62-381">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-381">NONE</span></span> |

<span data-ttu-id="06e62-382">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-382">**Response**:</span></span>

<span data-ttu-id="06e62-383">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-383">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-384">I dati vengono restituiti come una raccolta di proprietà.</span><span class="sxs-lookup"><span data-stu-id="06e62-384">The data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="06e62-385">La tabella seguente illustra il valore rappresentato da ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="06e62-385">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="06e62-386">Chiave</span><span class="sxs-lookup"><span data-stu-id="06e62-386">Key</span></span> | <span data-ttu-id="06e62-387">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="06e62-388">CatalogCoverage</span></span> |<span data-ttu-id="06e62-389">La parte del catalogo che è possibile modellare con modelli di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-389">What part of the catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="06e62-390">Il resto degli elementi richiederà funzionalità basate sul contenuto.</span><span class="sxs-lookup"><span data-stu-id="06e62-390">The rest of the items will need content-based features.</span></span> |
| <span data-ttu-id="06e62-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="06e62-391">Mpr</span></span> |<span data-ttu-id="06e62-392">Classificazione percentile media del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-392">Mean percentile ranking of the model.</span></span> <span data-ttu-id="06e62-393">È preferibile un valore basso.</span><span class="sxs-lookup"><span data-stu-id="06e62-393">Lower is better.</span></span> |
| <span data-ttu-id="06e62-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="06e62-394">NumberOfDimensions</span></span> |<span data-ttu-id="06e62-395">Numero di dimensioni usate dall'algoritmo di fattorizzazione di matrice.</span><span class="sxs-lookup"><span data-stu-id="06e62-395">Number of dimensions used by the matrix factorization algorithm.</span></span> |

<span data-ttu-id="06e62-396">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="06e62-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-397">6.3.</span></span>    <span data-ttu-id="06e62-398">Ottenere un esempio del modello</span><span class="sxs-lookup"><span data-stu-id="06e62-398">Get Model Sample</span></span>
<span data-ttu-id="06e62-399">Ottiene un esempio del modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-399">Gets a sample of the recommendation model.</span></span>

| <span data-ttu-id="06e62-400">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-400">HTTP Method</span></span> | <span data-ttu-id="06e62-401">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-402">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="06e62-403">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-404">Con ID compilazione specifica:</span><span class="sxs-lookup"><span data-stu-id="06e62-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="06e62-405">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-406">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-406">Parameter Name</span></span> | <span data-ttu-id="06e62-407">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-408">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-408">modelId</span></span> |<span data-ttu-id="06e62-409">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-409">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-410">apiVersion</span></span> |<span data-ttu-id="06e62-411">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-411">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-412">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-412">Request Body</span></span> |<span data-ttu-id="06e62-413">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-413">NONE</span></span> |

<span data-ttu-id="06e62-414">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-414">**Response**:</span></span>

<span data-ttu-id="06e62-415">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-415">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-416">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-416">OData XML</span></span>

<span data-ttu-id="06e62-417">La risposta viene restituita in un formato di testo non elaborato:</span><span class="sxs-lookup"><span data-stu-id="06e62-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If the Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of the Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on the Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in the Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, The Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On the Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, The Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories to Tell in the Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, The Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic the Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in the Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, The Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, The X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell the President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In the Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, The Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of the Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, The Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in the Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (The Official Guide to the X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, The Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, The Truth Is Out There (The Official Guide to the X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, The Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of the Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where the Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, The God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (The Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in the Time of Cholera (Penguin Great Books of the 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, The Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories To Tell In The Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from the Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="06e62-418">7. Modello Business Rules</span><span class="sxs-lookup"><span data-stu-id="06e62-418">7. Model Business Rules</span></span>
<span data-ttu-id="06e62-419">Questi sono i tipi di regole supportati:</span><span class="sxs-lookup"><span data-stu-id="06e62-419">These are the types of rules supported:</span></span>

* <span data-ttu-id="06e62-420"><strong>BlockList</strong>: BlockList consente di fornire un elenco degli elementi che non devono essere restituiti nei risultati delle raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-420"><strong>BlockList</strong> - BlockList enables you to provide a list of items that you do not want to return in the recommendation results.</span></span> 
* <span data-ttu-id="06e62-421"><strong>FeatureBlockList</strong>: FeatureBlockList consente di bloccare gli elementi in base ai valori delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you to block items based on the values of its features.</span></span>

<span data-ttu-id="06e62-422">*Non inviare più di 1000 elementi in una singola regola blocklist o si rischia il timeout della chiamata. Se si desidera bloccare più di 1000 elementi, è possibile effettuare diverse chiamate in blocklist.*</span><span class="sxs-lookup"><span data-stu-id="06e62-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need to block more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="06e62-423"><strong>Upsale</strong>: consente di imporre gli elementi da restituire nel risultati delle raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-423"><strong>Upsale</strong> - Upsale enables you to enforce items to return in the recommendation results.</span></span>
* <span data-ttu-id="06e62-424"><strong>WhiteList</strong>: consente di fornire raccomandazioni solo da un elenco di elementi.</span><span class="sxs-lookup"><span data-stu-id="06e62-424"><strong>WhiteList</strong> - White List enables you to only suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="06e62-425"><strong>FeatureWhiteList</strong>: consente di raccomandare solo gli elementi che hanno valori di funzionalità specifici.</span><span class="sxs-lookup"><span data-stu-id="06e62-425"><strong>FeatureWhiteList</strong> - Feature White List enables you to only recommend items that have specific feature values.</span></span>
* <span data-ttu-id="06e62-426"><strong>PerSeedBlockList</strong>: consente di specificare un elenco, per tipo di elemento, degli elementi che non possono essere restituiti come risultati delle raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you to provide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="06e62-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-427">7.1.</span></span>    <span data-ttu-id="06e62-428">Ottenere le regole del modello</span><span class="sxs-lookup"><span data-stu-id="06e62-428">Get Model Rules</span></span>
| <span data-ttu-id="06e62-429">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-429">HTTP Method</span></span> | <span data-ttu-id="06e62-430">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-431">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="06e62-432">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-433">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-433">Parameter Name</span></span> | <span data-ttu-id="06e62-434">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-435">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-435">modelId</span></span> |<span data-ttu-id="06e62-436">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-436">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-437">apiVersion</span></span> |<span data-ttu-id="06e62-438">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-438">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-439">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-439">Request Body</span></span> |<span data-ttu-id="06e62-440">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-440">NONE</span></span> |

<span data-ttu-id="06e62-441">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-441">**Response**:</span></span>

<span data-ttu-id="06e62-442">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="06e62-443">`feed/entry/content/properties/Id` : identificatore univoco della regola.</span><span class="sxs-lookup"><span data-stu-id="06e62-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="06e62-444">`feed/entry/content/properties/Type` : tipo di regola.</span><span class="sxs-lookup"><span data-stu-id="06e62-444">`feed/entry/content/properties/Type` - Type of the rule.</span></span>
* <span data-ttu-id="06e62-445">`feed/entry/content/properties/Parameter` : parametro della regola.</span><span class="sxs-lookup"><span data-stu-id="06e62-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="06e62-446">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="06e62-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-447">7.2.</span></span>    <span data-ttu-id="06e62-448">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="06e62-448">Add Rule</span></span>
| <span data-ttu-id="06e62-449">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-449">HTTP Method</span></span> | <span data-ttu-id="06e62-450">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-451">POST</span><span class="sxs-lookup"><span data-stu-id="06e62-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="06e62-452">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="06e62-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="06e62-453">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-453">Parameter Name</span></span> | <span data-ttu-id="06e62-454">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-455">apiVersion</span></span> |<span data-ttu-id="06e62-456">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-456">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-457">Request Body</span><span class="sxs-lookup"><span data-stu-id="06e62-457">Request Body</span></span> | |

<span data-ttu-id="06e62-458"><ins>Ogni volta che si specificano gli ID elemento per le regole di business, assicurarsi di usare l'ID esterno dell'elemento (lo stesso ID usato nel file di catalogo)</ins></span><span class="sxs-lookup"><span data-stu-id="06e62-458"><ins>Whenever providing Item Ids for business rules, make sure to use the External Id of the item (the same Id that you used in the catalog file)</ins></span></span><br><span data-ttu-id="06e62-459">
<ins>Per aggiungere una regola BlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="06e62-459">
<ins>To add a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="06e62-460"><ins>
<ins>Per aggiungere una regola FeatureBlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="06e62-460"><ins>
<ins>To add a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="06e62-461"><ins> Per aggiungere una regola Upsale:</ins></span><span class="sxs-lookup"><span data-stu-id="06e62-461"><ins> To add an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="06e62-462">
<ins>Per aggiungere una regola WhiteList:</ins></span><span class="sxs-lookup"><span data-stu-id="06e62-462">
<ins>To add a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="06e62-463"><ins>
<ins>Per aggiungere una regola FeatureWhiteList:</ins></span><span class="sxs-lookup"><span data-stu-id="06e62-463"><ins>
<ins>To add a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="06e62-464"><ins> Per aggiungere una regola PerSeedBlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="06e62-464"><ins> To add a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="06e62-465">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-465">**Response**:</span></span>

<span data-ttu-id="06e62-466">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-466">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-467">L'API restituisce la regola appena creata con i relativi dettagli.</span><span class="sxs-lookup"><span data-stu-id="06e62-467">The API returns the newly created rule with its details.</span></span> <span data-ttu-id="06e62-468">Le proprietà della regola possono essere recuperate dai percorsi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-468">The rules property can be retrieved from the following paths:</span></span>

* <span data-ttu-id="06e62-469">`feed/entry/content/properties/Id` : identificatore univoco della regola.</span><span class="sxs-lookup"><span data-stu-id="06e62-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="06e62-470">`feed/entry/content/properties/Type` : tipo di regola, ovvero BlockList o Upsale.</span><span class="sxs-lookup"><span data-stu-id="06e62-470">`feed/entry/content/properties/Type` - Type of the rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="06e62-471">`feed/entry/content/properties/Parameter` : parametro della regola.</span><span class="sxs-lookup"><span data-stu-id="06e62-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="06e62-472">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="06e62-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-473">7.3.</span></span>    <span data-ttu-id="06e62-474">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="06e62-474">Delete Rule</span></span>
| <span data-ttu-id="06e62-475">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-475">HTTP Method</span></span> | <span data-ttu-id="06e62-476">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-477">DELETE</span><span class="sxs-lookup"><span data-stu-id="06e62-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-478">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-479">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-479">Parameter Name</span></span> | <span data-ttu-id="06e62-480">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-481">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-481">modelId</span></span> |<span data-ttu-id="06e62-482">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-482">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-483">filterId</span><span class="sxs-lookup"><span data-stu-id="06e62-483">filterId</span></span> |<span data-ttu-id="06e62-484">Identificatore univoco del filtro.</span><span class="sxs-lookup"><span data-stu-id="06e62-484">Unique identifier of the filter</span></span> |
| <span data-ttu-id="06e62-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-485">apiVersion</span></span> |<span data-ttu-id="06e62-486">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-486">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-487">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-487">Request Body</span></span> |<span data-ttu-id="06e62-488">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-488">NONE</span></span> |

<span data-ttu-id="06e62-489">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-489">**Response**:</span></span>

<span data-ttu-id="06e62-490">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="06e62-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="06e62-491">7.4.</span></span>    <span data-ttu-id="06e62-492">Eliminare tutte le regole</span><span class="sxs-lookup"><span data-stu-id="06e62-492">Delete All Rules</span></span>
| <span data-ttu-id="06e62-493">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-493">HTTP Method</span></span> | <span data-ttu-id="06e62-494">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-495">DELETE</span><span class="sxs-lookup"><span data-stu-id="06e62-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-496">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-497">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-497">Parameter Name</span></span> | <span data-ttu-id="06e62-498">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-499">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-499">modelId</span></span> |<span data-ttu-id="06e62-500">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-500">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-501">apiVersion</span></span> |<span data-ttu-id="06e62-502">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-502">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-503">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-503">Request Body</span></span> |<span data-ttu-id="06e62-504">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-504">NONE</span></span> |

<span data-ttu-id="06e62-505">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-505">**Response**:</span></span>

<span data-ttu-id="06e62-506">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="06e62-507">8. Catalogo</span><span class="sxs-lookup"><span data-stu-id="06e62-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="06e62-508">8.1</span><span class="sxs-lookup"><span data-stu-id="06e62-508">8.1.</span></span>    <span data-ttu-id="06e62-509">Importare i dati del catalogo</span><span class="sxs-lookup"><span data-stu-id="06e62-509">Import Catalog Data</span></span>
<span data-ttu-id="06e62-510">Se si caricano diversi file del catalogo nello stesso modello con diverse chiamate, verranno inseriti solo i nuovi elementi del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-510">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="06e62-511">Gli elementi esistenti manterranno i valori originali.</span><span class="sxs-lookup"><span data-stu-id="06e62-511">Existing items will remain with the original values.</span></span> <span data-ttu-id="06e62-512">Non è possibile aggiornare i dati del catalogo con questo metodo.</span><span class="sxs-lookup"><span data-stu-id="06e62-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="06e62-513">I dati del catalogo devono seguire il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="06e62-513">The catalog data should follow the following format:</span></span>

* <span data-ttu-id="06e62-514">Senza funzionalità: `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="06e62-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="06e62-515">Con funzionalità: `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="06e62-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="06e62-516">Nota: le dimensioni massime del file sono pari a 200 MB.</span><span class="sxs-lookup"><span data-stu-id="06e62-516">Note: The maximum file size is 200MB.</span></span>

<span data-ttu-id="06e62-517">** Dettagli relativi al formato **</span><span class="sxs-lookup"><span data-stu-id="06e62-517">** Format details **</span></span>

| <span data-ttu-id="06e62-518">Nome</span><span class="sxs-lookup"><span data-stu-id="06e62-518">Name</span></span> | <span data-ttu-id="06e62-519">Mandatory</span><span class="sxs-lookup"><span data-stu-id="06e62-519">Mandatory</span></span> | <span data-ttu-id="06e62-520">Tipo</span><span class="sxs-lookup"><span data-stu-id="06e62-520">Type</span></span> | <span data-ttu-id="06e62-521">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="06e62-522">Item Id</span><span class="sxs-lookup"><span data-stu-id="06e62-522">Item Id</span></span> |<span data-ttu-id="06e62-523">Sì</span><span class="sxs-lookup"><span data-stu-id="06e62-523">Yes</span></span> |<span data-ttu-id="06e62-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="06e62-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="06e62-525">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="06e62-525">Max length: 50</span></span> |<span data-ttu-id="06e62-526">Identificatore univoco di un elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="06e62-527">Item Name</span><span class="sxs-lookup"><span data-stu-id="06e62-527">Item Name</span></span> |<span data-ttu-id="06e62-528">Sì</span><span class="sxs-lookup"><span data-stu-id="06e62-528">Yes</span></span> |<span data-ttu-id="06e62-529">Qualsiasi carattere alfanumerico</span><span class="sxs-lookup"><span data-stu-id="06e62-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="06e62-530">Lunghezza massima: 255</span><span class="sxs-lookup"><span data-stu-id="06e62-530">Max length: 255</span></span> |<span data-ttu-id="06e62-531">Nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-531">Item name.</span></span> |
| <span data-ttu-id="06e62-532">Item Category</span><span class="sxs-lookup"><span data-stu-id="06e62-532">Item Category</span></span> |<span data-ttu-id="06e62-533">Sì</span><span class="sxs-lookup"><span data-stu-id="06e62-533">Yes</span></span> |<span data-ttu-id="06e62-534">Qualsiasi carattere alfanumerico</span><span class="sxs-lookup"><span data-stu-id="06e62-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="06e62-535">Lunghezza massima: 255</span><span class="sxs-lookup"><span data-stu-id="06e62-535">Max length: 255</span></span> |<span data-ttu-id="06e62-536">Categoria alla quale appartiene l'elemento (ad esempio, libri di cucina, letteratura e così via); può essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="06e62-536">Category to which this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="06e62-537">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-537">Description</span></span> |<span data-ttu-id="06e62-538">No, a meno che siano presenti funzionalità (può essere vuoto)</span><span class="sxs-lookup"><span data-stu-id="06e62-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="06e62-539">Qualsiasi carattere alfanumerico</span><span class="sxs-lookup"><span data-stu-id="06e62-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="06e62-540">Lunghezza massima: 4000</span><span class="sxs-lookup"><span data-stu-id="06e62-540">Max length: 4000</span></span> |<span data-ttu-id="06e62-541">Descrizione dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-541">Description of this item.</span></span> |
| <span data-ttu-id="06e62-542">Elenco di funzionalità</span><span class="sxs-lookup"><span data-stu-id="06e62-542">Features list</span></span> |<span data-ttu-id="06e62-543">No</span><span class="sxs-lookup"><span data-stu-id="06e62-543">No</span></span> |<span data-ttu-id="06e62-544">Qualsiasi carattere alfanumerico</span><span class="sxs-lookup"><span data-stu-id="06e62-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="06e62-545">Lunghezza massima: 4000, numero massimo di funzionalità: 20</span><span class="sxs-lookup"><span data-stu-id="06e62-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="06e62-546">Elenco delimitato da virgole di nome funzionalità=valore funzionalità che può essere usato per migliorare la raccomandazione sul modello. Vedere la sezione [Advanced topics](#2-advanced-topics) (Argomenti avanzati).</span><span class="sxs-lookup"><span data-stu-id="06e62-546">Comma-separated list of feature name=feature value that can be used to enhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="06e62-547">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-547">HTTP Method</span></span> | <span data-ttu-id="06e62-548">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-549">POST</span><span class="sxs-lookup"><span data-stu-id="06e62-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-550">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="06e62-551">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="06e62-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="06e62-552">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-552">Parameter Name</span></span> | <span data-ttu-id="06e62-553">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-554">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-554">modelId</span></span> |<span data-ttu-id="06e62-555">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-555">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-556">filename</span><span class="sxs-lookup"><span data-stu-id="06e62-556">filename</span></span> |<span data-ttu-id="06e62-557">Identificatore testuale del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-557">Textual identifier of the catalog.</span></span><br><span data-ttu-id="06e62-558">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="06e62-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="06e62-559">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="06e62-559">Max length: 50</span></span> |
| <span data-ttu-id="06e62-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-560">apiVersion</span></span> |<span data-ttu-id="06e62-561">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-561">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-562">Request Body</span><span class="sxs-lookup"><span data-stu-id="06e62-562">Request Body</span></span> |<span data-ttu-id="06e62-563">Esempio (con funzionalità):</span><span class="sxs-lookup"><span data-stu-id="06e62-563">Example (with features):</span></span><br/><span data-ttu-id="06e62-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span><span class="sxs-lookup"><span data-stu-id="06e62-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="06e62-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span><span class="sxs-lookup"><span data-stu-id="06e62-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="06e62-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="06e62-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="06e62-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span><span class="sxs-lookup"><span data-stu-id="06e62-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="06e62-568">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-568">**Response**:</span></span>

<span data-ttu-id="06e62-569">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-569">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-570">L'API restituisce un report dell'importazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-570">The API returns a report of the import.</span></span>

* <span data-ttu-id="06e62-571">`feed\entry\content\properties\LineCount` : numero di righe accettate.</span><span class="sxs-lookup"><span data-stu-id="06e62-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="06e62-572">`feed\entry\content\properties\ErrorCount` : numero di righe non inserite a causa di un errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="06e62-573">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="06e62-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-574">8.2.</span></span>    <span data-ttu-id="06e62-575">Ottenere il catalogo</span><span class="sxs-lookup"><span data-stu-id="06e62-575">Get Catalog</span></span>
<span data-ttu-id="06e62-576">Recupera tutti gli elementi del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="06e62-577">Il catalogo verrà recuperato una pagina alla volta.</span><span class="sxs-lookup"><span data-stu-id="06e62-577">The catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="06e62-578">Se si desidera ottenere gli elementi con un indice specifico, è possibile usare il parametro odata $skip.</span><span class="sxs-lookup"><span data-stu-id="06e62-578">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="06e62-579">Ad esempio se si desidera ottenere gli elementi a partire dalla posizione 100, aggiungere il parametro $skip=100 alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="06e62-579">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="06e62-580">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-580">HTTP Method</span></span> | <span data-ttu-id="06e62-581">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-582">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-583">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-584">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-584">Parameter Name</span></span> | <span data-ttu-id="06e62-585">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-586">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-586">modelId</span></span> |<span data-ttu-id="06e62-587">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-587">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-588">apiVersion</span></span> |<span data-ttu-id="06e62-589">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-589">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-590">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-590">Request Body</span></span> |<span data-ttu-id="06e62-591">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-591">NONE</span></span> |

<span data-ttu-id="06e62-592">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-592">**Response**:</span></span>

<span data-ttu-id="06e62-593">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-593">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-594">La risposta include una voce per ogni elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-594">The response includes one entry per catalog item.</span></span> <span data-ttu-id="06e62-595">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-595">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-596">`feed/entry/content/properties/ExternalId` : ID esterno dell'elemento del catalogo, specificato dal cliente.</span><span class="sxs-lookup"><span data-stu-id="06e62-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, the one provided by the customer.</span></span>
* <span data-ttu-id="06e62-597">`feed/entry/content/properties/InternalId` : ID interno dell'elemento del catalogo, generato dall'API Recommendations di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="06e62-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="06e62-598">`feed/entry/content/properties/Name` : nome dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="06e62-599">`feed/entry/content/properties/Category` : categoria dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="06e62-600">`feed/entry/content/properties/Description` : descrizione dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="06e62-601">`feed/entry/content/properties/Metadata` : metadati dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="06e62-602">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">The Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="06e62-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-603">8.3.</span></span>    <span data-ttu-id="06e62-604">Ottenere gli elementi del catalogo in base al token</span><span class="sxs-lookup"><span data-stu-id="06e62-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="06e62-605">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-605">HTTP Method</span></span> | <span data-ttu-id="06e62-606">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-607">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-608">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-609">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-609">Parameter Name</span></span> | <span data-ttu-id="06e62-610">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-611">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-611">modelId</span></span> |<span data-ttu-id="06e62-612">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-612">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-613">token</span><span class="sxs-lookup"><span data-stu-id="06e62-613">token</span></span> |<span data-ttu-id="06e62-614">Token del nome dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-614">Token of the catalog item’s name.</span></span> <span data-ttu-id="06e62-615">Deve contenere almeno tre caratteri.</span><span class="sxs-lookup"><span data-stu-id="06e62-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="06e62-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-616">apiVersion</span></span> |<span data-ttu-id="06e62-617">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-617">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-618">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-618">Request Body</span></span> |<span data-ttu-id="06e62-619">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-619">NONE</span></span> |

<span data-ttu-id="06e62-620">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-620">**Response**:</span></span>

<span data-ttu-id="06e62-621">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-621">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-622">La risposta include una voce per ogni elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-622">The response includes one entry per catalog item.</span></span> <span data-ttu-id="06e62-623">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-623">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-624">`feed/entry/content/properties/InternalId` : ID interno dell'elemento del catalogo, generato dall'API Recommendations di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="06e62-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="06e62-625">`feed/entry/content/properties/Name` : nome dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="06e62-626">`feed/entry/content/properties/Rating` : per uso futuro</span><span class="sxs-lookup"><span data-stu-id="06e62-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="06e62-627">`feed/entry/content/properties/Reasoning` : per uso futuro</span><span class="sxs-lookup"><span data-stu-id="06e62-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="06e62-628">`feed/entry/content/properties/Metadata` : per uso futuro</span><span class="sxs-lookup"><span data-stu-id="06e62-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="06e62-629">`feed/entry/content/properties/FormattedRating` : per uso futuro</span><span class="sxs-lookup"><span data-stu-id="06e62-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="06e62-630">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="06e62-631">9. Dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="06e62-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="06e62-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-632">9.1.</span></span>    <span data-ttu-id="06e62-633">Importare i dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="06e62-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="06e62-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-634">9.1.1.</span></span> <span data-ttu-id="06e62-635">Caricamento del file</span><span class="sxs-lookup"><span data-stu-id="06e62-635">Uploading File</span></span>
<span data-ttu-id="06e62-636">Queste sezioni mostrano come caricare i dati di utilizzo tramite un file.</span><span class="sxs-lookup"><span data-stu-id="06e62-636">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="06e62-637">È possibile chiamare l'API più volte con i dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="06e62-638">Tutti i dati di utilizzo verranno salvati per tutte le chiamate.</span><span class="sxs-lookup"><span data-stu-id="06e62-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="06e62-639">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-639">HTTP Method</span></span> | <span data-ttu-id="06e62-640">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-641">POST</span><span class="sxs-lookup"><span data-stu-id="06e62-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-642">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-643">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-643">Parameter Name</span></span> | <span data-ttu-id="06e62-644">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-645">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-645">modelId</span></span> |<span data-ttu-id="06e62-646">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-646">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-647">filename</span><span class="sxs-lookup"><span data-stu-id="06e62-647">filename</span></span> |<span data-ttu-id="06e62-648">Identificatore testuale del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-648">Textual identifier of the catalog.</span></span><br><span data-ttu-id="06e62-649">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="06e62-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="06e62-650">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="06e62-650">Max length: 50</span></span> |
| <span data-ttu-id="06e62-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-651">apiVersion</span></span> |<span data-ttu-id="06e62-652">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-652">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-653">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-653">Request Body</span></span> |<span data-ttu-id="06e62-654">Dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-654">Usage data.</span></span> <span data-ttu-id="06e62-655">Formato:</span><span class="sxs-lookup"><span data-stu-id="06e62-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="06e62-656">Nome</span><span class="sxs-lookup"><span data-stu-id="06e62-656">Name</span></span></th><th><span data-ttu-id="06e62-657">Mandatory</span><span class="sxs-lookup"><span data-stu-id="06e62-657">Mandatory</span></span></th><th><span data-ttu-id="06e62-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="06e62-658">Type</span></span></th><th><span data-ttu-id="06e62-659">Descrizione</span><span class="sxs-lookup"><span data-stu-id="06e62-659">Description</span></span></th></tr><tr><td><span data-ttu-id="06e62-660">User Id</span><span class="sxs-lookup"><span data-stu-id="06e62-660">User Id</span></span></td><td><span data-ttu-id="06e62-661">Sì</span><span class="sxs-lookup"><span data-stu-id="06e62-661">Yes</span></span></td><td><span data-ttu-id="06e62-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="06e62-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="06e62-663">Lunghezza massima: 255</span><span class="sxs-lookup"><span data-stu-id="06e62-663">Max length: 255</span></span> </td><td><span data-ttu-id="06e62-664">Identificatore univoco di un utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="06e62-665">Item Id</span><span class="sxs-lookup"><span data-stu-id="06e62-665">Item Id</span></span></td><td><span data-ttu-id="06e62-666">Sì</span><span class="sxs-lookup"><span data-stu-id="06e62-666">Yes</span></span></td><td><span data-ttu-id="06e62-667">[A-z], [a-z], [0-9], [&#95;] &#40;carattere di sottolineatura&#41;, [-] &#40;trattino&#41;</span><span class="sxs-lookup"><span data-stu-id="06e62-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="06e62-668">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="06e62-668">Max length: 50</span></span></td><td><span data-ttu-id="06e62-669">Identificatore univoco di un elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="06e62-670">Time</span><span class="sxs-lookup"><span data-stu-id="06e62-670">Time</span></span></td><td><span data-ttu-id="06e62-671">No</span><span class="sxs-lookup"><span data-stu-id="06e62-671">No</span></span></td><td><span data-ttu-id="06e62-672">Data in formato: AAAA/MM/GGTHH:MM:SS (ad esempio 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="06e62-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="06e62-673">Ora dei dati.</span><span class="sxs-lookup"><span data-stu-id="06e62-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="06e62-674">Evento</span><span class="sxs-lookup"><span data-stu-id="06e62-674">Event</span></span></td><td><span data-ttu-id="06e62-675">No. Se viene specificato, deve essere inserita anche la data</span><span class="sxs-lookup"><span data-stu-id="06e62-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="06e62-676">Uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-676">One of the following:</span></span><br><span data-ttu-id="06e62-677">• Click</span><span class="sxs-lookup"><span data-stu-id="06e62-677">• Click</span></span><br><span data-ttu-id="06e62-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="06e62-678">• RecommendationClick</span></span><br><span data-ttu-id="06e62-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="06e62-679">•    AddShopCart</span></span><br><span data-ttu-id="06e62-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="06e62-680">• RemoveShopCart</span></span><br><span data-ttu-id="06e62-681">• Acquisto</span><span class="sxs-lookup"><span data-stu-id="06e62-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="06e62-682">Dimensione massima file: 200 MB</span><span class="sxs-lookup"><span data-stu-id="06e62-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="06e62-683">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="06e62-684">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-684">**Response**:</span></span>

<span data-ttu-id="06e62-685">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="06e62-686">`Feed\entry\content\properties\LineCount` : numero di righe accettate.</span><span class="sxs-lookup"><span data-stu-id="06e62-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="06e62-687">`Feed\entry\content\properties\ErrorCount` : numero di righe non inserite a causa di un errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="06e62-688">`Feed\entry\content\properties\FileId` : identificatore del file.</span><span class="sxs-lookup"><span data-stu-id="06e62-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="06e62-689">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="06e62-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-690">9.1.2.</span></span> <span data-ttu-id="06e62-691">Uso dell'acquisizione dei dati</span><span class="sxs-lookup"><span data-stu-id="06e62-691">Using Data Acquisition</span></span>
<span data-ttu-id="06e62-692">Questa sezione illustra come inviare eventi in tempo reale a Recommendations di Azure Machine Learning, in genere dal sito Web.</span><span class="sxs-lookup"><span data-stu-id="06e62-692">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="06e62-693">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-693">HTTP Method</span></span> | <span data-ttu-id="06e62-694">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-695">POST</span><span class="sxs-lookup"><span data-stu-id="06e62-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="06e62-696">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="06e62-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="06e62-697">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-697">Parameter Name</span></span> | <span data-ttu-id="06e62-698">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-699">apiVersion</span></span> |<span data-ttu-id="06e62-700">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-700">1.0</span></span> |
| <span data-ttu-id="06e62-701">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-701">Request body</span></span> |<span data-ttu-id="06e62-702">Immissione di dati evento per ogni evento da inviare.</span><span class="sxs-lookup"><span data-stu-id="06e62-702">Event data entry for each event you want to send.</span></span> <span data-ttu-id="06e62-703">Per lo stesso utente o la stessa sessione del browser si dovrà inviare lo stesso ID nel campo SessionId.</span><span class="sxs-lookup"><span data-stu-id="06e62-703">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="06e62-704">Vedere l'esempio di corpo dell'evento di seguito.</span><span class="sxs-lookup"><span data-stu-id="06e62-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="06e62-705">Esempio di evento "Click":</span><span class="sxs-lookup"><span data-stu-id="06e62-705">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="06e62-706">Esempio di evento "RecommendationClick":</span><span class="sxs-lookup"><span data-stu-id="06e62-706">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="06e62-707">Esempio di evento "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="06e62-707">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="06e62-708">Esempio di evento "RemoveShopCart":</span><span class="sxs-lookup"><span data-stu-id="06e62-708">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
              <EventData>
                      <Name>RemoveShopCart</Name>
                      <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="06e62-709">Esempio di evento "Purchase":</span><span class="sxs-lookup"><span data-stu-id="06e62-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="06e62-710">Esempio di invio di due eventi, "Click" e "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="06e62-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="06e62-711">**Risposta**: Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="06e62-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-712">9.2.</span></span>    <span data-ttu-id="06e62-713">Elencare i file di dati di utilizzo del modello</span><span class="sxs-lookup"><span data-stu-id="06e62-713">List Model Usage Files</span></span>
<span data-ttu-id="06e62-714">Recupera i metadati di tutti i file di dati di utilizzo del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="06e62-715">Il file di dati di utilizzo verrà recuperato una pagina alla volta.</span><span class="sxs-lookup"><span data-stu-id="06e62-715">The usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="06e62-716">Ogni pagina contiene 100 elementi.</span><span class="sxs-lookup"><span data-stu-id="06e62-716">Each page containes 100 items.</span></span> <span data-ttu-id="06e62-717">Se si desidera ottenere gli elementi con un indice specifico, è possibile usare il parametro odata $skip.</span><span class="sxs-lookup"><span data-stu-id="06e62-717">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="06e62-718">Ad esempio se si desidera ottenere gli elementi a partire dalla posizione 100, aggiungere il parametro $skip=100 alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="06e62-718">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="06e62-719">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-719">HTTP Method</span></span> | <span data-ttu-id="06e62-720">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-721">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-722">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-723">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-723">Parameter Name</span></span> | <span data-ttu-id="06e62-724">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="06e62-725">forModelId</span></span> |<span data-ttu-id="06e62-726">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-726">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-727">apiVersion</span></span> |<span data-ttu-id="06e62-728">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-728">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-729">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-729">Request Body</span></span> |<span data-ttu-id="06e62-730">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-730">NONE</span></span> |

<span data-ttu-id="06e62-731">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-731">**Response**:</span></span>

<span data-ttu-id="06e62-732">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-732">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-733">La risposta include una voce per ogni file di dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-733">The response includes one entry per usage file.</span></span> <span data-ttu-id="06e62-734">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-734">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-735">`feed\entry\content\properties\Id` : ID del file di dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="06e62-736">`feed\entry\content\properties\Length` : lunghezza del file di dati di utilizzo, in MB.</span><span class="sxs-lookup"><span data-stu-id="06e62-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="06e62-737">`feed\entry\content\properties\DateModified` : data di creazione del file di dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-737">`feed\entry\content\properties\DateModified` - Date when the usage file was created.</span></span>
* <span data-ttu-id="06e62-738">`feed\entry\content\properties\UseInModel` : indica se il file di dati di utilizzo viene usato nel modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-738">`feed\entry\content\properties\UseInModel` - Whether the usage file is used in the model.</span></span>

<span data-ttu-id="06e62-739">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="06e62-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-740">9.3.</span></span>    <span data-ttu-id="06e62-741">Ottenere statistiche di utilizzo</span><span class="sxs-lookup"><span data-stu-id="06e62-741">Get Usage Statistics</span></span>
<span data-ttu-id="06e62-742">Ottiene le statistiche di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-742">Gets usage statistics.</span></span>

| <span data-ttu-id="06e62-743">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-743">HTTP Method</span></span> | <span data-ttu-id="06e62-744">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-745">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-746">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-747">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-747">Parameter Name</span></span> | <span data-ttu-id="06e62-748">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-749">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-749">modelId</span></span> |<span data-ttu-id="06e62-750">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-750">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-751">startDate</span><span class="sxs-lookup"><span data-stu-id="06e62-751">startDate</span></span> |<span data-ttu-id="06e62-752">Data di inizio.</span><span class="sxs-lookup"><span data-stu-id="06e62-752">Start date.</span></span> <span data-ttu-id="06e62-753">Formato: aaaa/MM/ggTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="06e62-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="06e62-754">endDate</span><span class="sxs-lookup"><span data-stu-id="06e62-754">endDate</span></span> |<span data-ttu-id="06e62-755">Data di fine.</span><span class="sxs-lookup"><span data-stu-id="06e62-755">End date.</span></span> <span data-ttu-id="06e62-756">Formato: aaaa/MM/ggTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="06e62-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="06e62-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="06e62-757">eventTypes</span></span> |<span data-ttu-id="06e62-758">Stringa con valori delimitati da virgole di tipi di evento specifici o Null per ottenere tutti gli eventi.</span><span class="sxs-lookup"><span data-stu-id="06e62-758">Comma-separated string of event types or null to get all events</span></span> |
| <span data-ttu-id="06e62-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-759">apiVersion</span></span> |<span data-ttu-id="06e62-760">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-760">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-761">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-761">Request Body</span></span> |<span data-ttu-id="06e62-762">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-762">NONE</span></span> |

<span data-ttu-id="06e62-763">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-763">**Response**:</span></span>

<span data-ttu-id="06e62-764">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-764">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-765">Raccolta di elementi chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="06e62-765">A collection of key/value elements.</span></span> <span data-ttu-id="06e62-766">Ognuno contiene la somma degli eventi per un tipo specifico di eventi raggruppati in base all'ora.</span><span class="sxs-lookup"><span data-stu-id="06e62-766">Each one contains the sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="06e62-767">`feed\entry[i]\content\properties\Key` : contiene la data e l'ora (raggruppate per ora) e il tipo di evento.</span><span class="sxs-lookup"><span data-stu-id="06e62-767">`feed\entry[i]\content\properties\Key` - Contains the time (grouped by hour) and the event type.</span></span>
* <span data-ttu-id="06e62-768">`feed\entry[i]\content\properties\Value` : numero totale di eventi.</span><span class="sxs-lookup"><span data-stu-id="06e62-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="06e62-769">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="06e62-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="06e62-770">9.4.</span></span>    <span data-ttu-id="06e62-771">Ottenere un esempio del file di dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="06e62-771">Get Usage File Sample</span></span>
<span data-ttu-id="06e62-772">Recupera i primi 2 KB del contenuto del file di dati di utilizzo:</span><span class="sxs-lookup"><span data-stu-id="06e62-772">Retrieves the first 2KB of usage file content.</span></span>

| <span data-ttu-id="06e62-773">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-773">HTTP Method</span></span> | <span data-ttu-id="06e62-774">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-775">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-776">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-777">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-777">Parameter Name</span></span> | <span data-ttu-id="06e62-778">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-779">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-779">modelId</span></span> |<span data-ttu-id="06e62-780">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-780">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-781">fileId</span><span class="sxs-lookup"><span data-stu-id="06e62-781">fileId</span></span> |<span data-ttu-id="06e62-782">Identificatore univoco del file di dati di utilizzo del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-782">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="06e62-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-783">apiVersion</span></span> |<span data-ttu-id="06e62-784">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-784">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-785">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-785">Request Body</span></span> |<span data-ttu-id="06e62-786">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-786">NONE</span></span> |

<span data-ttu-id="06e62-787">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-787">**Response**:</span></span>

<span data-ttu-id="06e62-788">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-788">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-789">La risposta viene restituita in un formato di testo non elaborato:</span><span class="sxs-lookup"><span data-stu-id="06e62-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="06e62-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="06e62-790">9.5.</span></span>    <span data-ttu-id="06e62-791">Ottenere il file di dati di utilizzo del modello</span><span class="sxs-lookup"><span data-stu-id="06e62-791">Get Model Usage File</span></span>
<span data-ttu-id="06e62-792">Recupera l'intero contenuto del file. di dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-792">Retrieves the full content of the usage file.</span></span>

| <span data-ttu-id="06e62-793">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-793">HTTP Method</span></span> | <span data-ttu-id="06e62-794">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-795">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-796">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-797">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-797">Parameter Name</span></span> | <span data-ttu-id="06e62-798">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-799">mid</span><span class="sxs-lookup"><span data-stu-id="06e62-799">mid</span></span> |<span data-ttu-id="06e62-800">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-800">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-801">fid</span><span class="sxs-lookup"><span data-stu-id="06e62-801">fid</span></span> |<span data-ttu-id="06e62-802">Identificatore univoco del file di dati di utilizzo del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-802">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="06e62-803">download</span><span class="sxs-lookup"><span data-stu-id="06e62-803">download</span></span> |<span data-ttu-id="06e62-804">1</span><span class="sxs-lookup"><span data-stu-id="06e62-804">1</span></span> |
| <span data-ttu-id="06e62-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-805">apiVersion</span></span> |<span data-ttu-id="06e62-806">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-806">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-807">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-807">Request Body</span></span> |<span data-ttu-id="06e62-808">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-808">NONE</span></span> |

<span data-ttu-id="06e62-809">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-809">**Response**:</span></span>

<span data-ttu-id="06e62-810">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-810">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-811">La risposta viene restituita in un formato di testo non elaborato:</span><span class="sxs-lookup"><span data-stu-id="06e62-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="06e62-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="06e62-812">9.6.</span></span>    <span data-ttu-id="06e62-813">Eliminare il file di dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="06e62-813">Delete Usage File</span></span>
<span data-ttu-id="06e62-814">Elimina il file di dati di utilizzo del modello specificato.</span><span class="sxs-lookup"><span data-stu-id="06e62-814">Deletes the specified model usage file.</span></span>

| <span data-ttu-id="06e62-815">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-815">HTTP Method</span></span> | <span data-ttu-id="06e62-816">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-817">DELETE</span><span class="sxs-lookup"><span data-stu-id="06e62-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-818">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-819">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-819">Parameter Name</span></span> | <span data-ttu-id="06e62-820">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-821">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-821">modelId</span></span> |<span data-ttu-id="06e62-822">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-822">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-823">fileId</span><span class="sxs-lookup"><span data-stu-id="06e62-823">fileId</span></span> |<span data-ttu-id="06e62-824">Identificatore univoco del file da eliminare.</span><span class="sxs-lookup"><span data-stu-id="06e62-824">Unique identifier of the file to be deleted</span></span> |
| <span data-ttu-id="06e62-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-825">apiVersion</span></span> |<span data-ttu-id="06e62-826">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-826">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-827">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-827">Request Body</span></span> |<span data-ttu-id="06e62-828">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-828">NONE</span></span> |

<span data-ttu-id="06e62-829">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-829">**Response**:</span></span>

<span data-ttu-id="06e62-830">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="06e62-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="06e62-831">9.7.</span></span>    <span data-ttu-id="06e62-832">Eliminare tutti i file di dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="06e62-832">Delete All Usage Files</span></span>
<span data-ttu-id="06e62-833">Elimina tutti i file di dati di utilizzo del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="06e62-834">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-834">HTTP Method</span></span> | <span data-ttu-id="06e62-835">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-836">DELETE</span><span class="sxs-lookup"><span data-stu-id="06e62-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-837">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-838">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-838">Parameter Name</span></span> | <span data-ttu-id="06e62-839">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-840">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-840">modelId</span></span> |<span data-ttu-id="06e62-841">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-841">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-842">apiVersion</span></span> |<span data-ttu-id="06e62-843">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-843">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-844">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-844">Request Body</span></span> |<span data-ttu-id="06e62-845">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-845">NONE</span></span> |

<span data-ttu-id="06e62-846">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-846">**Response**:</span></span>

<span data-ttu-id="06e62-847">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="06e62-848">10. Funzionalità</span><span class="sxs-lookup"><span data-stu-id="06e62-848">10. Features</span></span>
<span data-ttu-id="06e62-849">Questa sezione illustra come recuperare informazioni sulle funzionalità, ad esempio le funzionalità importate e i relativi valori, la classificazione e la relativa data di allocazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-849">This section shows how to retrieve feature information, such as the imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="06e62-850">Le funzionalità vengono importate come parte dei dati del catalogo e quindi la relativa classificazione viene associata durante una compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-850">Features are imported as part of the catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="06e62-851">La classificazione delle funzionalità può cambiare in base al modello di dati di utilizzo e al tipo di elementi.</span><span class="sxs-lookup"><span data-stu-id="06e62-851">Feature rank can change according to the pattern of usage data and type of items.</span></span> <span data-ttu-id="06e62-852">Per la coerenza dei dati di utilizzo e degli elementi, è opportuno che le fluttuazioni siano limitate.</span><span class="sxs-lookup"><span data-stu-id="06e62-852">But for consistent usage/items, the rank should have only small fluctuations.</span></span>
<span data-ttu-id="06e62-853">La classificazione delle funzionalità è espressa mediante un numero non negativo.</span><span class="sxs-lookup"><span data-stu-id="06e62-853">The rank of features is a non-negative number.</span></span> <span data-ttu-id="06e62-854">Il numero 0 indica che la funzionalità non è stata classificata, ad esempio nel caso in cui l'API venga richiamata prima che sia completata la prima compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-854">The  number 0 means that the feature was not ranked (happens if you invoke this API prior to the completion of the first rank build).</span></span> <span data-ttu-id="06e62-855">La data in cui è stata attribuita la classificazione è detta aggiornamento del punteggio.</span><span class="sxs-lookup"><span data-stu-id="06e62-855">The date at which the rank was attributed is called the score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="06e62-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-856">10.1.</span></span> <span data-ttu-id="06e62-857">Ottenere informazioni sulle funzionalità (per l'ultima compilazione della classifica)</span><span class="sxs-lookup"><span data-stu-id="06e62-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="06e62-858">Recupera le informazioni sulle funzionalità, inclusa la classificazione per l'ultima compilazione della classifica riuscita.</span><span class="sxs-lookup"><span data-stu-id="06e62-858">Retrieves the feature information, including ranking, for the last successful rank build.</span></span>

| <span data-ttu-id="06e62-859">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-859">HTTP Method</span></span> | <span data-ttu-id="06e62-860">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-861">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-862">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-863">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-863">Parameter Name</span></span> | <span data-ttu-id="06e62-864">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-865">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-865">modelId</span></span> |<span data-ttu-id="06e62-866">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-866">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="06e62-867">samplingSize</span></span> |<span data-ttu-id="06e62-868">Numero di valori da includere per ogni funzionalità, in base ai dati presenti nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-868">Number of values to include for each feature according to the data present in the catalog.</span></span> <br/><span data-ttu-id="06e62-869">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="06e62-869">Possible values are:</span></span><br> <span data-ttu-id="06e62-870">-1, tutti i campioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-870">-1 - All samples.</span></span> <br><span data-ttu-id="06e62-871">0, nessun campionamento.</span><span class="sxs-lookup"><span data-stu-id="06e62-871">0 - No sampling.</span></span> <br><span data-ttu-id="06e62-872">N, restituisce N campioni per ogni nome di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="06e62-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-873">apiVersion</span></span> |<span data-ttu-id="06e62-874">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-874">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-875">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-875">Request Body</span></span> |<span data-ttu-id="06e62-876">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-876">NONE</span></span> |

<span data-ttu-id="06e62-877">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-877">**Response**:</span></span>

<span data-ttu-id="06e62-878">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-878">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-879">La risposta contiene un elenco di voci di informazioni sulle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-879">The response contains a list of feature info entries.</span></span> <span data-ttu-id="06e62-880">Ogni voce contiene:</span><span class="sxs-lookup"><span data-stu-id="06e62-880">Each entry contains:</span></span>

* <span data-ttu-id="06e62-881">`feed/entry/content/m:properties/d:Name` : nome della funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="06e62-882">`feed/entry/content/m:properties/d:RankUpdateDate`: data in cui la classifica è stata allocata alla funzionalità, nota anche come</span><span class="sxs-lookup"><span data-stu-id="06e62-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="06e62-883">funzionalità di aggiornamento del punteggio.</span><span class="sxs-lookup"><span data-stu-id="06e62-883">score freshness feature.</span></span> <span data-ttu-id="06e62-884">Una data cronologica ("0001-01-01T00:00:00") indica che non è stata eseguita alcuna compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="06e62-885">`feed/entry/content/m:properties/d:Rank` classificazione delle funzionalità (mobile).</span><span class="sxs-lookup"><span data-stu-id="06e62-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="06e62-886">Una classificazione pari ad almeno 2.0 è considerata una funzionalità valida.</span><span class="sxs-lookup"><span data-stu-id="06e62-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="06e62-887">`feed/entry/content/m:properties/d:SampleValues` : elenco con valori delimitati da virgole fino alle dimensioni di campionamento richieste.</span><span class="sxs-lookup"><span data-stu-id="06e62-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="06e62-888">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get the features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="06e62-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-889">10.2.</span></span> <span data-ttu-id="06e62-890">Ottenere informazioni sulle funzionalità (per la specifica compilazione della classifica)</span><span class="sxs-lookup"><span data-stu-id="06e62-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="06e62-891">Recupera le informazioni sulle funzionalità, inclusa la classificazione per una compilazione della classifica specifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-891">Retrieves the feature information, including the ranking for a specific rank build.</span></span>

| <span data-ttu-id="06e62-892">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-892">HTTP Method</span></span> | <span data-ttu-id="06e62-893">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-894">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-895">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-896">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-896">Parameter Name</span></span> | <span data-ttu-id="06e62-897">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-898">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-898">modelId</span></span> |<span data-ttu-id="06e62-899">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-899">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="06e62-900">samplingSize</span></span> |<span data-ttu-id="06e62-901">Numero di valori da includere per ogni funzionalità, in base ai dati presenti nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-901">Number of values to include for each feature according to the data present in the catalog.</span></span><br/> <span data-ttu-id="06e62-902">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="06e62-902">Possible values are:</span></span><br> <span data-ttu-id="06e62-903">-1, tutti i campioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-903">-1 - All samples.</span></span> <br><span data-ttu-id="06e62-904">0, nessun campionamento.</span><span class="sxs-lookup"><span data-stu-id="06e62-904">0 - No sampling.</span></span> <br><span data-ttu-id="06e62-905">N, restituisce N campioni per ogni nome di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="06e62-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="06e62-906">rankBuildId</span></span> |<span data-ttu-id="06e62-907">Identificatore univoco per la compilazione della classifica o -1 per l'ultima compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-907">Unique identifier of the rank build or -1 for the last rank build</span></span> |
| <span data-ttu-id="06e62-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-908">apiVersion</span></span> |<span data-ttu-id="06e62-909">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-909">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-910">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-910">Request Body</span></span> |<span data-ttu-id="06e62-911">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-911">NONE</span></span> |

<span data-ttu-id="06e62-912">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-912">**Response**:</span></span>

<span data-ttu-id="06e62-913">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-913">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-914">La risposta contiene un elenco di voci di informazioni sulle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-914">The response contains a list of feature info entries.</span></span> <span data-ttu-id="06e62-915">Ogni voce contiene:</span><span class="sxs-lookup"><span data-stu-id="06e62-915">Each entry contains:</span></span>

* <span data-ttu-id="06e62-916">`feed/entry/content/m:properties/d:Name` : nome della funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="06e62-917">`feed/entry/content/m:properties/d:RankUpdateDate`: data in cui la classifica è stata allocata alla funzionalità, nota anche come</span><span class="sxs-lookup"><span data-stu-id="06e62-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="06e62-918">funzionalità di aggiornamento del punteggio.</span><span class="sxs-lookup"><span data-stu-id="06e62-918">score freshness feature.</span></span> <span data-ttu-id="06e62-919">Una data cronologica ("0001-01-01T00:00:00") indica che non è stata eseguita alcuna compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="06e62-920">`feed/entry/content/m:properties/d:Rank` classificazione delle funzionalità (mobile).</span><span class="sxs-lookup"><span data-stu-id="06e62-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="06e62-921">Una classificazione pari ad almeno 2.0 è considerata una funzionalità valida.</span><span class="sxs-lookup"><span data-stu-id="06e62-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="06e62-922">`feed/entry/content/m:properties/d:SampleValues` : elenco con valori delimitati da virgole fino alle dimensioni di campionamento richieste.</span><span class="sxs-lookup"><span data-stu-id="06e62-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="06e62-923">OData</span><span class="sxs-lookup"><span data-stu-id="06e62-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get the features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="06e62-924">11. Compilazione</span><span class="sxs-lookup"><span data-stu-id="06e62-924">11. Build</span></span>
  <span data-ttu-id="06e62-925">Questa sezione descrive le diverse API correlate alle compilazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-925">This section explains the different APIs related to builds.</span></span> <span data-ttu-id="06e62-926">Esistono tre tipi di compilazione: una compilazione raccomandazione, una compilazione classifica e una compilazione FBT (Frequently Bought Together).</span><span class="sxs-lookup"><span data-stu-id="06e62-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="06e62-927">Lo scopo della compilazione raccomandazione è di generare un modello di raccomandazione usato per le stime.</span><span class="sxs-lookup"><span data-stu-id="06e62-927">The recommendation build's purpose is to generate a recommendation model used for predictions.</span></span> <span data-ttu-id="06e62-928">Le stime (per questo tipo di compilazione) sono di due tipi:</span><span class="sxs-lookup"><span data-stu-id="06e62-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="06e62-929">I2I, nota anche come</span><span class="sxs-lookup"><span data-stu-id="06e62-929">I2I - a.k.a.</span></span> <span data-ttu-id="06e62-930">Raccomandazioni da elemento a elemento: dato un elemento o un elenco di elementi, questa opzione stimerà un elenco di elementi che possono risultare molto interessanti.</span><span class="sxs-lookup"><span data-stu-id="06e62-930">Item to Item recommendations - given an item or a list of items this option will predict a list of items that are likely to be of high interest.</span></span>
* <span data-ttu-id="06e62-931">U2I, nota anche come</span><span class="sxs-lookup"><span data-stu-id="06e62-931">U2I - a.k.a.</span></span> <span data-ttu-id="06e62-932">Raccomandazioni da utente a elemento: dato un ID utente (e facoltativamente un elenco di elementi), questa opzione stimerà un elenco di elementi che possono risultare molto interessanti per l'utente specificato (e la scelta di elementi aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="06e62-932">User to Item recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely to be of high interest for the given user (and its additional choice of items).</span></span> <span data-ttu-id="06e62-933">Le indicazioni U2I si basano sulla cronologia di elementi di interesse per l'utente fino al momento in cui è stato compilato il modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-933">The U2I recommendations are based on the history of items that were of interest for the user up to the time the model was built.</span></span>

<span data-ttu-id="06e62-934">Una compilazione della classifica è una compilazione tecnica che consente di ottenere informazioni sull'utilità delle proprie funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-934">A rank build is a technical build that allows you to learn about the usefulness of your features.</span></span> <span data-ttu-id="06e62-935">In genere, per ottenere risultati migliori per un modello di raccomandazione riguardante le funzionalità, è necessario seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="06e62-935">Usually, in order to get the best result for a recommendation model involving features, you should take the following steps:</span></span>

* <span data-ttu-id="06e62-936">Attivare una compilazione della classifica, a meno che il punteggio delle funzionalità non sia stabile, quindi attendere il punteggio delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-936">Trigger a rank build (unless the score of your features is stable) and wait till you get the feature score.</span></span>
* <span data-ttu-id="06e62-937">Recuperare la classificazione delle funzionalità chiamando l'API [Get Features Info](#101-get-features-info-for-last-rank-build) .</span><span class="sxs-lookup"><span data-stu-id="06e62-937">Retrieve the rank of your features by calling the [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="06e62-938">Configurare una compilazione di raccomandazioni con i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-938">Configure a recommendation build with the following parameters:</span></span>
  * <span data-ttu-id="06e62-939">`useFeatureInModel` : impostare su True.</span><span class="sxs-lookup"><span data-stu-id="06e62-939">`useFeatureInModel` - Set to True.</span></span>
  * <span data-ttu-id="06e62-940">`ModelingFeatureList` : impostare su un elenco di funzionalità separate da virgole con un punteggio pari a 2,0 o superiore in base alle classificazioni recuperate nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="06e62-940">`ModelingFeatureList` - Set to a comma-separated list of features with a score of 2.0 or more (according to the ranks you retrieved in the previous step).</span></span>
  * <span data-ttu-id="06e62-941">`AllowColdItemPlacement`: impostare su True.</span><span class="sxs-lookup"><span data-stu-id="06e62-941">`AllowColdItemPlacement` - Set to True.</span></span>
  * <span data-ttu-id="06e62-942">È possibile scegliere di impostare `EnableFeatureCorrelation` su True e `ReasoningFeatureList` sull'elenco di funzionalità che si vuole usare come spiegazioni. In genere si tratta dello stesso elenco di funzionalità usato nella creazione di modelli o di un sottoelenco.</span><span class="sxs-lookup"><span data-stu-id="06e62-942">Optionally you can set `EnableFeatureCorrelation` to True and `ReasoningFeatureList` to the list of features you want to use for explanations (usually the same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="06e62-943">Attivare la compilazione di raccomandazioni con i parametri configurati.</span><span class="sxs-lookup"><span data-stu-id="06e62-943">Trigger the recommendation build with the configured parameters.</span></span>

<span data-ttu-id="06e62-944">Nota: se non si configurano parametri, ovvero se si richiama la compilazione di raccomandazioni senza parametri, oppure non si disabilita in modo esplicito l'utilizzo di funzionalità (ad esempio, `UseFeatureInModel` impostato su False), il sistema imposterà i parametri correlati alla funzionalità sui valori illustrati sopra, se esiste una compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-944">Note: If you do not configure any parameters (e.g. invoke the recommendation build without parameters) or you do not explicitly disable the usage of features (e.g. `UseFeatureInModel` set to False), the system will set up the feature-related parameters to the explained values above in case a rank build exists.</span></span>

<span data-ttu-id="06e62-945">Non esistono limitazioni all'esecuzione contemporanea di una compilazione della classifica e di una compilazione di raccomandazioni per lo stesso modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-945">There is no restriction on running a rank build and a recommendation build concurrently for the same model.</span></span> <span data-ttu-id="06e62-946">Non è tuttavia possibile eseguire due compilazioni dello stesso tipo nello stesso modello in parallelo.</span><span class="sxs-lookup"><span data-stu-id="06e62-946">Nevertheless, you cannot run two builds of the same type on the same model in parallel.</span></span>

<span data-ttu-id="06e62-947">Una compilazione FBT (Frequently Bought Together) è un altro algoritmo di raccomandazione, detto a volte sistema di raccomandazione "conservativo", che risulta appropriato per i cataloghi non omogenei per natura (omogenei: libri, film, alcuni alimenti, moda; non omogenei: computer e dispositivi, interdominio, estremamente diversi).</span><span class="sxs-lookup"><span data-stu-id="06e62-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="06e62-948">Nota: se i file di dati di utilizzo caricati contengono il campo facoltativo "event type", per la creazione del modello FBT verranno usati solo eventi "Purchase".</span><span class="sxs-lookup"><span data-stu-id="06e62-948">Note: if the usage files that you uploaded contain the optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="06e62-949">Se non viene specificato alcun tipo di evento, tutti gli eventi verranno considerati come acquisti.</span><span class="sxs-lookup"><span data-stu-id="06e62-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="06e62-950">11.1 Parametri della compilazione</span><span class="sxs-lookup"><span data-stu-id="06e62-950">11.1 Build parameters</span></span>
<span data-ttu-id="06e62-951">Ogni tipo di compilazione può essere configurato con un set di parametri, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="06e62-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="06e62-952">Se non si configurano parametri, il sistema attribuirà automaticamente i valori ai parametri in base alle informazioni presenti nel momento in cui si attiva una compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-952">If you don't configure the parameters, the system will automatically attribute values to the parameters according to the information present at the time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="06e62-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-953">11.1.1.</span></span> <span data-ttu-id="06e62-954">Concentrazione dei dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="06e62-954">Usage condenser</span></span>
<span data-ttu-id="06e62-955">Gli utenti o gli elementi con pochi punti di utilizzo possono contenere una quantità di dati non significativi maggiore delle informazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="06e62-956">Il sistema tenta di stimare il numero minimo di punti di utilizzo per utente/elemento da usare in un modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-956">The system attempts to predict the minimal number of usage points per user/item to be used in a model.</span></span> <span data-ttu-id="06e62-957">Questo numero sarà compreso nell'intervallo definito dai parametri ItemCutoffLowerBound e ItemCutoffUpperBound per gli elementi e nell'intervallo definito dai parametri UserCutOffLowerBound e UserCutoffUpperBound per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="06e62-957">This number will be within the range defined by the ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and the range defined by the UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="06e62-958">L'effetto di concentrazione di elementi o utenti può essere ridotto impostando su zero almeno uno dei limiti corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="06e62-958">The condenser effect on items or users can be minimized by setting at least one of the corresponding bounds to zero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="06e62-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-959">11.1.2.</span></span> <span data-ttu-id="06e62-960">Parametri di compilazione della classifica</span><span class="sxs-lookup"><span data-stu-id="06e62-960">Rank build parameters</span></span>
<span data-ttu-id="06e62-961">La tabella seguente illustra i parametri per una compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-961">The table below depicts the build parameters for a rank build.</span></span>

| <span data-ttu-id="06e62-962">Chiave</span><span class="sxs-lookup"><span data-stu-id="06e62-962">Key</span></span> | <span data-ttu-id="06e62-963">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-963">Description</span></span> | <span data-ttu-id="06e62-964">Tipo</span><span class="sxs-lookup"><span data-stu-id="06e62-964">Type</span></span> | <span data-ttu-id="06e62-965">Valore valido</span><span class="sxs-lookup"><span data-stu-id="06e62-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="06e62-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="06e62-966">NumberOfModelIterations</span></span> |<span data-ttu-id="06e62-967">Il numero di iterazioni eseguite dal modello viene riflesso dal tempo di calcolo complessivo e dall'accuratezza del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-967">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="06e62-968">A un numero più alto corrisponderà una migliore accuratezza, ma il tempo di calcolo sarà maggiore.</span><span class="sxs-lookup"><span data-stu-id="06e62-968">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="06e62-969">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-969">Integer</span></span> |<span data-ttu-id="06e62-970">10-50</span><span class="sxs-lookup"><span data-stu-id="06e62-970">10-50</span></span> |
| <span data-ttu-id="06e62-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="06e62-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="06e62-972">Il numero di dimensioni è correlato al numero di "funzionalità" che il modello proverà a trovare nei dati.</span><span class="sxs-lookup"><span data-stu-id="06e62-972">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="06e62-973">L'aumento del numero di dimensioni consentirà l'ottimizzazione dei risultati in cluster più piccoli.</span><span class="sxs-lookup"><span data-stu-id="06e62-973">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="06e62-974">Troppe dimensioni impediranno tuttavia al modello di trovare correlazioni tra gli elementi.</span><span class="sxs-lookup"><span data-stu-id="06e62-974">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="06e62-975">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-975">Integer</span></span> |<span data-ttu-id="06e62-976">10-40</span><span class="sxs-lookup"><span data-stu-id="06e62-976">10-40</span></span> |
| <span data-ttu-id="06e62-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="06e62-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="06e62-978">Definisce il limite minimo dell'elemento per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-978">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="06e62-979">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-979">See usage condenser above.</span></span> |<span data-ttu-id="06e62-980">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-980">Integer</span></span> |<span data-ttu-id="06e62-981">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="06e62-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="06e62-983">Definisce il limite massimo dell'elemento per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-983">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="06e62-984">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-984">See usage condenser above.</span></span> |<span data-ttu-id="06e62-985">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-985">Integer</span></span> |<span data-ttu-id="06e62-986">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="06e62-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="06e62-988">Definisce il limite minimo dell'utente per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-988">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="06e62-989">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-989">See usage condenser above.</span></span> |<span data-ttu-id="06e62-990">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-990">Integer</span></span> |<span data-ttu-id="06e62-991">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="06e62-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="06e62-993">Definisce il limite massimo dell'utente per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-993">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="06e62-994">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-994">See usage condenser above.</span></span> |<span data-ttu-id="06e62-995">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-995">Integer</span></span> |<span data-ttu-id="06e62-996">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="06e62-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-997">11.1.3.</span></span> <span data-ttu-id="06e62-998">Parametri della compilazione di raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="06e62-998">Recommendation build parameters</span></span>
<span data-ttu-id="06e62-999">La tabella seguente illustra i parametri per la compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-999">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="06e62-1000">Chiave</span><span class="sxs-lookup"><span data-stu-id="06e62-1000">Key</span></span> | <span data-ttu-id="06e62-1001">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-1001">Description</span></span> | <span data-ttu-id="06e62-1002">Tipo</span><span class="sxs-lookup"><span data-stu-id="06e62-1002">Type</span></span> | <span data-ttu-id="06e62-1003">Valore valido</span><span class="sxs-lookup"><span data-stu-id="06e62-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="06e62-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="06e62-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="06e62-1005">Il numero di iterazioni eseguite dal modello viene riflesso dal tempo di calcolo complessivo e dall'accuratezza del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1005">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="06e62-1006">A un numero più alto corrisponderà una migliore accuratezza, ma il tempo di calcolo sarà maggiore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1006">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="06e62-1007">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1007">Integer</span></span> |<span data-ttu-id="06e62-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="06e62-1008">10-50</span></span> |
| <span data-ttu-id="06e62-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="06e62-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="06e62-1010">Il numero di dimensioni è correlato al numero di "funzionalità" che il modello proverà a trovare nei dati.</span><span class="sxs-lookup"><span data-stu-id="06e62-1010">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="06e62-1011">L'aumento del numero di dimensioni consentirà l'ottimizzazione dei risultati in cluster più piccoli.</span><span class="sxs-lookup"><span data-stu-id="06e62-1011">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="06e62-1012">Troppe dimensioni impediranno tuttavia al modello di trovare correlazioni tra gli elementi.</span><span class="sxs-lookup"><span data-stu-id="06e62-1012">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="06e62-1013">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1013">Integer</span></span> |<span data-ttu-id="06e62-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="06e62-1014">10-40</span></span> |
| <span data-ttu-id="06e62-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="06e62-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="06e62-1016">Definisce il limite minimo dell'elemento per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1016">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="06e62-1017">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1017">See usage condenser above.</span></span> |<span data-ttu-id="06e62-1018">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1018">Integer</span></span> |<span data-ttu-id="06e62-1019">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="06e62-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="06e62-1021">Definisce il limite massimo dell'elemento per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1021">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="06e62-1022">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1022">See usage condenser above.</span></span> |<span data-ttu-id="06e62-1023">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1023">Integer</span></span> |<span data-ttu-id="06e62-1024">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="06e62-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="06e62-1026">Definisce il limite minimo dell'utente per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1026">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="06e62-1027">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1027">See usage condenser above.</span></span> |<span data-ttu-id="06e62-1028">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1028">Integer</span></span> |<span data-ttu-id="06e62-1029">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="06e62-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="06e62-1031">Definisce il limite massimo dell'utente per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1031">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="06e62-1032">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1032">See usage condenser above.</span></span> |<span data-ttu-id="06e62-1033">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1033">Integer</span></span> |<span data-ttu-id="06e62-1034">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-1035">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-1035">Description</span></span> |<span data-ttu-id="06e62-1036">Descrizione della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1036">Build description.</span></span> |<span data-ttu-id="06e62-1037">String</span><span class="sxs-lookup"><span data-stu-id="06e62-1037">String</span></span> |<span data-ttu-id="06e62-1038">Qualsiasi testo, con un massimo di 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="06e62-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="06e62-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="06e62-1039">EnableModelingInsights</span></span> |<span data-ttu-id="06e62-1040">Consente di calcolare la metrica nel modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1040">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="06e62-1041">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1041">Boolean</span></span> |<span data-ttu-id="06e62-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="06e62-1042">True/False</span></span> |
| <span data-ttu-id="06e62-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="06e62-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="06e62-1044">Indica se le funzionalità possono essere usate in ordine per migliorare il modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1044">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="06e62-1045">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1045">Boolean</span></span> |<span data-ttu-id="06e62-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="06e62-1046">True/False</span></span> |
| <span data-ttu-id="06e62-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="06e62-1047">ModelingFeatureList</span></span> |<span data-ttu-id="06e62-1048">Elenco con valori delimitati da virgole dei nomi di funzionalità da usare nella compilazione di raccomandazioni, allo scopo di migliorare la raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1048">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="06e62-1049">String</span><span class="sxs-lookup"><span data-stu-id="06e62-1049">String</span></span> |<span data-ttu-id="06e62-1050">Nomi di funzionalità, con un massimo di 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="06e62-1050">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="06e62-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="06e62-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="06e62-1052">Indica se la raccomandazione dovrà effettuare il push anche degli elementi ignoti in base alla somiglianza di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-1052">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="06e62-1053">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1053">Boolean</span></span> |<span data-ttu-id="06e62-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="06e62-1054">True/False</span></span> |
| <span data-ttu-id="06e62-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="06e62-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="06e62-1056">Indica se le funzionalità possono essere usate nella motivazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="06e62-1057">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1057">Boolean</span></span> |<span data-ttu-id="06e62-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="06e62-1058">True/False</span></span> |
| <span data-ttu-id="06e62-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="06e62-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="06e62-1060">Elenco con valori delimitati da virgole dei nomi delle funzionalità da usare nelle frasi relative alla motivazione (ad esempio, le spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1060">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="06e62-1061">String</span><span class="sxs-lookup"><span data-stu-id="06e62-1061">String</span></span> |<span data-ttu-id="06e62-1062">Nomi di funzionalità, con un massimo di 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="06e62-1062">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="06e62-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="06e62-1063">EnableU2I</span></span> |<span data-ttu-id="06e62-1064">Consente la raccomandazione personalizzata, nota anche come</span><span class="sxs-lookup"><span data-stu-id="06e62-1064">Allow the personalized recommendation a.k.a.</span></span> <span data-ttu-id="06e62-1065">U2I (raccomandazioni da utente a elemento).</span><span class="sxs-lookup"><span data-stu-id="06e62-1065">U2I (user to item recommendations).</span></span> |<span data-ttu-id="06e62-1066">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1066">Boolean</span></span> |<span data-ttu-id="06e62-1067">True/False (valore predefinito true)</span><span class="sxs-lookup"><span data-stu-id="06e62-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="06e62-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="06e62-1068">11.1.4.</span></span> <span data-ttu-id="06e62-1069">Parametri della compilazione FBT</span><span class="sxs-lookup"><span data-stu-id="06e62-1069">FBT build parameters</span></span>
<span data-ttu-id="06e62-1070">La tabella seguente illustra i parametri per la compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1070">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="06e62-1071">Chiave</span><span class="sxs-lookup"><span data-stu-id="06e62-1071">Key</span></span> | <span data-ttu-id="06e62-1072">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-1072">Description</span></span> | <span data-ttu-id="06e62-1073">Tipo</span><span class="sxs-lookup"><span data-stu-id="06e62-1073">Type</span></span> | <span data-ttu-id="06e62-1074">Valore valido (predefinito)</span><span class="sxs-lookup"><span data-stu-id="06e62-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="06e62-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="06e62-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="06e62-1076">Indica il livello conservativo del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1076">How conservative the model is.</span></span> <span data-ttu-id="06e62-1077">Numero di co-occorrenze di elementi da considerare per la creazione del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1077">Number of co-occurrences of items to be considered for modeling.</span></span> |<span data-ttu-id="06e62-1078">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1078">Integer</span></span> |<span data-ttu-id="06e62-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="06e62-1079">3-50 (6)</span></span> |
| <span data-ttu-id="06e62-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="06e62-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="06e62-1081">Limita il numero di elementi in un set frequente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1081">Bounds the number of items in a frequent set.</span></span> |<span data-ttu-id="06e62-1082">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1082">Integer</span></span> |<span data-ttu-id="06e62-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="06e62-1083">2-3 (2)</span></span> |
| <span data-ttu-id="06e62-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="06e62-1084">FbtMinimalScore</span></span> |<span data-ttu-id="06e62-1085">Punteggio minimo che un set frequente deve avere per essere incluso nei risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="06e62-1085">Minimal score that a frequent set should have in order to be included in the returned results.</span></span> <span data-ttu-id="06e62-1086">Più alto è il valore, migliori saranno i risultati.</span><span class="sxs-lookup"><span data-stu-id="06e62-1086">The higher the better.</span></span> |<span data-ttu-id="06e62-1087">Double</span><span class="sxs-lookup"><span data-stu-id="06e62-1087">Double</span></span> |<span data-ttu-id="06e62-1088">0 e superiore (0)</span><span class="sxs-lookup"><span data-stu-id="06e62-1088">0 and above (0)</span></span> |
| <span data-ttu-id="06e62-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="06e62-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="06e62-1090">Definisce la funzione di somiglianza da usare per la compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1090">Defines the similarity function to be used by the build.</span></span> <span data-ttu-id="06e62-1091">L’accuratezza favorisce la serendipità, la co-occorrenza favorisce la prevedibilità e Jaccard è un interessante compromesso tra i due.</span><span class="sxs-lookup"><span data-stu-id="06e62-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between the two.</span></span> |<span data-ttu-id="06e62-1092">String</span><span class="sxs-lookup"><span data-stu-id="06e62-1092">String</span></span> |<span data-ttu-id="06e62-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="06e62-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="06e62-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-1094">11.2.</span></span> <span data-ttu-id="06e62-1095">Attivare una compilazione di raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="06e62-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="06e62-1096">Per impostazione predefinita, questa API attiverà la compilazione di un modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="06e62-1097">Per attivare la compilazione della classifica (per assegnare un punteggio alle funzionalità), è necessario usare la variante dell'API di compilazione con il parametro del tipo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1097">To trigger a rank build (in order to score  features), the build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="06e62-1098">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1098">HTTP Method</span></span> | <span data-ttu-id="06e62-1099">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1100">POST</span><span class="sxs-lookup"><span data-stu-id="06e62-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1101">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="06e62-1102">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="06e62-1102">HEADER</span></span> |<span data-ttu-id="06e62-1103">`"Content-Type", "text/xml"` (Se si sta inviando il corpo della richiesta)</span><span class="sxs-lookup"><span data-stu-id="06e62-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="06e62-1104">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1104">Parameter Name</span></span> | <span data-ttu-id="06e62-1105">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1106">modelId</span></span> |<span data-ttu-id="06e62-1107">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1107">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="06e62-1108">userDescription</span></span> |<span data-ttu-id="06e62-1109">Identificatore testuale del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1109">Textual identifier of the catalog.</span></span> <span data-ttu-id="06e62-1110">Tenere presente che, se si usano degli spazi, è necessario codificarli con il simbolo %20.</span><span class="sxs-lookup"><span data-stu-id="06e62-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="06e62-1111">Vedere l'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1111">See example above.</span></span><br><span data-ttu-id="06e62-1112">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="06e62-1112">Max length: 50</span></span> |
| <span data-ttu-id="06e62-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1113">apiVersion</span></span> |<span data-ttu-id="06e62-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-1115">Request Body</span><span class="sxs-lookup"><span data-stu-id="06e62-1115">Request Body</span></span> |<span data-ttu-id="06e62-1116">Se lasciato vuoto, la compilazione verrà eseguita con i parametri di compilazione predefiniti.</span><span class="sxs-lookup"><span data-stu-id="06e62-1116">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="06e62-1117">Per impostare i parametri di compilazione, inviarli in formato XML nel corpo come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1117">If you want to set the build parameters, send the parameters as XML into the body as in the following sample.</span></span> <span data-ttu-id="06e62-1118">Per una spiegazione dei parametri, vedere la sezione "Parametri della compilazione".`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="06e62-1118">(See the "Build parameters" section for an explanation of the parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="06e62-1119">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-1119">**Response**:</span></span>

<span data-ttu-id="06e62-1120">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1121">Questa è un'API asincrona.</span><span class="sxs-lookup"><span data-stu-id="06e62-1121">This is an asynchronous API.</span></span> <span data-ttu-id="06e62-1122">Come risposta si otterrà un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="06e62-1123">Per sapere quando termina l'esecuzione della compilazione, è necessario chiamare l'API "Get Builds Status of a Model" e individuare l'ID compilazione nella risposta.</span><span class="sxs-lookup"><span data-stu-id="06e62-1123">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="06e62-1124">Tenere presente che una compilazione può richiedere minuti o ore, a seconda delle dimensioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="06e62-1124">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="06e62-1125">Non è possibile usare raccomandazioni finché la compilazione non viene completata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1125">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="06e62-1126">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="06e62-1126">Valid build status:</span></span>

* <span data-ttu-id="06e62-1127">Create: è stata creata una richiesta di compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="06e62-1128">Queued: la richiesta di compilazione è stata inviata e accodata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="06e62-1129">Building: la compilazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="06e62-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="06e62-1130">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="06e62-1131">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="06e62-1132">Cancelled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="06e62-1133">Cancelling: è stata inviata una richiesta di annullamento per la compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1133">Cancelling - A cancel request for the build was sent.</span></span>

<span data-ttu-id="06e62-1134">È possibile trovare l'ID compilazione nel percorso seguente: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="06e62-1134">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="06e62-1135">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="06e62-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-1136">11.3.</span></span> <span data-ttu-id="06e62-1137">Attivare la compilazione (di raccomandazioni, della classifica o FBT)</span><span class="sxs-lookup"><span data-stu-id="06e62-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="06e62-1138">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1138">HTTP Method</span></span> | <span data-ttu-id="06e62-1139">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1140">POST</span><span class="sxs-lookup"><span data-stu-id="06e62-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1141">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="06e62-1142">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="06e62-1142">HEADER</span></span> |<span data-ttu-id="06e62-1143">`"Content-Type", "text/xml"` (Se si sta inviando il corpo della richiesta)</span><span class="sxs-lookup"><span data-stu-id="06e62-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="06e62-1144">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1144">Parameter Name</span></span> | <span data-ttu-id="06e62-1145">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1146">modelId</span></span> |<span data-ttu-id="06e62-1147">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1147">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="06e62-1148">userDescription</span></span> |<span data-ttu-id="06e62-1149">Identificatore testuale del catalogo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1149">Textual identifier of the catalog.</span></span> <span data-ttu-id="06e62-1150">Tenere presente che, se si usano degli spazi, è necessario codificarli con il simbolo %20.</span><span class="sxs-lookup"><span data-stu-id="06e62-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="06e62-1151">Vedere l'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1151">See example above.</span></span><br><span data-ttu-id="06e62-1152">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="06e62-1152">Max length: 50</span></span> |
| <span data-ttu-id="06e62-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="06e62-1153">buildType</span></span> |<span data-ttu-id="06e62-1154">Tipo della compilazione da richiamare: </span><span class="sxs-lookup"><span data-stu-id="06e62-1154">Type of the build to invoke:</span></span> <br/> <span data-ttu-id="06e62-1155">- "Recommendation" per la compilazione di raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="06e62-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="06e62-1156">- "Ranking" per la compilazione di classifiche</span><span class="sxs-lookup"><span data-stu-id="06e62-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="06e62-1157">- "Fbt" per una compilazione FBT</span><span class="sxs-lookup"><span data-stu-id="06e62-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="06e62-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1158">apiVersion</span></span> |<span data-ttu-id="06e62-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-1160">Request Body</span><span class="sxs-lookup"><span data-stu-id="06e62-1160">Request Body</span></span> |<span data-ttu-id="06e62-1161">Se lasciato vuoto, la compilazione verrà eseguita con i parametri di compilazione predefiniti.</span><span class="sxs-lookup"><span data-stu-id="06e62-1161">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="06e62-1162">Per impostare i parametri di compilazione, inviarli in formato XML nel corpo come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1162">If you want to set build parameters, send them as XML into the body like in the following sample.</span></span> <span data-ttu-id="06e62-1163">Per la descrizione e l'elenco completo dei parametri, vedere la sezione "Parametri della compilazione".`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="06e62-1163">(See the "Build parameters" section for an explanation and full list of the parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="06e62-1164">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-1164">**Response**:</span></span>

<span data-ttu-id="06e62-1165">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1166">Questa è un'API asincrona.</span><span class="sxs-lookup"><span data-stu-id="06e62-1166">This is an asynchronous API.</span></span> <span data-ttu-id="06e62-1167">Come risposta si otterrà un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="06e62-1168">Per sapere quando termina l'esecuzione della compilazione, è necessario chiamare l'API "Get Builds Status of a Model" e individuare l'ID compilazione nella risposta.</span><span class="sxs-lookup"><span data-stu-id="06e62-1168">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="06e62-1169">Tenere presente che una compilazione può richiedere minuti o ore, a seconda delle dimensioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="06e62-1169">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="06e62-1170">Non è possibile usare raccomandazioni finché la compilazione non viene completata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1170">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="06e62-1171">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="06e62-1171">Valid build status:</span></span>

* <span data-ttu-id="06e62-1172">Create: il modello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1172">Create - Model was created.</span></span>
* <span data-ttu-id="06e62-1173">Queued: la compilazione del modello è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="06e62-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="06e62-1174">Building: la compilazione del modello è in corso.</span><span class="sxs-lookup"><span data-stu-id="06e62-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="06e62-1175">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="06e62-1176">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="06e62-1177">Cancelled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="06e62-1178">Cancelling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="06e62-1179">È possibile trovare l'ID compilazione nel percorso seguente: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="06e62-1179">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="06e62-1180">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="06e62-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="06e62-1181">11.4.</span></span> <span data-ttu-id="06e62-1182">Ottenere lo stato delle compilazioni di un modello</span><span class="sxs-lookup"><span data-stu-id="06e62-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="06e62-1183">Recupera le compilazioni e il relativo stato per un modello specifico.</span><span class="sxs-lookup"><span data-stu-id="06e62-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="06e62-1184">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1184">HTTP Method</span></span> | <span data-ttu-id="06e62-1185">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1186">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1187">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1188">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1188">Parameter Name</span></span> | <span data-ttu-id="06e62-1189">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1190">modelId</span></span> |<span data-ttu-id="06e62-1191">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1191">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="06e62-1192">onlyLastBuild</span></span> |<span data-ttu-id="06e62-1193">Indica se restituire l'intera cronologia di compilazioni del modello o solo lo stato della compilazione più recente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1193">Indicates whether to return all the build history of the model or only the status of the most recent build</span></span> |
| <span data-ttu-id="06e62-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1194">apiVersion</span></span> |<span data-ttu-id="06e62-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1195">1.0</span></span> |

<span data-ttu-id="06e62-1196">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-1196">**Response**:</span></span>

<span data-ttu-id="06e62-1197">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1198">La risposta include una voce per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1198">The response includes one entry per build.</span></span> <span data-ttu-id="06e62-1199">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1199">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1200">`feed/entry/content/properties/UserName` : nome dell'utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1200">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="06e62-1201">`feed/entry/content/properties/ModelName` : nome del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1201">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="06e62-1202">`feed/entry/content/properties/ModelId` : identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="06e62-1203">`feed/entry/content/properties/IsDeployed` : se la compilazione viene distribuita (nota anche come</span><span class="sxs-lookup"><span data-stu-id="06e62-1203">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="06e62-1204">compilazione attiva).</span><span class="sxs-lookup"><span data-stu-id="06e62-1204">active build).</span></span>
* <span data-ttu-id="06e62-1205">`feed/entry/content/properties/BuildId` : identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="06e62-1206">`feed/entry/content/properties/BuildType` : tipo della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1206">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="06e62-1207">`feed/entry/content/properties/Status` : stato della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="06e62-1208">Può essere uno dei seguenti: Error, Building, Queued, Cancelling, Cancelled, Success.</span><span class="sxs-lookup"><span data-stu-id="06e62-1208">Can be one of the following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="06e62-1209">`feed/entry/content/properties/StatusMessage` : messaggio di stato dettagliato (si applica solo a stati specifici).</span><span class="sxs-lookup"><span data-stu-id="06e62-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="06e62-1210">`feed/entry/content/properties/Progress` : stato di avanzamento della compilazione (%).</span><span class="sxs-lookup"><span data-stu-id="06e62-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="06e62-1211">`feed/entry/content/properties/StartTime` : data/ora di inizio della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="06e62-1212">`feed/entry/content/properties/EndTime` : data/ora di fine della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="06e62-1213">`feed/entry/content/properties/ExecutionTime` : durata della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="06e62-1214">`feed/entry/content/properties/ProgressStep` : dettagli relativi alla fase corrente di una compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="06e62-1214">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="06e62-1215">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="06e62-1215">Valid build status:</span></span>

* <span data-ttu-id="06e62-1216">Created: la voce della richiesta di compilazione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="06e62-1217">Queued: la richiesta di compilazione è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="06e62-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="06e62-1218">Building: la compilazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="06e62-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="06e62-1219">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="06e62-1220">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="06e62-1221">Cancelled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="06e62-1222">Cancelling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="06e62-1223">Valori validi per il tipo di compilazione:</span><span class="sxs-lookup"><span data-stu-id="06e62-1223">Valid values for build type:</span></span>

* <span data-ttu-id="06e62-1224">Rank: compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="06e62-1225">Recommendation: compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="06e62-1226">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="115-get-builds-status"></a><span data-ttu-id="06e62-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="06e62-1227">11.5.</span></span> <span data-ttu-id="06e62-1228">Ottenere lo stato delle compilazioni</span><span class="sxs-lookup"><span data-stu-id="06e62-1228">Get Builds Status</span></span>
<span data-ttu-id="06e62-1229">Recupera lo stato delle compilazioni di tutti i modelli di un utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="06e62-1230">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1230">HTTP Method</span></span> | <span data-ttu-id="06e62-1231">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1232">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1233">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1234">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1234">Parameter Name</span></span> | <span data-ttu-id="06e62-1235">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="06e62-1236">onlyLastBuild</span></span> |<span data-ttu-id="06e62-1237">Indica se restituire l'intera cronologia di compilazioni del modello o solo lo stato della compilazione più recente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1237">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="06e62-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1238">apiVersion</span></span> |<span data-ttu-id="06e62-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1239">1.0</span></span> |

<span data-ttu-id="06e62-1240">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-1240">**Response**:</span></span>

<span data-ttu-id="06e62-1241">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1242">La risposta include una voce per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1242">The response includes one entry per build.</span></span> <span data-ttu-id="06e62-1243">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1243">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1244">`feed/entry/content/properties/UserName` : nome dell'utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1244">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="06e62-1245">`feed/entry/content/properties/ModelName` : nome del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1245">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="06e62-1246">`feed/entry/content/properties/ModelId` : identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="06e62-1247">`feed/entry/content/properties/IsDeployed` : indica se la compilazione viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="06e62-1247">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed.</span></span>
* <span data-ttu-id="06e62-1248">`feed/entry/content/properties/BuildId` : identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="06e62-1249">`feed/entry/content/properties/BuildType` : tipo della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1249">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="06e62-1250">`feed/entry/content/properties/Status` : stato della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="06e62-1251">Può essere uno dei seguenti: Error, Building, Queued, Cancelled, Cancelling, Success.</span><span class="sxs-lookup"><span data-stu-id="06e62-1251">Can be one of the following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="06e62-1252">`feed/entry/content/properties/StatusMessage` : messaggio di stato dettagliato (si applica solo a stati specifici).</span><span class="sxs-lookup"><span data-stu-id="06e62-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="06e62-1253">`feed/entry/content/properties/Progress` : stato di avanzamento della compilazione (%).</span><span class="sxs-lookup"><span data-stu-id="06e62-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="06e62-1254">`feed/entry/content/properties/StartTime` : data/ora di inizio della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="06e62-1255">`feed/entry/content/properties/EndTime` : data/ora di fine della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="06e62-1256">`feed/entry/content/properties/ExecutionTime` : durata della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="06e62-1257">`feed/entry/content/properties/ProgressStep` : dettagli relativi alla fase corrente di una compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="06e62-1257">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="06e62-1258">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="06e62-1258">Valid build status:</span></span>

* <span data-ttu-id="06e62-1259">Created: la voce della richiesta di compilazione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="06e62-1260">Queued: la richiesta di compilazione è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="06e62-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="06e62-1261">Building: la compilazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="06e62-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="06e62-1262">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="06e62-1263">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="06e62-1264">Cancelled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="06e62-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="06e62-1265">Cancelling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="06e62-1266">Valori validi per il tipo di compilazione:</span><span class="sxs-lookup"><span data-stu-id="06e62-1266">Valid values for build type:</span></span>

* <span data-ttu-id="06e62-1267">Rank: compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="06e62-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="06e62-1268">Recommendation: compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="06e62-1269">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="116-delete-build"></a><span data-ttu-id="06e62-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="06e62-1270">11.6.</span></span> <span data-ttu-id="06e62-1271">Eliminare una compilazione</span><span class="sxs-lookup"><span data-stu-id="06e62-1271">Delete Build</span></span>
<span data-ttu-id="06e62-1272">Elimina una compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1272">Deletes a build.</span></span>

<span data-ttu-id="06e62-1273">NOTA: </span><span class="sxs-lookup"><span data-stu-id="06e62-1273">NOTE:</span></span> <br><span data-ttu-id="06e62-1274">Non è possibile eliminare una compilazione attiva.</span><span class="sxs-lookup"><span data-stu-id="06e62-1274">You cannot delete an active build.</span></span> <span data-ttu-id="06e62-1275">Per poterla eliminare, è necessario aggiornare il modello a una compilazione attiva diversa.</span><span class="sxs-lookup"><span data-stu-id="06e62-1275">The model should be updated to a different active build before you delete it.</span></span><br><span data-ttu-id="06e62-1276">Non è possibile eliminare una compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="06e62-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="06e62-1277">È necessario annullare prima la compilazione chiamando <strong>Annullare una compilazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="06e62-1277">You should cancel the build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="06e62-1278">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1278">HTTP Method</span></span> | <span data-ttu-id="06e62-1279">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1280">DELETE</span><span class="sxs-lookup"><span data-stu-id="06e62-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1281">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1282">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1282">Parameter Name</span></span> | <span data-ttu-id="06e62-1283">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-1284">buildId</span></span> |<span data-ttu-id="06e62-1285">Identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1285">Unique identifier of the build.</span></span> |
| <span data-ttu-id="06e62-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1286">apiVersion</span></span> |<span data-ttu-id="06e62-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1287">1.0</span></span> |

<span data-ttu-id="06e62-1288">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1288">**Response:**</span></span>

<span data-ttu-id="06e62-1289">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="06e62-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="06e62-1290">11.7.</span></span> <span data-ttu-id="06e62-1291">Annullare una compilazione</span><span class="sxs-lookup"><span data-stu-id="06e62-1291">Cancel Build</span></span>
<span data-ttu-id="06e62-1292">Annulla una compilazione nello stato di creazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="06e62-1293">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1293">HTTP Method</span></span> | <span data-ttu-id="06e62-1294">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="06e62-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1296">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1297">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1297">Parameter Name</span></span> | <span data-ttu-id="06e62-1298">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-1299">buildId</span></span> |<span data-ttu-id="06e62-1300">Identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1300">Unique identifier of the build.</span></span> |
| <span data-ttu-id="06e62-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1301">apiVersion</span></span> |<span data-ttu-id="06e62-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1302">1.0</span></span> |

<span data-ttu-id="06e62-1303">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1303">**Response:**</span></span>

<span data-ttu-id="06e62-1304">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="06e62-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="06e62-1305">11.8.</span></span> <span data-ttu-id="06e62-1306">Ottenere i parametri della compilazione</span><span class="sxs-lookup"><span data-stu-id="06e62-1306">Get Build Parameters</span></span>
<span data-ttu-id="06e62-1307">Recupera i parametri della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="06e62-1308">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1308">HTTP Method</span></span> | <span data-ttu-id="06e62-1309">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1310">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1311">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1312">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1312">Parameter Name</span></span> | <span data-ttu-id="06e62-1313">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-1314">buildId</span></span> |<span data-ttu-id="06e62-1315">Identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1315">Unique identifier of the build.</span></span> |
| <span data-ttu-id="06e62-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1316">apiVersion</span></span> |<span data-ttu-id="06e62-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1317">1.0</span></span> |

<span data-ttu-id="06e62-1318">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1318">**Response:**</span></span>

<span data-ttu-id="06e62-1319">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1320">L'API restituisce una raccolta di elementi chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="06e62-1321">Ogni elemento rappresenta un parametro e il relativo valore:</span><span class="sxs-lookup"><span data-stu-id="06e62-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="06e62-1322">`feed/entry/content/properties/Key` : nome del parametro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="06e62-1323">`feed/entry/content/properties/Value` : valore del parametro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="06e62-1324">La tabella seguente illustra il valore rappresentato da ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="06e62-1324">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="06e62-1325">Chiave</span><span class="sxs-lookup"><span data-stu-id="06e62-1325">Key</span></span> | <span data-ttu-id="06e62-1326">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-1326">Description</span></span> | <span data-ttu-id="06e62-1327">Tipo</span><span class="sxs-lookup"><span data-stu-id="06e62-1327">Type</span></span> | <span data-ttu-id="06e62-1328">Valore valido</span><span class="sxs-lookup"><span data-stu-id="06e62-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="06e62-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="06e62-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="06e62-1330">Il numero di iterazioni eseguite dal modello viene riflesso dal tempo di calcolo complessivo e dall'accuratezza del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1330">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="06e62-1331">A un numero più alto corrisponderà una migliore accuratezza, ma il tempo di calcolo sarà maggiore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1331">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="06e62-1332">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1332">Integer</span></span> |<span data-ttu-id="06e62-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="06e62-1333">10-50</span></span> |
| <span data-ttu-id="06e62-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="06e62-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="06e62-1335">Il numero di dimensioni è correlato al numero di "funzionalità" che il modello proverà a trovare nei dati.</span><span class="sxs-lookup"><span data-stu-id="06e62-1335">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="06e62-1336">L'aumento del numero di dimensioni consentirà l'ottimizzazione dei risultati in cluster più piccoli.</span><span class="sxs-lookup"><span data-stu-id="06e62-1336">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="06e62-1337">Troppe dimensioni impediranno tuttavia al modello di trovare correlazioni tra gli elementi.</span><span class="sxs-lookup"><span data-stu-id="06e62-1337">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="06e62-1338">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1338">Integer</span></span> |<span data-ttu-id="06e62-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="06e62-1339">10-40</span></span> |
| <span data-ttu-id="06e62-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="06e62-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="06e62-1341">Definisce il limite minimo dell'elemento per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1341">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="06e62-1342">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1342">See usage condenser above.</span></span> |<span data-ttu-id="06e62-1343">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1343">Integer</span></span> |<span data-ttu-id="06e62-1344">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="06e62-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="06e62-1346">Definisce il limite massimo dell'elemento per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1346">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="06e62-1347">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1347">See usage condenser above.</span></span> |<span data-ttu-id="06e62-1348">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1348">Integer</span></span> |<span data-ttu-id="06e62-1349">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="06e62-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="06e62-1351">Definisce il limite minimo dell'utente per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1351">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="06e62-1352">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1352">See usage condenser above.</span></span> |<span data-ttu-id="06e62-1353">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1353">Integer</span></span> |<span data-ttu-id="06e62-1354">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="06e62-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="06e62-1356">Definisce il limite massimo dell'utente per la concentrazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1356">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="06e62-1357">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1357">See usage condenser above.</span></span> |<span data-ttu-id="06e62-1358">Integer</span><span class="sxs-lookup"><span data-stu-id="06e62-1358">Integer</span></span> |<span data-ttu-id="06e62-1359">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="06e62-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="06e62-1360">Description</span><span class="sxs-lookup"><span data-stu-id="06e62-1360">Description</span></span> |<span data-ttu-id="06e62-1361">Descrizione della compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1361">Build description.</span></span> |<span data-ttu-id="06e62-1362">String</span><span class="sxs-lookup"><span data-stu-id="06e62-1362">String</span></span> |<span data-ttu-id="06e62-1363">Qualsiasi testo, con un massimo di 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="06e62-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="06e62-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="06e62-1364">EnableModelingInsights</span></span> |<span data-ttu-id="06e62-1365">Consente di calcolare la metrica nel modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1365">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="06e62-1366">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1366">Boolean</span></span> |<span data-ttu-id="06e62-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="06e62-1367">True/False</span></span> |
| <span data-ttu-id="06e62-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="06e62-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="06e62-1369">Indica se le funzionalità possono essere usate in ordine per migliorare il modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1369">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="06e62-1370">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1370">Boolean</span></span> |<span data-ttu-id="06e62-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="06e62-1371">True/False</span></span> |
| <span data-ttu-id="06e62-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="06e62-1372">ModelingFeatureList</span></span> |<span data-ttu-id="06e62-1373">Elenco con valori delimitati da virgole dei nomi di funzionalità da usare nella compilazione di raccomandazioni, allo scopo di migliorare la raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1373">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="06e62-1374">String</span><span class="sxs-lookup"><span data-stu-id="06e62-1374">String</span></span> |<span data-ttu-id="06e62-1375">Nomi di funzionalità, con un massimo di 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="06e62-1375">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="06e62-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="06e62-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="06e62-1377">Indica se la raccomandazione dovrà effettuare il push anche degli elementi ignoti in base alla somiglianza di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="06e62-1377">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="06e62-1378">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1378">Boolean</span></span> |<span data-ttu-id="06e62-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="06e62-1379">True/False</span></span> |
| <span data-ttu-id="06e62-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="06e62-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="06e62-1381">Indica se le funzionalità possono essere usate nella motivazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="06e62-1382">Boolean</span><span class="sxs-lookup"><span data-stu-id="06e62-1382">Boolean</span></span> |<span data-ttu-id="06e62-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="06e62-1383">True/False</span></span> |
| <span data-ttu-id="06e62-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="06e62-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="06e62-1385">Elenco con valori delimitati da virgole dei nomi delle funzionalità da usare nelle frasi relative alla motivazione (ad esempio, le spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1385">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="06e62-1386">String</span><span class="sxs-lookup"><span data-stu-id="06e62-1386">String</span></span> |<span data-ttu-id="06e62-1387">Nomi di funzionalità, con un massimo di 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="06e62-1387">Feature names, up to 512 chars</span></span> |

<span data-ttu-id="06e62-1388">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="06e62-1389">12. Raccomandazione</span><span class="sxs-lookup"><span data-stu-id="06e62-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="06e62-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-1390">12.1.</span></span> <span data-ttu-id="06e62-1391">Ottenere le raccomandazioni degli elementi (per la compilazione attiva)</span><span class="sxs-lookup"><span data-stu-id="06e62-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="06e62-1392">Ottenere le raccomandazioni della compilazione attiva di tipo "Recommendation" o "Fbt" in base a un elenco di elementi seeds (input).</span><span class="sxs-lookup"><span data-stu-id="06e62-1392">Get recommendations of the active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="06e62-1393">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1393">HTTP Method</span></span> | <span data-ttu-id="06e62-1394">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1395">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1396">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1397">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1397">Parameter Name</span></span> | <span data-ttu-id="06e62-1398">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1399">modelId</span></span> |<span data-ttu-id="06e62-1400">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1400">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="06e62-1401">itemIds</span></span> |<span data-ttu-id="06e62-1402">Elenco con valori delimitati da virgole degli elementi per i quali aggiungere raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1402">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="06e62-1403">Se la compilazione attiva è di tipo FBT, è possibile inviare un solo elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1403">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="06e62-1404">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="06e62-1404">Max length: 1024</span></span> |
| <span data-ttu-id="06e62-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="06e62-1405">numberOfResults</span></span> |<span data-ttu-id="06e62-1406">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="06e62-1406">Number of required results</span></span> <br> <span data-ttu-id="06e62-1407">Massimo: 150</span><span class="sxs-lookup"><span data-stu-id="06e62-1407">Max: 150</span></span> |
| <span data-ttu-id="06e62-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="06e62-1408">includeMetatadata</span></span> |<span data-ttu-id="06e62-1409">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="06e62-1409">Future use, always false</span></span> |
| <span data-ttu-id="06e62-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1410">apiVersion</span></span> |<span data-ttu-id="06e62-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1411">1.0</span></span> |

<span data-ttu-id="06e62-1412">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1412">**Response:**</span></span>

<span data-ttu-id="06e62-1413">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1414">La risposta include una voce per ogni elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1414">The response includes one entry per recommended item.</span></span> <span data-ttu-id="06e62-1415">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1415">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1416">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1417">`Feed\entry\content\properties\Name` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1417">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1418">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="06e62-1418">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="06e62-1419">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="06e62-1420">La risposta di esempio seguente include 10 elementi raccomandati.</span><span class="sxs-lookup"><span data-stu-id="06e62-1420">The example response below includes 10 recommended items.</span></span>

<span data-ttu-id="06e62-1421">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="06e62-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-1422">12.2.</span></span> <span data-ttu-id="06e62-1423">Ottenere le raccomandazioni degli elementi (di una compilazione specifica)</span><span class="sxs-lookup"><span data-stu-id="06e62-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="06e62-1424">Ottiene raccomandazioni di una compilazione specifica di tipo "Recommendation" o "Fbt".</span><span class="sxs-lookup"><span data-stu-id="06e62-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="06e62-1425">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1425">HTTP Method</span></span> | <span data-ttu-id="06e62-1426">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1427">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1428">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1429">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1429">Parameter Name</span></span> | <span data-ttu-id="06e62-1430">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1431">modelId</span></span> |<span data-ttu-id="06e62-1432">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1432">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="06e62-1433">itemIds</span></span> |<span data-ttu-id="06e62-1434">Elenco con valori delimitati da virgole degli elementi per i quali aggiungere raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1434">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="06e62-1435">Se la compilazione attiva è di tipo FBT, è possibile inviare un solo elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1435">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="06e62-1436">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="06e62-1436">Max length: 1024</span></span> |
| <span data-ttu-id="06e62-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="06e62-1437">numberOfResults</span></span> |<span data-ttu-id="06e62-1438">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="06e62-1438">Number of required results</span></span> <br> <span data-ttu-id="06e62-1439">Massimo: 150</span><span class="sxs-lookup"><span data-stu-id="06e62-1439">Max: 150</span></span> |
| <span data-ttu-id="06e62-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="06e62-1440">includeMetatadata</span></span> |<span data-ttu-id="06e62-1441">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="06e62-1441">Future use, always false</span></span> |
| <span data-ttu-id="06e62-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-1442">buildId</span></span> |<span data-ttu-id="06e62-1443">L'ID compilazione da usare per questa richiesta di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1443">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="06e62-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1444">apiVersion</span></span> |<span data-ttu-id="06e62-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1445">1.0</span></span> |

<span data-ttu-id="06e62-1446">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1446">**Response:**</span></span>

<span data-ttu-id="06e62-1447">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1448">La risposta include una voce per ogni elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1448">The response includes one entry per recommended item.</span></span> <span data-ttu-id="06e62-1449">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1449">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1450">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1451">`Feed\entry\content\properties\Name` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1451">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1452">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="06e62-1452">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="06e62-1453">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="06e62-1454">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="06e62-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-1455">12.3.</span></span> <span data-ttu-id="06e62-1456">Ottenere le raccomandazioni FBT (per la compilazione attiva)</span><span class="sxs-lookup"><span data-stu-id="06e62-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="06e62-1457">Ottiene le raccomandazioni della compilazione attiva di tipo "Fbt" in base a un elemento seed (input).</span><span class="sxs-lookup"><span data-stu-id="06e62-1457">Get recommendations of the active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="06e62-1458">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1458">HTTP Method</span></span> | <span data-ttu-id="06e62-1459">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1460">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1461">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1462">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1462">Parameter Name</span></span> | <span data-ttu-id="06e62-1463">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1464">modelId</span></span> |<span data-ttu-id="06e62-1465">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1465">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="06e62-1466">itemId</span></span> |<span data-ttu-id="06e62-1467">Elemento per il quale aggiungere raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1467">Item to recommend for.</span></span> <br><span data-ttu-id="06e62-1468">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="06e62-1468">Max length: 1024</span></span> |
| <span data-ttu-id="06e62-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="06e62-1469">numberOfResults</span></span> |<span data-ttu-id="06e62-1470">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="06e62-1470">Number of required results</span></span> <br><span data-ttu-id="06e62-1471">Massimo: 150</span><span class="sxs-lookup"><span data-stu-id="06e62-1471">Max: 150</span></span> |
| <span data-ttu-id="06e62-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="06e62-1472">minimalScore</span></span> |<span data-ttu-id="06e62-1473">Punteggio minimo che un set frequente deve avere per essere incluso nei risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="06e62-1473">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="06e62-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="06e62-1474">includeMetatadata</span></span> |<span data-ttu-id="06e62-1475">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="06e62-1475">Future use, always false</span></span> |
| <span data-ttu-id="06e62-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1476">apiVersion</span></span> |<span data-ttu-id="06e62-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1477">1.0</span></span> |

<span data-ttu-id="06e62-1478">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1478">**Response:**</span></span>

<span data-ttu-id="06e62-1479">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1480">La risposta include una voce per ogni set di elementi consigliati (un set di elementi che in genere vengono acquistati con l'elemento del valore di inizializzazione/input).</span><span class="sxs-lookup"><span data-stu-id="06e62-1480">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="06e62-1481">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1481">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1482">`Feed\entry\content\properties\Id1` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1483">`Feed\entry\content\properties\Name1` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1483">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1484">`Feed\entry\content\properties\Id2` : ID 2° elemento consigliato (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="06e62-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="06e62-1485">`Feed\entry\content\properties\Name2` : nome del 2° elemento (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="06e62-1485">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="06e62-1486">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="06e62-1486">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="06e62-1487">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="06e62-1488">La risposta di esempio seguente include tre set di elementi consigliati.</span><span class="sxs-lookup"><span data-stu-id="06e62-1488">The example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="06e62-1489">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="06e62-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="06e62-1490">12.4.</span></span> <span data-ttu-id="06e62-1491">Ottenere le raccomandazioni FBT (di una compilazione specifica)</span><span class="sxs-lookup"><span data-stu-id="06e62-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="06e62-1492">Ottenere le raccomandazioni di una compilazione specifica di tipo "Fbt".</span><span class="sxs-lookup"><span data-stu-id="06e62-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="06e62-1493">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1493">HTTP Method</span></span> | <span data-ttu-id="06e62-1494">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1495">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1496">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1497">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1497">Parameter Name</span></span> | <span data-ttu-id="06e62-1498">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1499">modelId</span></span> |<span data-ttu-id="06e62-1500">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1500">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="06e62-1501">itemId</span></span> |<span data-ttu-id="06e62-1502">Elemento per il quale aggiungere raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1502">Item to recommend for.</span></span> <br><span data-ttu-id="06e62-1503">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="06e62-1503">Max length: 1024</span></span> |
| <span data-ttu-id="06e62-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="06e62-1504">numberOfResults</span></span> |<span data-ttu-id="06e62-1505">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="06e62-1505">Number of required results</span></span> <br><span data-ttu-id="06e62-1506">Massimo: 150</span><span class="sxs-lookup"><span data-stu-id="06e62-1506">Max: 150</span></span> |
| <span data-ttu-id="06e62-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="06e62-1507">minimalScore</span></span> |<span data-ttu-id="06e62-1508">Punteggio minimo che un set frequente deve avere per essere incluso nei risultati restituiti.</span><span class="sxs-lookup"><span data-stu-id="06e62-1508">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="06e62-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="06e62-1509">includeMetatadata</span></span> |<span data-ttu-id="06e62-1510">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="06e62-1510">Future use, always false</span></span> |
| <span data-ttu-id="06e62-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-1511">buildId</span></span> |<span data-ttu-id="06e62-1512">L'ID compilazione da usare per questa richiesta di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1512">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="06e62-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1513">apiVersion</span></span> |<span data-ttu-id="06e62-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1514">1.0</span></span> |

<span data-ttu-id="06e62-1515">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1515">**Response:**</span></span>

<span data-ttu-id="06e62-1516">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1517">La risposta include una voce per ogni set di elementi consigliati (un set di elementi che in genere vengono acquistati con l'elemento del valore di inizializzazione/input).</span><span class="sxs-lookup"><span data-stu-id="06e62-1517">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="06e62-1518">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1518">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1519">`Feed\entry\content\properties\Id1` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1520">`Feed\entry\content\properties\Name1` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1520">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1521">`Feed\entry\content\properties\Id2` : ID 2° elemento consigliato (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="06e62-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="06e62-1522">`Feed\entry\content\properties\Name2` : nome del 2° elemento (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="06e62-1522">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="06e62-1523">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="06e62-1523">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="06e62-1524">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="06e62-1525">Vedere un esempio di risposta nella sezione 12.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="06e62-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="06e62-1526">12.5.</span></span> <span data-ttu-id="06e62-1527">Ottenere le raccomandazioni utente (per la compilazione attiva)</span><span class="sxs-lookup"><span data-stu-id="06e62-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="06e62-1528">Ottenere le raccomandazioni utente di una compilazione di tipo "Recommendation" contrassegnata come compilazione attiva.</span><span class="sxs-lookup"><span data-stu-id="06e62-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="06e62-1529">L'API restituirà un elenco di elementi stimati secondo la cronologia di utilizzo dell'utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1529">The API will return a list of predicted item according to the usage history of the user.</span></span>

<span data-ttu-id="06e62-1530">Note:</span><span class="sxs-lookup"><span data-stu-id="06e62-1530">Notes:</span></span> 

1. <span data-ttu-id="06e62-1531">Non esiste alcuna raccomandazione utente per la compilazione FBT.</span><span class="sxs-lookup"><span data-stu-id="06e62-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="06e62-1532">Se la compilazione attiva è FBT, questo metodo restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1532">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="06e62-1533">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1533">HTTP Method</span></span> | <span data-ttu-id="06e62-1534">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1535">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1536">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1537">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1537">Parameter Name</span></span> | <span data-ttu-id="06e62-1538">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1539">modelId</span></span> |<span data-ttu-id="06e62-1540">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1540">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1541">userId</span><span class="sxs-lookup"><span data-stu-id="06e62-1541">userId</span></span> |<span data-ttu-id="06e62-1542">Identificatore univoco dell'utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1542">Unique identifier of the user</span></span> |
| <span data-ttu-id="06e62-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="06e62-1543">numberOfResults</span></span> |<span data-ttu-id="06e62-1544">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="06e62-1544">Number of required results</span></span> |
| <span data-ttu-id="06e62-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="06e62-1545">includeMetatadata</span></span> |<span data-ttu-id="06e62-1546">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="06e62-1546">Future use, always false</span></span> |
| <span data-ttu-id="06e62-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1547">apiVersion</span></span> |<span data-ttu-id="06e62-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1548">1.0</span></span> |

<span data-ttu-id="06e62-1549">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1549">**Response:**</span></span>

<span data-ttu-id="06e62-1550">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1551">La risposta include una voce per ogni elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1551">The response includes one entry per recommended item.</span></span> <span data-ttu-id="06e62-1552">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1552">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1553">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1554">`Feed\entry\content\properties\Name` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1554">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1555">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="06e62-1555">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="06e62-1556">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="06e62-1557">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="06e62-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="06e62-1558">12.6.</span></span> <span data-ttu-id="06e62-1559">Ottenere le raccomandazioni utente con l'elenco di elementi (per la compilazione attiva)</span><span class="sxs-lookup"><span data-stu-id="06e62-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="06e62-1560">Ottenere raccomandazioni utente di una compilazione di tipo "Recommendation" contrassegnata come compilazione attiva con un elenco aggiuntivo di elementi</span><span class="sxs-lookup"><span data-stu-id="06e62-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="06e62-1561">L'API restituirà un elenco di elementi stimati secondo la cronologia di utilizzo dell'utente e gli elementi stimati aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="06e62-1561">The API will return a list of predicted item according to the usage history of the user and the additional provided items.</span></span>

<span data-ttu-id="06e62-1562">Note:</span><span class="sxs-lookup"><span data-stu-id="06e62-1562">Notes:</span></span> 

1. <span data-ttu-id="06e62-1563">Non esiste alcuna raccomandazione utente per la compilazione FBT.</span><span class="sxs-lookup"><span data-stu-id="06e62-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="06e62-1564">Se la compilazione attiva è FBT, questo metodo restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="06e62-1564">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="06e62-1565">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1565">HTTP Method</span></span> | <span data-ttu-id="06e62-1566">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1567">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1568">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1569">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1569">Parameter Name</span></span> | <span data-ttu-id="06e62-1570">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1571">modelId</span></span> |<span data-ttu-id="06e62-1572">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1572">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1573">userId</span><span class="sxs-lookup"><span data-stu-id="06e62-1573">userId</span></span> |<span data-ttu-id="06e62-1574">Identificatore univoco dell'utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1574">Unique identifier of the user</span></span> |
| <span data-ttu-id="06e62-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="06e62-1575">itemsIds</span></span> |<span data-ttu-id="06e62-1576">Elenco con valori delimitati da virgole degli elementi per i quali aggiungere raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1576">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="06e62-1577">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="06e62-1577">Max length: 1024</span></span> |
| <span data-ttu-id="06e62-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="06e62-1578">numberOfResults</span></span> |<span data-ttu-id="06e62-1579">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="06e62-1579">Number of required results</span></span> |
| <span data-ttu-id="06e62-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="06e62-1580">includeMetatadata</span></span> |<span data-ttu-id="06e62-1581">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="06e62-1581">Future use, always false</span></span> |
| <span data-ttu-id="06e62-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1582">apiVersion</span></span> |<span data-ttu-id="06e62-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1583">1.0</span></span> |

<span data-ttu-id="06e62-1584">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1584">**Response:**</span></span>

<span data-ttu-id="06e62-1585">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1586">La risposta include una voce per ogni elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1586">The response includes one entry per recommended item.</span></span> <span data-ttu-id="06e62-1587">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1587">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1588">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1589">`Feed\entry\content\properties\Name` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1589">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1590">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="06e62-1590">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="06e62-1591">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="06e62-1592">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="06e62-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="06e62-1593">12.7.</span></span> <span data-ttu-id="06e62-1594">Ottenere le raccomandazioni utente (di una compilazione specifica)</span><span class="sxs-lookup"><span data-stu-id="06e62-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="06e62-1595">Ottenere le raccomandazioni utente di una compilazione specifica di tipo "Recommendation".</span><span class="sxs-lookup"><span data-stu-id="06e62-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="06e62-1596">L'API restituirà un elenco di elementi stimati secondo la cronologia di utilizzo dell'utente (usato nella compilazione specifica).</span><span class="sxs-lookup"><span data-stu-id="06e62-1596">The API will return a list of predicted item according to the usage history of the user (used in the specific build).</span></span>

<span data-ttu-id="06e62-1597">Nota: non esiste alcuna raccomandazione utente per la compilazione FBT.</span><span class="sxs-lookup"><span data-stu-id="06e62-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="06e62-1598">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1598">HTTP Method</span></span> | <span data-ttu-id="06e62-1599">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1600">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1601">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1602">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1602">Parameter Name</span></span> | <span data-ttu-id="06e62-1603">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1604">modelId</span></span> |<span data-ttu-id="06e62-1605">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1605">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1606">userId</span><span class="sxs-lookup"><span data-stu-id="06e62-1606">userId</span></span> |<span data-ttu-id="06e62-1607">Identificatore univoco dell'utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1607">Unique identifier of the user</span></span> |
| <span data-ttu-id="06e62-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="06e62-1608">numberOfResults</span></span> |<span data-ttu-id="06e62-1609">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="06e62-1609">Number of required results</span></span> |
| <span data-ttu-id="06e62-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="06e62-1610">includeMetatadata</span></span> |<span data-ttu-id="06e62-1611">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="06e62-1611">Future use, always false</span></span> |
| <span data-ttu-id="06e62-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-1612">buildId</span></span> |<span data-ttu-id="06e62-1613">L'ID compilazione da usare per questa richiesta di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1613">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="06e62-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1614">apiVersion</span></span> |<span data-ttu-id="06e62-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1615">1.0</span></span> |

<span data-ttu-id="06e62-1616">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1616">**Response:**</span></span>

<span data-ttu-id="06e62-1617">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1618">La risposta include una voce per ogni elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1618">The response includes one entry per recommended item.</span></span> <span data-ttu-id="06e62-1619">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1619">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1620">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1621">`Feed\entry\content\properties\Name` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1621">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1622">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="06e62-1622">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="06e62-1623">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="06e62-1624">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="06e62-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="06e62-1625">12.8.</span></span> <span data-ttu-id="06e62-1626">Ottenere le raccomandazioni utente con l'elenco di elementi (di una compilazione specifica)</span><span class="sxs-lookup"><span data-stu-id="06e62-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="06e62-1627">Ottenere le raccomandazioni utente di una compilazione specifica di tipo "Recommendation" e l'elenco di elementi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="06e62-1627">Get user recommendations of a specific build of type "Recommendation" and the list of additional items.</span></span>

<span data-ttu-id="06e62-1628">L'API restituirà un elenco di elementi stimati secondo la cronologia di utilizzo dell'utente e l'elenco aggiuntivo di elementi.</span><span class="sxs-lookup"><span data-stu-id="06e62-1628">The API will return a list of predicted item according to the usage history of the user and the additional list of items.</span></span>

<span data-ttu-id="06e62-1629">Nota: non esiste alcuna raccomandazione utente per la compilazione FBT.</span><span class="sxs-lookup"><span data-stu-id="06e62-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="06e62-1630">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1630">HTTP Method</span></span> | <span data-ttu-id="06e62-1631">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1632">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1633">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1634">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1634">Parameter Name</span></span> | <span data-ttu-id="06e62-1635">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1636">modelId</span></span> |<span data-ttu-id="06e62-1637">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1637">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1638">userId</span><span class="sxs-lookup"><span data-stu-id="06e62-1638">userId</span></span> |<span data-ttu-id="06e62-1639">Identificatore univoco dell'utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1639">Unique identifier of the user</span></span> |
| <span data-ttu-id="06e62-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="06e62-1640">itemIds</span></span> |<span data-ttu-id="06e62-1641">Elenco con valori delimitati da virgole degli elementi per i quali aggiungere raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1641">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="06e62-1642">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="06e62-1642">Max length: 1024</span></span> |
| <span data-ttu-id="06e62-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="06e62-1643">numberOfResults</span></span> |<span data-ttu-id="06e62-1644">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="06e62-1644">Number of required results</span></span> |
| <span data-ttu-id="06e62-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="06e62-1645">includeMetatadata</span></span> |<span data-ttu-id="06e62-1646">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="06e62-1646">Future use, always false</span></span> |
| <span data-ttu-id="06e62-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-1647">buildId</span></span> |<span data-ttu-id="06e62-1648">L'ID compilazione da usare per questa richiesta di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="06e62-1648">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="06e62-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1649">apiVersion</span></span> |<span data-ttu-id="06e62-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1650">1.0</span></span> |

<span data-ttu-id="06e62-1651">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1651">**Response:**</span></span>

<span data-ttu-id="06e62-1652">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1653">La risposta include una voce per ogni elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1653">The response includes one entry per recommended item.</span></span> <span data-ttu-id="06e62-1654">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1654">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1655">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1656">`Feed\entry\content\properties\Name` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1656">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1657">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="06e62-1657">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="06e62-1658">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="06e62-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="06e62-1659">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="06e62-1660">13. Cronologia utilizzo utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1660">13. User Usage History</span></span>
<span data-ttu-id="06e62-1661">Una volta compilato un modello di raccomandazione, il sistema consentirà di recuperare la cronologia utente (elementi associati a un utente specifico) usata per la compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1661">Once a recommendation model was built the system will allow to retrieve the user history (items associated to a specific user) used for the build.</span></span>
<span data-ttu-id="06e62-1662">Questa API consente di recuperare la cronologia utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1662">This API allow to retrieve the user history</span></span>

<span data-ttu-id="06e62-1663">Nota: la cronologia utente è attualmente disponibile solo per le compilazioni raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1663">Note: the user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="06e62-1664">13.1 Recuperare la cronologia utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="06e62-1665">Recuperare l'elenco di elementi usati nella compilazione attiva o nella compilazione specificata per l'ID utente specificato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1665">Retrieve the list of item used in the active build or in the specified build for the given user id.</span></span>

| <span data-ttu-id="06e62-1666">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1666">HTTP Method</span></span> | <span data-ttu-id="06e62-1667">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1668">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1668">GET</span></span> |<span data-ttu-id="06e62-1669">Ottenere la cronologia utente per la compilazione attiva.</span><span class="sxs-lookup"><span data-stu-id="06e62-1669">Get the user history for the active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="06e62-1670">Ottenere la cronologia utente per la compilazione specifica `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="06e62-1670">Get the user history for the given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="06e62-1671">Esempio:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="06e62-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="06e62-1672">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1672">Parameter Name</span></span> | <span data-ttu-id="06e62-1673">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1674">modelId</span></span> |<span data-ttu-id="06e62-1675">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1675">the unique identifier of the model.</span></span> |
| <span data-ttu-id="06e62-1676">userId</span><span class="sxs-lookup"><span data-stu-id="06e62-1676">userId</span></span> |<span data-ttu-id="06e62-1677">Identificatore univoco dell'utente.</span><span class="sxs-lookup"><span data-stu-id="06e62-1677">the unique identifier of the user.</span></span> |
| <span data-ttu-id="06e62-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="06e62-1678">buildId</span></span> |<span data-ttu-id="06e62-1679">Parametro facoltativo, consente di indicare da quale compilazione deve essere recuperata la cronologia utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1679">optional parameter, allow to indicate from which build the user history should be fetch</span></span> |
| <span data-ttu-id="06e62-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1680">apiVersion</span></span> |<span data-ttu-id="06e62-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1681">1.0</span></span> |

<span data-ttu-id="06e62-1682">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1682">**Response:**</span></span>

<span data-ttu-id="06e62-1683">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1684">La risposta include una voce per ogni elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1684">The response includes one entry per recommended item.</span></span> <span data-ttu-id="06e62-1685">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="06e62-1685">Each entry has the following data:</span></span>

* <span data-ttu-id="06e62-1686">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="06e62-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="06e62-1687">`Feed\entry\content\properties\Name` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1687">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="06e62-1688">`Feed\entry\content\properties\Rating` : N/A.</span><span class="sxs-lookup"><span data-stu-id="06e62-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="06e62-1689">`Feed\entry\content\properties\Reasoning` : N/A.</span><span class="sxs-lookup"><span data-stu-id="06e62-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="06e62-1690">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="06e62-1691">14. Notifiche</span><span class="sxs-lookup"><span data-stu-id="06e62-1691">14. Notifications</span></span>
<span data-ttu-id="06e62-1692">L'API Recommendations di Azure Machine Learning crea notifiche quando nel sistema si verificano errori persistenti.</span><span class="sxs-lookup"><span data-stu-id="06e62-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in the system.</span></span> <span data-ttu-id="06e62-1693">Esistono 3 tipi di notifiche:</span><span class="sxs-lookup"><span data-stu-id="06e62-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="06e62-1694">Build failure: questa notifica viene attivata per ogni errore di compilazione.</span><span class="sxs-lookup"><span data-stu-id="06e62-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="06e62-1695">Data acquisition processing failure: questa notifica viene attivata quando, durante l'elaborazione degli eventi di utilizzo per ogni modello, si verificano più di 100 errori nell'arco di cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="06e62-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of usage events per model.</span></span>
3. <span data-ttu-id="06e62-1696">Recommendation consumption failure: questa notifica viene attivata quando, durante l'elaborazione delle richieste di raccomandazione per ogni modello, si verificano più di 100 errori nell'arco di cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="06e62-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="06e62-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="06e62-1697">14.1.</span></span> <span data-ttu-id="06e62-1698">Ottenere notifiche</span><span class="sxs-lookup"><span data-stu-id="06e62-1698">Get Notifications</span></span>
<span data-ttu-id="06e62-1699">Recupera tutte le notifiche relative a tutti i modelli o a un singolo modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1699">Retrieves all the notifications for all models or for a single model.</span></span>

| <span data-ttu-id="06e62-1700">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1700">HTTP Method</span></span> | <span data-ttu-id="06e62-1701">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1702">GET</span><span class="sxs-lookup"><span data-stu-id="06e62-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1703">Per ottenere tutte le notifiche relative a tutti i modelli:</span><span class="sxs-lookup"><span data-stu-id="06e62-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1704">Esempio per ottenere le notifiche relative a un modello specifico:</span><span class="sxs-lookup"><span data-stu-id="06e62-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="06e62-1705">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1705">Parameter Name</span></span> | <span data-ttu-id="06e62-1706">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1707">modelId</span></span> |<span data-ttu-id="06e62-1708">Parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="06e62-1708">Optional parameter.</span></span> <span data-ttu-id="06e62-1709">Se omesso, vengono restituite tutte le notifiche relative a tutti i modelli.</span><span class="sxs-lookup"><span data-stu-id="06e62-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="06e62-1710">Valore valido: identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1710">Valid value: unique identifier of the model.</span></span> |
| <span data-ttu-id="06e62-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1711">apiVersion</span></span> |<span data-ttu-id="06e62-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-1713">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-1713">Request Body</span></span> |<span data-ttu-id="06e62-1714">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-1714">NONE</span></span> |

<span data-ttu-id="06e62-1715">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="06e62-1715">**Response:**</span></span>

<span data-ttu-id="06e62-1716">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="06e62-1717">XML OData</span><span class="sxs-lookup"><span data-stu-id="06e62-1717">OData XML</span></span>

    The response includes one entry per notification. Each entry has the following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="06e62-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="06e62-1718">14.2.</span></span> <span data-ttu-id="06e62-1719">Eliminare le notifiche di modello</span><span class="sxs-lookup"><span data-stu-id="06e62-1719">Delete Model Notifications</span></span>
<span data-ttu-id="06e62-1720">Elimina tutte le notifiche di lettura relative a un modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="06e62-1721">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1721">HTTP Method</span></span> | <span data-ttu-id="06e62-1722">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1723">DELETE</span><span class="sxs-lookup"><span data-stu-id="06e62-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="06e62-1724">Esempio:</span><span class="sxs-lookup"><span data-stu-id="06e62-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1725">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1725">Parameter Name</span></span> | <span data-ttu-id="06e62-1726">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="06e62-1727">modelId</span></span> |<span data-ttu-id="06e62-1728">Identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="06e62-1728">Unique identifier of the model</span></span> |
| <span data-ttu-id="06e62-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1729">apiVersion</span></span> |<span data-ttu-id="06e62-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-1731">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-1731">Request Body</span></span> |<span data-ttu-id="06e62-1732">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-1732">NONE</span></span> |

<span data-ttu-id="06e62-1733">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-1733">**Response**:</span></span>

<span data-ttu-id="06e62-1734">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="06e62-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="06e62-1735">14.3.</span></span> <span data-ttu-id="06e62-1736">Eliminare le notifiche utente</span><span class="sxs-lookup"><span data-stu-id="06e62-1736">Delete User Notifications</span></span>
<span data-ttu-id="06e62-1737">Elimina tutte le notifiche relative a tutti i modelli.</span><span class="sxs-lookup"><span data-stu-id="06e62-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="06e62-1738">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="06e62-1738">HTTP Method</span></span> | <span data-ttu-id="06e62-1739">URI</span><span class="sxs-lookup"><span data-stu-id="06e62-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1740">DELETE</span><span class="sxs-lookup"><span data-stu-id="06e62-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="06e62-1741">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="06e62-1741">Parameter Name</span></span> | <span data-ttu-id="06e62-1742">Valori validi</span><span class="sxs-lookup"><span data-stu-id="06e62-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="06e62-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="06e62-1743">apiVersion</span></span> |<span data-ttu-id="06e62-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="06e62-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="06e62-1745">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="06e62-1745">Request Body</span></span> |<span data-ttu-id="06e62-1746">Nessuno</span><span class="sxs-lookup"><span data-stu-id="06e62-1746">NONE</span></span> |

<span data-ttu-id="06e62-1747">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="06e62-1747">**Response**:</span></span>

<span data-ttu-id="06e62-1748">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="06e62-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="06e62-1749">15. Note legali</span><span class="sxs-lookup"><span data-stu-id="06e62-1749">15. Legal</span></span>
<span data-ttu-id="06e62-1750">Questo documento viene fornito "così com'è".</span><span class="sxs-lookup"><span data-stu-id="06e62-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="06e62-1751">Le informazioni e le indicazioni riportate nel presente documento, inclusi URL e altri riferimenti a siti Web Internet, sono soggette a modifica senza preavviso.</span><span class="sxs-lookup"><span data-stu-id="06e62-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="06e62-1752">Alcuni esempi usati in questo documento vengono forniti a scopo puramente illustrativo e sono fittizi.</span><span class="sxs-lookup"><span data-stu-id="06e62-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="06e62-1753">Nessuna associazione reale o connessione è intenzionale o può essere desunta.</span><span class="sxs-lookup"><span data-stu-id="06e62-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="06e62-1754">Il presente documento non fornisce all'utente alcun diritto legale rispetto a qualsiasi proprietà intellettuale in qualsiasi prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06e62-1754">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="06e62-1755">È possibile copiare e usare il presente documento per scopi interni e di riferimento.</span><span class="sxs-lookup"><span data-stu-id="06e62-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="06e62-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="06e62-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="06e62-1757">Tutti i diritti sono riservati.</span><span class="sxs-lookup"><span data-stu-id="06e62-1757">All rights reserved.</span></span>

