---
title: la documentazione dell'API di apprendimento indicazioni aaaMachine | Documenti Microsoft
description: Documentazione di Azure Machine Learning indicazioni API per un motore di indicazioni disponibile in Microsoft Azure Marketplace hello.
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
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="4a953-103">Documentazione relativa all'API Recommendations di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4a953-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="4a953-104">È consigliabile iniziare utilizzando hello indicazioni API cognitivi servizio invece di questa versione.</span><span class="sxs-lookup"><span data-stu-id="4a953-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="4a953-105">Hello servizio cognitivi indicazioni andrà a sostituire questo servizio e tutte le nuove funzionalità hello verranno sviluppate non esiste.</span><span class="sxs-lookup"><span data-stu-id="4a953-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="4a953-106">Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.</span><span class="sxs-lookup"><span data-stu-id="4a953-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="4a953-107">Altre informazioni, vedere [toohello migrazione nuovo servizio cognitivi](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="4a953-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="4a953-108">Questo documento illustra le API Recommendations di Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4a953-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="4a953-109">1. Panoramica generale</span><span class="sxs-lookup"><span data-stu-id="4a953-109">1. General overview</span></span>
<span data-ttu-id="4a953-110">Questo è un documento di riferimento dell'API.</span><span class="sxs-lookup"><span data-stu-id="4a953-110">This document is an API reference.</span></span> <span data-ttu-id="4a953-111">È consigliabile iniziare con "Azure Machine Learning raccomandazione – avvio rapido" documento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="4a953-112">Hello Azure Machine Learning indicazioni API può essere suddivisi in gruppi logici seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="4a953-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="4a953-113"><ins>Limitazioni</ins>: limitazioni dell'API Recommendations.</span><span class="sxs-lookup"><span data-stu-id="4a953-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="4a953-114"><ins>Informazioni generali</ins>: informazioni su autenticazione, URI del servizio e controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="4a953-115"><ins>Modello Basic</ins> -API che consentono operazioni di base hello toodo nel modello (ad esempio, creare, aggiornare ed eliminare un modello).</span><span class="sxs-lookup"><span data-stu-id="4a953-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="4a953-116"><ins>Modello avanzate</ins> -API che consentono la comprensione dei dati nel modello hello tooget avanzate.</span><span class="sxs-lookup"><span data-stu-id="4a953-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="4a953-117"><ins>Le regole di Business del modello</ins> -API che consentono di regole di business toomanage sui risultati di raccomandazione modello hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="4a953-118"><ins>Catalogo</ins> -API che consentono operazioni di base toodo per un catalogo del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="4a953-119">Il catalogo contiene informazioni sui metadati per gli elementi di hello hello dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="4a953-120"><ins>Funzionalità</ins> -API che consentono di tooget informazioni dettagliate sull'elemento nel catalogo di hello e come toouse questo indicazioni migliori toobuild di informazioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="4a953-121"><ins>Dati di utilizzo</ins> -API che consentono operazioni di base sui dati di utilizzo del modello hello toodo.</span><span class="sxs-lookup"><span data-stu-id="4a953-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="4a953-122">Dati di utilizzo in form di base hello è costituito da righe che includono coppie di &#60; userId &#62; &#60; itemId &#62;.</span><span class="sxs-lookup"><span data-stu-id="4a953-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="4a953-123"><ins>Compilare</ins> - API che consentono di tootrigger un modello di compilazione e di eseguire operazioni di base che sono correlati toothis generazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="4a953-124">È possibile attivare la compilazione di un modello solo se sono disponibili dati di utilizzo rilevanti.</span><span class="sxs-lookup"><span data-stu-id="4a953-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="4a953-125"><ins>Indicazione</ins> -API che consentono di indicazioni tooconsume al termine della compilazione hello di un modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="4a953-126"><ins>Dati utente</ins> -API che consentono di toofetch informazioni sui dati di utilizzo di hello utente.</span><span class="sxs-lookup"><span data-stu-id="4a953-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="4a953-127"><ins>Le notifiche</ins> -API che consentono di notifiche tooreceive sui problemi relativi alle relative operazioni tooyour API.</span><span class="sxs-lookup"><span data-stu-id="4a953-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="4a953-128">(Ad esempio, si siano segnalando i dati di utilizzo tramite l'acquisizione dei dati e la maggior parte degli eventi di hello elaborazione hanno esito negativo.</span><span class="sxs-lookup"><span data-stu-id="4a953-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="4a953-129">viene generata una notifica di errore.</span><span class="sxs-lookup"><span data-stu-id="4a953-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="4a953-130">2. Limitazioni</span><span class="sxs-lookup"><span data-stu-id="4a953-130">2. Limitations</span></span>
* <span data-ttu-id="4a953-131">numero massimo di Hello di modelli per ogni sottoscrizione è 10.</span><span class="sxs-lookup"><span data-stu-id="4a953-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="4a953-132">numero massimo di Hello di compilazioni per ogni modello è 20.</span><span class="sxs-lookup"><span data-stu-id="4a953-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="4a953-133">numero massimo di Hello di elementi che può contenere un catalogo è 100.000.</span><span class="sxs-lookup"><span data-stu-id="4a953-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="4a953-134">numero massimo di Hello di punti di utilizzo che vengono conservati è ~ 5.000.000.</span><span class="sxs-lookup"><span data-stu-id="4a953-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="4a953-135">Hello meno recente verrà eliminato verranno caricati o segnalati nuovi.</span><span class="sxs-lookup"><span data-stu-id="4a953-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="4a953-136">dimensione massima di Hello di dati che possono essere inviati in POST (ad esempio, Importa dati del catalogo, importazione dati di utilizzo) è pari a 200MB.</span><span class="sxs-lookup"><span data-stu-id="4a953-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="4a953-137">numero massimo di Hello di elementi che possono essere formulate per durante il recupero delle indicazioni è 150.</span><span class="sxs-lookup"><span data-stu-id="4a953-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="4a953-138">3. API: informazioni generali</span><span class="sxs-lookup"><span data-stu-id="4a953-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="4a953-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-139">3.1.</span></span> <span data-ttu-id="4a953-140">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="4a953-140">Authentication</span></span>
<span data-ttu-id="4a953-141">Seguire le istruzioni di Microsoft Azure Marketplace hello riguardanti l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="4a953-142">marketplace Hello supporta un metodo di autenticazione Basic o OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="4a953-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-143">3.2.</span></span> <span data-ttu-id="4a953-144">URI del servizio</span><span class="sxs-lookup"><span data-stu-id="4a953-144">Service URI</span></span>
<span data-ttu-id="4a953-145">Hello URI radice del servizio per le API di Azure Machine Learning indicazioni hello è [qui.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="4a953-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="4a953-146">URI del servizio completo Hello viene espresso utilizzando gli elementi della specifica OData hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="4a953-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-147">3.3.</span></span> <span data-ttu-id="4a953-148">Versione dell'API</span><span class="sxs-lookup"><span data-stu-id="4a953-148">API version</span></span>
<span data-ttu-id="4a953-149">Ogni chiamata API al fine di hello, sarà necessario un parametro di query denominato apiVersion che deve essere impostata too1.0.</span><span class="sxs-lookup"><span data-stu-id="4a953-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="4a953-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="4a953-150">3.4.</span></span> <span data-ttu-id="4a953-151">Gli ID fanno distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="4a953-151">IDs are case sensitive</span></span>
<span data-ttu-id="4a953-152">Gli ID, restituiti da una delle API, hello tra maiuscole e minuscole e devono essere usati come tali, quando viene passato come parametro nelle chiamate API successive.</span><span class="sxs-lookup"><span data-stu-id="4a953-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="4a953-153">Ad esempio, per gli ID dei modelli e del catalogo viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4a953-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="4a953-154">4. Qualità delle raccomandazioni ed elementi ignoti</span><span class="sxs-lookup"><span data-stu-id="4a953-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="4a953-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-155">4.1.</span></span> <span data-ttu-id="4a953-156">Qualità delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="4a953-156">Recommendation quality</span></span>
<span data-ttu-id="4a953-157">Creazione di un modello di raccomandazione è in genere sufficiente indicazioni di tooprovide tooallow hello del sistema.</span><span class="sxs-lookup"><span data-stu-id="4a953-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="4a953-158">Tuttavia, qualità delle indicazioni varia in base all'utilizzo di hello elaborato e hello copertura del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="4a953-159">Ad esempio se si dispone di molti elementi ignoti (elementi senza un utilizzo significativo), il sistema hello avrà difficoltà a fornire un'indicazione di tale elemento o l'utilizzo di tale elemento come uno di quelli consigliati.</span><span class="sxs-lookup"><span data-stu-id="4a953-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="4a953-160">Problema di elementi ignoti hello tooovercome ordine, il sistema hello consente l'utilizzo di hello dei metadati delle indicazioni di hello elementi tooenhance hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="4a953-161">Questi metadati sono funzionalità tooas cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="4a953-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="4a953-162">L'autore di un libro o l'attore di un film è un esempio tipico di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="4a953-163">Funzionalità disponibili tramite catalogo hello sotto forma di hello di stringhe chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="4a953-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="4a953-164">Per il formato completo hello hello dei file di catalogo, consultare toohello [importare catalogo sezione](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="4a953-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="4a953-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-165">4.2.</span></span> <span data-ttu-id="4a953-166">Compilazione della classifica</span><span class="sxs-lookup"><span data-stu-id="4a953-166">Rank build</span></span>
<span data-ttu-id="4a953-167">Caratteristiche consentono di migliorare il modello di raccomandazione hello, ma toodo richiede pertanto l'uso di hello di funzionalità significative.</span><span class="sxs-lookup"><span data-stu-id="4a953-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="4a953-168">A questo scopo è stata introdotta una nuova compilazione per la definizione della classifica,</span><span class="sxs-lookup"><span data-stu-id="4a953-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="4a953-169">Questa compilazione verrà rank utilità hello delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="4a953-170">Una funzionalità significativa presenta un punteggio di classificazione minimo pari a 2.</span><span class="sxs-lookup"><span data-stu-id="4a953-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="4a953-171">Dopo avere acquisito familiarità quali funzioni hello sono significativi, attivare una compilazione di raccomandazione con elenco hello (o sottoelenco) delle funzionalità significative.</span><span class="sxs-lookup"><span data-stu-id="4a953-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="4a953-172">È possibile toouse che queste funzionalità per il miglioramento di hello del warm sia elementi ignoti.</span><span class="sxs-lookup"><span data-stu-id="4a953-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="4a953-173">In ordine toouse per gli elementi meno attivi, hello `UseFeatureInModel` parametro di compilazione deve essere configurato.</span><span class="sxs-lookup"><span data-stu-id="4a953-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="4a953-174">In funzionalità toouse ordine per elementi ignoti hello `AllowColdItemPlacement` parametro di compilazione deve essere abilitata.</span><span class="sxs-lookup"><span data-stu-id="4a953-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="4a953-175">Nota: Non è possibile tooenable `AllowColdItemPlacement` senza abilitare `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="4a953-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="4a953-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-176">4.3.</span></span> <span data-ttu-id="4a953-177">Motivazione delle raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="4a953-177">Recommendation reasoning</span></span>
<span data-ttu-id="4a953-178">La motivazione delle raccomandazioni è un altro aspetto dell'utilizzo delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="4a953-179">In effetti, il motore di Azure Machine Learning indicazioni hello può utilizzare spiegazioni di raccomandazione tooprovide funzionalità (anche noto come</span><span class="sxs-lookup"><span data-stu-id="4a953-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="4a953-180">ragionamento), iniziali confidenza toomore in hello consigliabile elemento consumer raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="4a953-181">tooenable ragionamento, hello `AllowFeatureCorrelation` e `ReasoningFeatureList` parametri devono essere il programma di installazione preventiva toorequesting una compilazione di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="4a953-182">5. Modello Basic</span><span class="sxs-lookup"><span data-stu-id="4a953-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="4a953-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-183">5.1.</span></span> <span data-ttu-id="4a953-184">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="4a953-184">Create Model</span></span>
<span data-ttu-id="4a953-185">Crea una richiesta di tipo "crea modello".</span><span class="sxs-lookup"><span data-stu-id="4a953-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="4a953-186">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-186">HTTP Method</span></span> | <span data-ttu-id="4a953-187">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-188">POST</span><span class="sxs-lookup"><span data-stu-id="4a953-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-189">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-190">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-190">Parameter Name</span></span> | <span data-ttu-id="4a953-191">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-192">modelName</span><span class="sxs-lookup"><span data-stu-id="4a953-192">modelName</span></span> |<span data-ttu-id="4a953-193">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="4a953-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4a953-194">Lunghezza massima: 20</span><span class="sxs-lookup"><span data-stu-id="4a953-194">Max length: 20</span></span> |
| <span data-ttu-id="4a953-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-195">apiVersion</span></span> |<span data-ttu-id="4a953-196">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-196">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-197">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-197">Request Body</span></span> |<span data-ttu-id="4a953-198">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-198">NONE</span></span> |

<span data-ttu-id="4a953-199">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-199">**Response**:</span></span>

<span data-ttu-id="4a953-200">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="4a953-201">`feed/entry/content/properties/id`-Contiene l'ID del modello hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="4a953-202">**Nota**: l'ID modello fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4a953-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="4a953-203">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-203">OData XML</span></span>

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

### <a name="52-get-model"></a><span data-ttu-id="4a953-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-204">5.2.</span></span> <span data-ttu-id="4a953-205">Ottenere il modello</span><span class="sxs-lookup"><span data-stu-id="4a953-205">Get Model</span></span>
<span data-ttu-id="4a953-206">Crea una richiesta di tipo "ottieni modello":</span><span class="sxs-lookup"><span data-stu-id="4a953-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="4a953-207">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-207">HTTP Method</span></span> | <span data-ttu-id="4a953-208">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-209">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="4a953-210">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-211">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-211">Parameter Name</span></span> | <span data-ttu-id="4a953-212">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-213">id</span><span class="sxs-lookup"><span data-stu-id="4a953-213">id</span></span> |<span data-ttu-id="4a953-214">Identificatore univoco del modello di hello (maiuscole / minuscole)</span><span class="sxs-lookup"><span data-stu-id="4a953-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="4a953-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-215">apiVersion</span></span> |<span data-ttu-id="4a953-216">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-216">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-217">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-217">Request Body</span></span> |<span data-ttu-id="4a953-218">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-218">NONE</span></span> |

<span data-ttu-id="4a953-219">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-219">**Response**:</span></span>

<span data-ttu-id="4a953-220">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-220">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-221">dati del modello Hello sono reperibile in hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4a953-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="4a953-222">`feed/entry/content/properties/Id` : ID univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="4a953-223">`feed/entry/content/properties/Name` : nome del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="4a953-224">`feed/entry/content/properties/Date` : data di creazione del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="4a953-225">`feed/entry/content/properties/Status` : stato del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="4a953-226">Uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="4a953-226">One of hello following:</span></span>
  * <span data-ttu-id="4a953-227">Created: il modello viene creato e non contiene dati del catalogo e di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="4a953-228">ReadyForBuild: il modello viene creato e contiene dati del catalogo e di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="4a953-229">`feed/entry/content/properties/HasActiveBuild`-Indica se il modello di hello è stato compilato correttamente.</span><span class="sxs-lookup"><span data-stu-id="4a953-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="4a953-230">`feed/entry/content/properties/BuildId` : ID compilazione attiva del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="4a953-231">`feed/entry/content/properties/Mpr`: classificazione percentile media (MPR, Mean Percentile Ranking) del modello. Vedere ModelInsight per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="4a953-232">`feed/entry/content/properties/UserName`: nome utente interno del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="4a953-233">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-233">OData XML</span></span>

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

### <a name="53----get-all-models"></a><span data-ttu-id="4a953-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-234">5.3.</span></span>    <span data-ttu-id="4a953-235">Ottenere tutti i modelli</span><span class="sxs-lookup"><span data-stu-id="4a953-235">Get All Models</span></span>
<span data-ttu-id="4a953-236">Recupera tutti i modelli dell'utente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="4a953-237">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-237">HTTP Method</span></span> | <span data-ttu-id="4a953-238">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-239">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="4a953-240">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-241">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-241">Parameter Name</span></span> | <span data-ttu-id="4a953-242">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-243">apiVersion</span></span> |<span data-ttu-id="4a953-244">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-244">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-245">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-245">Request Body</span></span> |<span data-ttu-id="4a953-246">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-246">NONE</span></span> |

<span data-ttu-id="4a953-247">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-247">**Response**:</span></span>

<span data-ttu-id="4a953-248">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="4a953-249">`feed/entry/content/properties/Id` : ID univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="4a953-250">`feed/entry/content/properties/Name` : nome del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="4a953-251">`feed/entry/content/properties/Date` : data di creazione del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="4a953-252">`feed/entry/content/properties/Status` : stato del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="4a953-253">Uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="4a953-253">One of hello following:</span></span>
  * <span data-ttu-id="4a953-254">Created: il modello viene creato e non contiene dati del catalogo e di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="4a953-255">ReadyForBuild: il modello viene creato e contiene dati del catalogo e di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="4a953-256">`feed/entry/content/properties/HasActiveBuild`-Indica se il modello di hello è stato compilato correttamente.</span><span class="sxs-lookup"><span data-stu-id="4a953-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="4a953-257">`feed/entry/content/properties/BuildId` : ID compilazione attiva del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="4a953-258">`feed/entry/content/properties/Mpr`:MPR del modello. Vedere ModelInsight per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="4a953-259">`feed/entry/content/properties/UserName`: nome utente interno del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="4a953-260">`feed/entry/content/properties/UsageFileNames` : elenco dei file di dati di utilizzo del modello, separati da virgole.</span><span class="sxs-lookup"><span data-stu-id="4a953-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="4a953-261">`feed/entry/content/properties/CatalogId` : ID catalogo del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="4a953-262">`feed/entry/content/properties/Description` : descrizione del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="4a953-263">`feed/entry/content/properties/CatalogFileName` : nome del file di catalogo del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="4a953-264">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-264">OData XML</span></span>

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

### <a name="54----update-model"></a><span data-ttu-id="4a953-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="4a953-265">5.4.</span></span>    <span data-ttu-id="4a953-266">Aggiornare il modello</span><span class="sxs-lookup"><span data-stu-id="4a953-266">Update Model</span></span>
<span data-ttu-id="4a953-267">È possibile aggiornare la descrizione del modello hello o hello ID di generazione attivo.</span><span class="sxs-lookup"><span data-stu-id="4a953-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="4a953-268">
<ins>ID compilazione attiva</ins>: la compilazione per ogni modello ha un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="4a953-269">ID compilazione attiva Hello è hello prima corretta compilazione di ogni nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="4a953-270">Quando si ha un ID compilazione attiva e si compilazioni aggiuntive per hello stesso modello, è necessario tooexplicitly impostarlo come hello predefinito ID compilazione se si desidera.</span><span class="sxs-lookup"><span data-stu-id="4a953-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="4a953-271">Quando si utilizzano indicazioni, se non si specifica l'ID compilazione hello che si desidera toouse, predefinito hello uno verrà utilizzato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4a953-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="4a953-272">Questo meccanismo consente - dopo aver un modello di raccomandazione nella produzione - toobuild nuovi modelli e testarli prima si innalza di livello li tooproduction.</span><span class="sxs-lookup"><span data-stu-id="4a953-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="4a953-273">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-273">HTTP Method</span></span> | <span data-ttu-id="4a953-274">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-275">PUT</span><span class="sxs-lookup"><span data-stu-id="4a953-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="4a953-276">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-277">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-277">Parameter Name</span></span> | <span data-ttu-id="4a953-278">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-279">id</span><span class="sxs-lookup"><span data-stu-id="4a953-279">id</span></span> |<span data-ttu-id="4a953-280">Identificatore univoco del modello di hello (maiuscole / minuscole)</span><span class="sxs-lookup"><span data-stu-id="4a953-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="4a953-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-281">apiVersion</span></span> |<span data-ttu-id="4a953-282">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-282">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-283">Request Body</span><span class="sxs-lookup"><span data-stu-id="4a953-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="4a953-284">Si noti che hello XML tag descrizione ActiveBuildId sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="4a953-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="4a953-285">Se non si desidera tooset descrizione o ActiveBuildId, rimuovere i tag intero hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="4a953-286">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-286">**Response**:</span></span>

<span data-ttu-id="4a953-287">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="4a953-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="4a953-288">5.5.</span></span>    <span data-ttu-id="4a953-289">Eliminare il modello</span><span class="sxs-lookup"><span data-stu-id="4a953-289">Delete Model</span></span>
<span data-ttu-id="4a953-290">Elimina un modello esistente in base all'ID.</span><span class="sxs-lookup"><span data-stu-id="4a953-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="4a953-291">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-291">HTTP Method</span></span> | <span data-ttu-id="4a953-292">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-293">DELETE</span><span class="sxs-lookup"><span data-stu-id="4a953-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="4a953-294">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-295">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-295">Parameter Name</span></span> | <span data-ttu-id="4a953-296">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-297">id</span><span class="sxs-lookup"><span data-stu-id="4a953-297">id</span></span> |<span data-ttu-id="4a953-298">Identificatore univoco del modello di hello (maiuscole / minuscole)</span><span class="sxs-lookup"><span data-stu-id="4a953-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="4a953-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-299">apiVersion</span></span> |<span data-ttu-id="4a953-300">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-300">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-301">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-301">Request Body</span></span> |<span data-ttu-id="4a953-302">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-302">NONE</span></span> |

<span data-ttu-id="4a953-303">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-303">**Response**:</span></span>

<span data-ttu-id="4a953-304">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-304">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-305">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-305">OData XML</span></span>

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

## <a name="6-model-advanced"></a><span data-ttu-id="4a953-306">6. Modello Advanced</span><span class="sxs-lookup"><span data-stu-id="4a953-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="4a953-307">6.1</span><span class="sxs-lookup"><span data-stu-id="4a953-307">6.1.</span></span>    <span data-ttu-id="4a953-308">Modello Data Insight</span><span class="sxs-lookup"><span data-stu-id="4a953-308">Model Data Insight</span></span>
<span data-ttu-id="4a953-309">Restituisce dati statistici sui dati di utilizzo hello generato con questo modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="4a953-310">Disponibile solo per la compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="4a953-311">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-311">HTTP Method</span></span> | <span data-ttu-id="4a953-312">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-313">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="4a953-314">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-315">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-315">Parameter Name</span></span> | <span data-ttu-id="4a953-316">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-317">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-317">modelId</span></span> |<span data-ttu-id="4a953-318">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-319">apiVersion</span></span> |<span data-ttu-id="4a953-320">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-320">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-321">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-321">Request Body</span></span> |<span data-ttu-id="4a953-322">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-322">NONE</span></span> |

<span data-ttu-id="4a953-323">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-323">**Response**:</span></span>

<span data-ttu-id="4a953-324">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-324">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-325">dati Hello viene restituiti come una raccolta di proprietà.</span><span class="sxs-lookup"><span data-stu-id="4a953-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="4a953-326">`feed/entry/id/content/properties/key`-Contiene il nome di proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="4a953-327">`feed/entry/id/content/properties/value`-Contiene il valore di proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="4a953-328">tabella Hello riportata di seguito viene illustrata valore hello che rappresenta ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="4a953-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="4a953-329">Chiave</span><span class="sxs-lookup"><span data-stu-id="4a953-329">Key</span></span> | <span data-ttu-id="4a953-330">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="4a953-331">AvgItemLength</span></span> |<span data-ttu-id="4a953-332">Numero medio di utenti distinti per elemento.</span><span class="sxs-lookup"><span data-stu-id="4a953-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="4a953-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="4a953-333">AvgUserLength</span></span> |<span data-ttu-id="4a953-334">Numero medio di elementi distinti per utente.</span><span class="sxs-lookup"><span data-stu-id="4a953-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="4a953-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="4a953-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="4a953-336">Numero di elementi dopo l'eliminazione degli elementi che non possono essere modellati.</span><span class="sxs-lookup"><span data-stu-id="4a953-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="4a953-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="4a953-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="4a953-338">Numero di punti di utilizzo dopo l'eliminazione degli utenti e degli elementi che non possono essere modellati.</span><span class="sxs-lookup"><span data-stu-id="4a953-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="4a953-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="4a953-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="4a953-340">Numero di punti di utilizzo dopo l'eliminazione degli utenti e degli elementi che non possono essere modellati.</span><span class="sxs-lookup"><span data-stu-id="4a953-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="4a953-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="4a953-341">MaxItemLength</span></span> |<span data-ttu-id="4a953-342">Numero di utenti distinti per l'elemento più diffuso hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="4a953-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="4a953-343">MaxUserLength</span></span> |<span data-ttu-id="4a953-344">Numero massimo di elementi distinti per un utente.</span><span class="sxs-lookup"><span data-stu-id="4a953-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="4a953-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="4a953-345">MinItemLength</span></span> |<span data-ttu-id="4a953-346">Numero massimo di utenti distinti per un elemento.</span><span class="sxs-lookup"><span data-stu-id="4a953-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="4a953-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="4a953-347">MinUserLength</span></span> |<span data-ttu-id="4a953-348">Numero minimo di elementi distinti per un utente.</span><span class="sxs-lookup"><span data-stu-id="4a953-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="4a953-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="4a953-349">RawNumberOfItems</span></span> |<span data-ttu-id="4a953-350">Numero di elementi nel file hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="4a953-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="4a953-351">RawNumberOfUsers</span></span> |<span data-ttu-id="4a953-352">Numero di punti di utilizzo prima di qualsiasi eliminazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="4a953-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="4a953-353">RawNumberOfRecords</span></span> |<span data-ttu-id="4a953-354">Numero di punti di utilizzo prima di qualsiasi eliminazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="4a953-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="4a953-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="4a953-356">N/D</span><span class="sxs-lookup"><span data-stu-id="4a953-356">N/A</span></span> |
| <span data-ttu-id="4a953-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="4a953-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="4a953-358">N/D</span><span class="sxs-lookup"><span data-stu-id="4a953-358">N/A</span></span> |
| <span data-ttu-id="4a953-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="4a953-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="4a953-360">N/D</span><span class="sxs-lookup"><span data-stu-id="4a953-360">N/A</span></span> |

<span data-ttu-id="4a953-361">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-361">OData XML</span></span>

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

### <a name="62----model-insight"></a><span data-ttu-id="4a953-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-362">6.2.</span></span>    <span data-ttu-id="4a953-363">Modello Insight</span><span class="sxs-lookup"><span data-stu-id="4a953-363">Model Insight</span></span>
<span data-ttu-id="4a953-364">Restituisce informazioni dettagliate del modello in fase di compilazione active hello o (se disponibile) in una compilazione specifica.</span><span class="sxs-lookup"><span data-stu-id="4a953-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="4a953-365">Disponibile solo per la compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="4a953-366">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-366">HTTP Method</span></span> | <span data-ttu-id="4a953-367">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-368">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-368">GET</span></span> |<span data-ttu-id="4a953-369">Con l'ID compilazione attiva:</span><span class="sxs-lookup"><span data-stu-id="4a953-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-370">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-371">Con ID compilazione specifica:</span><span class="sxs-lookup"><span data-stu-id="4a953-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-372">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-372">Parameter Name</span></span> | <span data-ttu-id="4a953-373">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-374">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-374">modelId</span></span> |<span data-ttu-id="4a953-375">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-376">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-376">buildId</span></span> |<span data-ttu-id="4a953-377">Facoltativo: numero che identifica una compilazione completata.</span><span class="sxs-lookup"><span data-stu-id="4a953-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="4a953-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-378">apiVersion</span></span> |<span data-ttu-id="4a953-379">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-379">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-380">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-380">Request Body</span></span> |<span data-ttu-id="4a953-381">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-381">NONE</span></span> |

<span data-ttu-id="4a953-382">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-382">**Response**:</span></span>

<span data-ttu-id="4a953-383">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-383">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-384">dati Hello viene restituiti come una raccolta di proprietà.</span><span class="sxs-lookup"><span data-stu-id="4a953-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="4a953-385">tabella Hello riportata di seguito viene illustrata valore hello che rappresenta ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="4a953-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="4a953-386">Chiave</span><span class="sxs-lookup"><span data-stu-id="4a953-386">Key</span></span> | <span data-ttu-id="4a953-387">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="4a953-388">CatalogCoverage</span></span> |<span data-ttu-id="4a953-389">La parte del catalogo hello può essere modellata con i modelli di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="4a953-390">altri Hello hello elementi saranno necessario funzionalità basata sul contenuto.</span><span class="sxs-lookup"><span data-stu-id="4a953-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="4a953-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="4a953-391">Mpr</span></span> |<span data-ttu-id="4a953-392">: Classificazione percentile del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="4a953-393">È preferibile un valore basso.</span><span class="sxs-lookup"><span data-stu-id="4a953-393">Lower is better.</span></span> |
| <span data-ttu-id="4a953-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="4a953-394">NumberOfDimensions</span></span> |<span data-ttu-id="4a953-395">Numero di dimensioni utilizzati dall'algoritmo di GPO hello matrice.</span><span class="sxs-lookup"><span data-stu-id="4a953-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="4a953-396">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-396">OData XML</span></span>

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

### <a name="63----get-model-sample"></a><span data-ttu-id="4a953-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-397">6.3.</span></span>    <span data-ttu-id="4a953-398">Ottenere un esempio del modello</span><span class="sxs-lookup"><span data-stu-id="4a953-398">Get Model Sample</span></span>
<span data-ttu-id="4a953-399">Ottiene un campione di modello di raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="4a953-400">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-400">HTTP Method</span></span> | <span data-ttu-id="4a953-401">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-402">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="4a953-403">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-404">Con ID compilazione specifica:</span><span class="sxs-lookup"><span data-stu-id="4a953-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="4a953-405">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-406">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-406">Parameter Name</span></span> | <span data-ttu-id="4a953-407">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-408">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-408">modelId</span></span> |<span data-ttu-id="4a953-409">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-410">apiVersion</span></span> |<span data-ttu-id="4a953-411">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-411">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-412">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-412">Request Body</span></span> |<span data-ttu-id="4a953-413">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-413">NONE</span></span> |

<span data-ttu-id="4a953-414">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-414">**Response**:</span></span>

<span data-ttu-id="4a953-415">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-415">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-416">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-416">OData XML</span></span>

<span data-ttu-id="4a953-417">La risposta viene restituita in un formato di testo non elaborato:</span><span class="sxs-lookup"><span data-stu-id="4a953-417">Response is returned in raw text format:</span></span>

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
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="4a953-418">7. Modello Business Rules</span><span class="sxs-lookup"><span data-stu-id="4a953-418">7. Model Business Rules</span></span>
<span data-ttu-id="4a953-419">Questi sono tipi di hello di regole supportate:</span><span class="sxs-lookup"><span data-stu-id="4a953-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="4a953-420"><strong>Blocco indirizzi</strong> -blocco indirizzi consentono tooprovide un elenco di elementi che non si desidera tooreturn nei risultati della raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="4a953-421"><strong>FeatureBlockList</strong> -blocco indirizzi funzionalità Abilita si tooblock gli elementi in base ai valori hello le sue funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="4a953-422">*Non inviare più di 1000 elementi in una singola regola blocklist o si rischia il timeout della chiamata. Se è necessario tooblock più di 1000 elementi, è possibile eseguire più chiamate di blocco indirizzi.*</span><span class="sxs-lookup"><span data-stu-id="4a953-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="4a953-423"><strong>Upsale</strong> -Upsale consente tooenforce tooreturn di elementi nei risultati della raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="4a953-424"><strong>WhiteList</strong> -Abilita elenco approvato è tooonly suggerire raccomandazioni a partire da un elenco di elementi.</span><span class="sxs-lookup"><span data-stu-id="4a953-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="4a953-425"><strong>FeatureWhiteList</strong> -elenco di funzionalità vuoto consente tooonly consigliabile elementi con i valori delle funzionalità specifiche.</span><span class="sxs-lookup"><span data-stu-id="4a953-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="4a953-426"><strong>PerSeedBlockList</strong> - Per consente di valore di inizializzazione dell'elenco di blocchi tooprovide per ogni elemento di un elenco di elementi che non può essere restituito come risultato di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="4a953-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-427">7.1.</span></span>    <span data-ttu-id="4a953-428">Ottenere le regole del modello</span><span class="sxs-lookup"><span data-stu-id="4a953-428">Get Model Rules</span></span>
| <span data-ttu-id="4a953-429">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-429">HTTP Method</span></span> | <span data-ttu-id="4a953-430">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-431">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="4a953-432">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-433">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-433">Parameter Name</span></span> | <span data-ttu-id="4a953-434">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-435">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-435">modelId</span></span> |<span data-ttu-id="4a953-436">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-437">apiVersion</span></span> |<span data-ttu-id="4a953-438">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-438">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-439">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-439">Request Body</span></span> |<span data-ttu-id="4a953-440">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-440">NONE</span></span> |

<span data-ttu-id="4a953-441">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-441">**Response**:</span></span>

<span data-ttu-id="4a953-442">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="4a953-443">`feed/entry/content/properties/Id` : identificatore univoco della regola.</span><span class="sxs-lookup"><span data-stu-id="4a953-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="4a953-444">`feed/entry/content/properties/Type`-Tipo di regola hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="4a953-445">`feed/entry/content/properties/Parameter` : parametro della regola.</span><span class="sxs-lookup"><span data-stu-id="4a953-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="4a953-446">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-446">OData XML</span></span>

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

### <a name="72----add-rule"></a><span data-ttu-id="4a953-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-447">7.2.</span></span>    <span data-ttu-id="4a953-448">Aggiungere una regola</span><span class="sxs-lookup"><span data-stu-id="4a953-448">Add Rule</span></span>
| <span data-ttu-id="4a953-449">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-449">HTTP Method</span></span> | <span data-ttu-id="4a953-450">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-451">POST</span><span class="sxs-lookup"><span data-stu-id="4a953-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="4a953-452">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="4a953-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="4a953-453">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-453">Parameter Name</span></span> | <span data-ttu-id="4a953-454">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-455">apiVersion</span></span> |<span data-ttu-id="4a953-456">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-456">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-457">Request Body</span><span class="sxs-lookup"><span data-stu-id="4a953-457">Request Body</span></span> | |

<span data-ttu-id="4a953-458"><ins>Ogni volta che specifica gli ID elemento per le regole di business, assicurarsi che toouse hello Id esterno dell'elemento hello (lo stesso Id utilizzato nel file di catalogo hello hello)</ins></span><span class="sxs-lookup"><span data-stu-id="4a953-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="4a953-459">
<ins>tooadd una regola dell'elenco indirizzi bloccati:</ins></span><span class="sxs-lookup"><span data-stu-id="4a953-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="4a953-460"><ins>
<ins>una regola FeatureBlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="4a953-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="4a953-461"><ins>una regola Upsale tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="4a953-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="4a953-462">
<ins>tooadd una regola WhiteList:</ins></span><span class="sxs-lookup"><span data-stu-id="4a953-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="4a953-463"><ins>
<ins>una regola FeatureWhiteList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="4a953-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="4a953-464"><ins>una regola PerSeedBlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="4a953-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="4a953-465">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-465">**Response**:</span></span>

<span data-ttu-id="4a953-466">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-466">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-467">Hello API restituisce hello appena creato regola con i dettagli.</span><span class="sxs-lookup"><span data-stu-id="4a953-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="4a953-468">proprietà rules Hello può essere recuperato da hello seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="4a953-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="4a953-469">`feed/entry/content/properties/Id` : identificatore univoco della regola.</span><span class="sxs-lookup"><span data-stu-id="4a953-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="4a953-470">`feed/entry/content/properties/Type`-Tipo di regola hello: blocco indirizzi o Upsale.</span><span class="sxs-lookup"><span data-stu-id="4a953-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="4a953-471">`feed/entry/content/properties/Parameter` : parametro della regola.</span><span class="sxs-lookup"><span data-stu-id="4a953-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="4a953-472">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-472">OData XML</span></span>

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

### <a name="73----delete-rule"></a><span data-ttu-id="4a953-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-473">7.3.</span></span>    <span data-ttu-id="4a953-474">Eliminare una regola</span><span class="sxs-lookup"><span data-stu-id="4a953-474">Delete Rule</span></span>
| <span data-ttu-id="4a953-475">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-475">HTTP Method</span></span> | <span data-ttu-id="4a953-476">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-477">DELETE</span><span class="sxs-lookup"><span data-stu-id="4a953-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-478">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-479">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-479">Parameter Name</span></span> | <span data-ttu-id="4a953-480">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-481">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-481">modelId</span></span> |<span data-ttu-id="4a953-482">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-483">filterId</span><span class="sxs-lookup"><span data-stu-id="4a953-483">filterId</span></span> |<span data-ttu-id="4a953-484">Identificatore univoco del filtro hello</span><span class="sxs-lookup"><span data-stu-id="4a953-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="4a953-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-485">apiVersion</span></span> |<span data-ttu-id="4a953-486">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-486">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-487">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-487">Request Body</span></span> |<span data-ttu-id="4a953-488">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-488">NONE</span></span> |

<span data-ttu-id="4a953-489">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-489">**Response**:</span></span>

<span data-ttu-id="4a953-490">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="4a953-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="4a953-491">7.4.</span></span>    <span data-ttu-id="4a953-492">Eliminare tutte le regole</span><span class="sxs-lookup"><span data-stu-id="4a953-492">Delete All Rules</span></span>
| <span data-ttu-id="4a953-493">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-493">HTTP Method</span></span> | <span data-ttu-id="4a953-494">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-495">DELETE</span><span class="sxs-lookup"><span data-stu-id="4a953-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-496">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-497">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-497">Parameter Name</span></span> | <span data-ttu-id="4a953-498">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-499">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-499">modelId</span></span> |<span data-ttu-id="4a953-500">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-501">apiVersion</span></span> |<span data-ttu-id="4a953-502">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-502">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-503">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-503">Request Body</span></span> |<span data-ttu-id="4a953-504">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-504">NONE</span></span> |

<span data-ttu-id="4a953-505">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-505">**Response**:</span></span>

<span data-ttu-id="4a953-506">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="4a953-507">8. Catalogo</span><span class="sxs-lookup"><span data-stu-id="4a953-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="4a953-508">8.1</span><span class="sxs-lookup"><span data-stu-id="4a953-508">8.1.</span></span>    <span data-ttu-id="4a953-509">Importare i dati del catalogo</span><span class="sxs-lookup"><span data-stu-id="4a953-509">Import Catalog Data</span></span>
<span data-ttu-id="4a953-510">Se si carica più catalogo file toohello stesso modello con più chiamate, si verranno inserire hello solo nuovi elementi di catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="4a953-511">Gli elementi esistenti verranno mantenuti con i valori originali di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="4a953-512">Non è possibile aggiornare i dati del catalogo con questo metodo.</span><span class="sxs-lookup"><span data-stu-id="4a953-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="4a953-513">dati del catalogo Hello devono seguire hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="4a953-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="4a953-514">Senza funzionalità: `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="4a953-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="4a953-515">Con funzionalità: `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="4a953-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="4a953-516">Nota: dimensioni massime del file hello sono pari a 200MB.</span><span class="sxs-lookup"><span data-stu-id="4a953-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="4a953-517">** Dettagli relativi al formato **</span><span class="sxs-lookup"><span data-stu-id="4a953-517">** Format details **</span></span>

| <span data-ttu-id="4a953-518">Nome</span><span class="sxs-lookup"><span data-stu-id="4a953-518">Name</span></span> | <span data-ttu-id="4a953-519">Mandatory</span><span class="sxs-lookup"><span data-stu-id="4a953-519">Mandatory</span></span> | <span data-ttu-id="4a953-520">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a953-520">Type</span></span> | <span data-ttu-id="4a953-521">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4a953-522">Item Id</span><span class="sxs-lookup"><span data-stu-id="4a953-522">Item Id</span></span> |<span data-ttu-id="4a953-523">Sì</span><span class="sxs-lookup"><span data-stu-id="4a953-523">Yes</span></span> |<span data-ttu-id="4a953-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="4a953-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="4a953-525">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4a953-525">Max length: 50</span></span> |<span data-ttu-id="4a953-526">Identificatore univoco di un elemento.</span><span class="sxs-lookup"><span data-stu-id="4a953-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="4a953-527">Item Name</span><span class="sxs-lookup"><span data-stu-id="4a953-527">Item Name</span></span> |<span data-ttu-id="4a953-528">Sì</span><span class="sxs-lookup"><span data-stu-id="4a953-528">Yes</span></span> |<span data-ttu-id="4a953-529">Qualsiasi carattere alfanumerico</span><span class="sxs-lookup"><span data-stu-id="4a953-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="4a953-530">Lunghezza massima: 255</span><span class="sxs-lookup"><span data-stu-id="4a953-530">Max length: 255</span></span> |<span data-ttu-id="4a953-531">Nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="4a953-531">Item name.</span></span> |
| <span data-ttu-id="4a953-532">Item Category</span><span class="sxs-lookup"><span data-stu-id="4a953-532">Item Category</span></span> |<span data-ttu-id="4a953-533">Sì</span><span class="sxs-lookup"><span data-stu-id="4a953-533">Yes</span></span> |<span data-ttu-id="4a953-534">Qualsiasi carattere alfanumerico</span><span class="sxs-lookup"><span data-stu-id="4a953-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="4a953-535">Lunghezza massima: 255</span><span class="sxs-lookup"><span data-stu-id="4a953-535">Max length: 255</span></span> |<span data-ttu-id="4a953-536">Categoria toowhich questo elemento appartiene (ad esempio cucina documentazione, serie...). può essere vuoto.</span><span class="sxs-lookup"><span data-stu-id="4a953-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="4a953-537">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a953-537">Description</span></span> |<span data-ttu-id="4a953-538">No, a meno che siano presenti funzionalità (può essere vuoto)</span><span class="sxs-lookup"><span data-stu-id="4a953-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="4a953-539">Qualsiasi carattere alfanumerico</span><span class="sxs-lookup"><span data-stu-id="4a953-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="4a953-540">Lunghezza massima: 4000</span><span class="sxs-lookup"><span data-stu-id="4a953-540">Max length: 4000</span></span> |<span data-ttu-id="4a953-541">Descrizione dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="4a953-541">Description of this item.</span></span> |
| <span data-ttu-id="4a953-542">Elenco di funzionalità</span><span class="sxs-lookup"><span data-stu-id="4a953-542">Features list</span></span> |<span data-ttu-id="4a953-543">No</span><span class="sxs-lookup"><span data-stu-id="4a953-543">No</span></span> |<span data-ttu-id="4a953-544">Qualsiasi carattere alfanumerico</span><span class="sxs-lookup"><span data-stu-id="4a953-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="4a953-545">Lunghezza massima: 4000, numero massimo di funzionalità: 20</span><span class="sxs-lookup"><span data-stu-id="4a953-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="4a953-546">Elenco delimitato da virgole di nome della funzionalità = valore di funzionalità che può essere utilizzati tooenhance modello raccomandazione; vedere [argomenti avanzati](#2-advanced-topics) sezione.</span><span class="sxs-lookup"><span data-stu-id="4a953-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="4a953-547">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-547">HTTP Method</span></span> | <span data-ttu-id="4a953-548">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-549">POST</span><span class="sxs-lookup"><span data-stu-id="4a953-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-550">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="4a953-551">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="4a953-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="4a953-552">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-552">Parameter Name</span></span> | <span data-ttu-id="4a953-553">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-554">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-554">modelId</span></span> |<span data-ttu-id="4a953-555">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-556">filename</span><span class="sxs-lookup"><span data-stu-id="4a953-556">filename</span></span> |<span data-ttu-id="4a953-557">Identificatore testuale del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="4a953-558">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="4a953-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4a953-559">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4a953-559">Max length: 50</span></span> |
| <span data-ttu-id="4a953-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-560">apiVersion</span></span> |<span data-ttu-id="4a953-561">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-561">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-562">Request Body</span><span class="sxs-lookup"><span data-stu-id="4a953-562">Request Body</span></span> |<span data-ttu-id="4a953-563">Esempio (con funzionalità):</span><span class="sxs-lookup"><span data-stu-id="4a953-563">Example (with features):</span></span><br/><span data-ttu-id="4a953-564">2406e770-c 769-4189-89de-1c9283f93a96, Clara Callan libro, descrizione libro hello, autore = Richard Wright, publisher = Harper Flamingo Canada, anno 2001 =</span><span class="sxs-lookup"><span data-stu-id="4a953-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="4a953-565">21bf8088-b6c0-4509-870c-e1c7ac78304a, hello chat Forgetting: A fittizio (Byzantium Book), libro, autore = Nick Bantock, publisher = Harpercollins, anno = 1997</span><span class="sxs-lookup"><span data-stu-id="4a953-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="4a953-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="4a953-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="4a953-567">552a1940-21e4-4399-82bb-594b46d7ed54, ritenuta di Belve, libro, descrizione libro hello, autore = Magnus Mills, publisher = Publishing per computer, anno 1998 =</span><span class="sxs-lookup"><span data-stu-id="4a953-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="4a953-568">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-568">**Response**:</span></span>

<span data-ttu-id="4a953-569">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-569">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-570">Hello API restituisce un report dell'importazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="4a953-571">`feed\entry\content\properties\LineCount` : numero di righe accettate.</span><span class="sxs-lookup"><span data-stu-id="4a953-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="4a953-572">`feed\entry\content\properties\ErrorCount`-Numero di righe che non sono state inserite a causa di errore tooan.</span><span class="sxs-lookup"><span data-stu-id="4a953-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="4a953-573">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-573">OData XML</span></span>

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

### <a name="82----get-catalog"></a><span data-ttu-id="4a953-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-574">8.2.</span></span>    <span data-ttu-id="4a953-575">Ottenere il catalogo</span><span class="sxs-lookup"><span data-stu-id="4a953-575">Get Catalog</span></span>
<span data-ttu-id="4a953-576">Recupera tutti gli elementi del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="4a953-577">catalogo Hello sarà recuperato una pagina alla volta.</span><span class="sxs-lookup"><span data-stu-id="4a953-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="4a953-578">Se si desidera tooget elementi da un indice specifico, è possibile utilizzare il parametro di odata hello $skip.</span><span class="sxs-lookup"><span data-stu-id="4a953-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="4a953-579">Ad esempio se si desidera tooget elementi a partire dalla posizione 100, aggiungere il parametro hello $skip = 100 toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="4a953-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="4a953-580">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-580">HTTP Method</span></span> | <span data-ttu-id="4a953-581">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-582">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-583">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-584">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-584">Parameter Name</span></span> | <span data-ttu-id="4a953-585">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-586">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-586">modelId</span></span> |<span data-ttu-id="4a953-587">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-588">apiVersion</span></span> |<span data-ttu-id="4a953-589">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-589">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-590">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-590">Request Body</span></span> |<span data-ttu-id="4a953-591">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-591">NONE</span></span> |

<span data-ttu-id="4a953-592">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-592">**Response**:</span></span>

<span data-ttu-id="4a953-593">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-593">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-594">risposta Hello include una voce per ogni elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="4a953-595">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-596">`feed/entry/content/properties/ExternalId`-ID esterno elemento del catalogo, hello quella fornita dal cliente hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="4a953-597">`feed/entry/content/properties/InternalId`-Catalogo elemento ID interno hello Azure Machine Learning indicazioni ha generato.</span><span class="sxs-lookup"><span data-stu-id="4a953-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="4a953-598">`feed/entry/content/properties/Name` : nome dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="4a953-599">`feed/entry/content/properties/Category` : categoria dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="4a953-600">`feed/entry/content/properties/Description` : descrizione dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="4a953-601">`feed/entry/content/properties/Metadata` : metadati dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="4a953-602">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-602">OData XML</span></span>

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
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="4a953-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-603">8.3.</span></span>    <span data-ttu-id="4a953-604">Ottenere gli elementi del catalogo in base al token</span><span class="sxs-lookup"><span data-stu-id="4a953-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="4a953-605">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-605">HTTP Method</span></span> | <span data-ttu-id="4a953-606">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-607">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-608">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-609">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-609">Parameter Name</span></span> | <span data-ttu-id="4a953-610">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-611">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-611">modelId</span></span> |<span data-ttu-id="4a953-612">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-613">token</span><span class="sxs-lookup"><span data-stu-id="4a953-613">token</span></span> |<span data-ttu-id="4a953-614">Token del nome dell'elemento del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="4a953-615">Deve contenere almeno tre caratteri.</span><span class="sxs-lookup"><span data-stu-id="4a953-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="4a953-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-616">apiVersion</span></span> |<span data-ttu-id="4a953-617">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-617">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-618">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-618">Request Body</span></span> |<span data-ttu-id="4a953-619">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-619">NONE</span></span> |

<span data-ttu-id="4a953-620">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-620">**Response**:</span></span>

<span data-ttu-id="4a953-621">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-621">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-622">risposta Hello include una voce per ogni elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="4a953-623">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-624">`feed/entry/content/properties/InternalId`-Catalogo elemento ID interno hello Azure Machine Learning indicazioni ha generato.</span><span class="sxs-lookup"><span data-stu-id="4a953-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="4a953-625">`feed/entry/content/properties/Name` : nome dell'elemento del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4a953-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="4a953-626">`feed/entry/content/properties/Rating` : per uso futuro</span><span class="sxs-lookup"><span data-stu-id="4a953-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="4a953-627">`feed/entry/content/properties/Reasoning` : per uso futuro</span><span class="sxs-lookup"><span data-stu-id="4a953-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="4a953-628">`feed/entry/content/properties/Metadata` : per uso futuro</span><span class="sxs-lookup"><span data-stu-id="4a953-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="4a953-629">`feed/entry/content/properties/FormattedRating` : per uso futuro</span><span class="sxs-lookup"><span data-stu-id="4a953-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="4a953-630">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-630">OData XML</span></span>

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

## <a name="9-usage-data"></a><span data-ttu-id="4a953-631">9. Dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="4a953-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="4a953-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-632">9.1.</span></span>    <span data-ttu-id="4a953-633">Importare i dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="4a953-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="4a953-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-634">9.1.1.</span></span> <span data-ttu-id="4a953-635">Caricamento del file</span><span class="sxs-lookup"><span data-stu-id="4a953-635">Uploading File</span></span>
<span data-ttu-id="4a953-636">Questa sezione viene illustrato come dati di utilizzo tooupload utilizzando un file.</span><span class="sxs-lookup"><span data-stu-id="4a953-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="4a953-637">È possibile chiamare l'API più volte con i dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="4a953-638">Tutti i dati di utilizzo verranno salvati per tutte le chiamate.</span><span class="sxs-lookup"><span data-stu-id="4a953-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="4a953-639">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-639">HTTP Method</span></span> | <span data-ttu-id="4a953-640">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-641">POST</span><span class="sxs-lookup"><span data-stu-id="4a953-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-642">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-643">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-643">Parameter Name</span></span> | <span data-ttu-id="4a953-644">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-645">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-645">modelId</span></span> |<span data-ttu-id="4a953-646">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-647">filename</span><span class="sxs-lookup"><span data-stu-id="4a953-647">filename</span></span> |<span data-ttu-id="4a953-648">Identificatore testuale del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="4a953-649">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="4a953-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4a953-650">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4a953-650">Max length: 50</span></span> |
| <span data-ttu-id="4a953-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-651">apiVersion</span></span> |<span data-ttu-id="4a953-652">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-652">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-653">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-653">Request Body</span></span> |<span data-ttu-id="4a953-654">Dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-654">Usage data.</span></span> <span data-ttu-id="4a953-655">Formato:</span><span class="sxs-lookup"><span data-stu-id="4a953-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="4a953-656">Nome</span><span class="sxs-lookup"><span data-stu-id="4a953-656">Name</span></span></th><th><span data-ttu-id="4a953-657">Mandatory</span><span class="sxs-lookup"><span data-stu-id="4a953-657">Mandatory</span></span></th><th><span data-ttu-id="4a953-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a953-658">Type</span></span></th><th><span data-ttu-id="4a953-659">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a953-659">Description</span></span></th></tr><tr><td><span data-ttu-id="4a953-660">User Id</span><span class="sxs-lookup"><span data-stu-id="4a953-660">User Id</span></span></td><td><span data-ttu-id="4a953-661">Sì</span><span class="sxs-lookup"><span data-stu-id="4a953-661">Yes</span></span></td><td><span data-ttu-id="4a953-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="4a953-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="4a953-663">Lunghezza massima: 255</span><span class="sxs-lookup"><span data-stu-id="4a953-663">Max length: 255</span></span> </td><td><span data-ttu-id="4a953-664">Identificatore univoco di un utente.</span><span class="sxs-lookup"><span data-stu-id="4a953-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="4a953-665">Item Id</span><span class="sxs-lookup"><span data-stu-id="4a953-665">Item Id</span></span></td><td><span data-ttu-id="4a953-666">Sì</span><span class="sxs-lookup"><span data-stu-id="4a953-666">Yes</span></span></td><td><span data-ttu-id="4a953-667">[A-z], [a-z], [0-9], [&#95;] &#40;carattere di sottolineatura&#41;, [-] &#40;trattino&#41;</span><span class="sxs-lookup"><span data-stu-id="4a953-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="4a953-668">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4a953-668">Max length: 50</span></span></td><td><span data-ttu-id="4a953-669">Identificatore univoco di un elemento.</span><span class="sxs-lookup"><span data-stu-id="4a953-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="4a953-670">Time</span><span class="sxs-lookup"><span data-stu-id="4a953-670">Time</span></span></td><td><span data-ttu-id="4a953-671">No</span><span class="sxs-lookup"><span data-stu-id="4a953-671">No</span></span></td><td><span data-ttu-id="4a953-672">Data in formato: AAAA/MM/GGTHH:MM:SS (ad esempio 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="4a953-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="4a953-673">Ora dei dati.</span><span class="sxs-lookup"><span data-stu-id="4a953-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="4a953-674">Evento</span><span class="sxs-lookup"><span data-stu-id="4a953-674">Event</span></span></td><td><span data-ttu-id="4a953-675">No. Se viene specificato, deve essere inserita anche la data</span><span class="sxs-lookup"><span data-stu-id="4a953-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="4a953-676">Uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="4a953-676">One of hello following:</span></span><br><span data-ttu-id="4a953-677">• Click</span><span class="sxs-lookup"><span data-stu-id="4a953-677">• Click</span></span><br><span data-ttu-id="4a953-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="4a953-678">• RecommendationClick</span></span><br><span data-ttu-id="4a953-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="4a953-679">•    AddShopCart</span></span><br><span data-ttu-id="4a953-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="4a953-680">• RemoveShopCart</span></span><br><span data-ttu-id="4a953-681">• Acquisto</span><span class="sxs-lookup"><span data-stu-id="4a953-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="4a953-682">Dimensione massima file: 200 MB</span><span class="sxs-lookup"><span data-stu-id="4a953-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="4a953-683">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="4a953-684">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-684">**Response**:</span></span>

<span data-ttu-id="4a953-685">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="4a953-686">`Feed\entry\content\properties\LineCount` : numero di righe accettate.</span><span class="sxs-lookup"><span data-stu-id="4a953-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="4a953-687">`Feed\entry\content\properties\ErrorCount`-Numero di righe che non sono state inserite a causa di errore tooan.</span><span class="sxs-lookup"><span data-stu-id="4a953-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="4a953-688">`Feed\entry\content\properties\FileId` : identificatore del file.</span><span class="sxs-lookup"><span data-stu-id="4a953-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="4a953-689">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-689">OData XML</span></span>

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


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="4a953-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-690">9.1.2.</span></span> <span data-ttu-id="4a953-691">Uso dell'acquisizione dei dati</span><span class="sxs-lookup"><span data-stu-id="4a953-691">Using Data Acquisition</span></span>
<span data-ttu-id="4a953-692">In questa sezione viene illustrato come gli eventi toosend reale ora tooAzure Machine Learning indicazioni, in genere il sito Web.</span><span class="sxs-lookup"><span data-stu-id="4a953-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="4a953-693">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-693">HTTP Method</span></span> | <span data-ttu-id="4a953-694">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-695">POST</span><span class="sxs-lookup"><span data-stu-id="4a953-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="4a953-696">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="4a953-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="4a953-697">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-697">Parameter Name</span></span> | <span data-ttu-id="4a953-698">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-699">apiVersion</span></span> |<span data-ttu-id="4a953-700">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-700">1.0</span></span> |
| <span data-ttu-id="4a953-701">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-701">Request body</span></span> |<span data-ttu-id="4a953-702">Immissione di dati di evento per ogni evento desiderato toosend.</span><span class="sxs-lookup"><span data-stu-id="4a953-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="4a953-703">È necessario inviare per stessa sessione utente o un browser hello hello stesso ID nel campo SessionId hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="4a953-704">Vedere l'esempio di corpo dell'evento di seguito.</span><span class="sxs-lookup"><span data-stu-id="4a953-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="4a953-705">Esempio di evento "Click":</span><span class="sxs-lookup"><span data-stu-id="4a953-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="4a953-706">Esempio di evento "RecommendationClick":</span><span class="sxs-lookup"><span data-stu-id="4a953-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="4a953-707">Esempio di evento "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="4a953-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="4a953-708">Esempio di evento "RemoveShopCart":</span><span class="sxs-lookup"><span data-stu-id="4a953-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="4a953-709">Esempio di evento "Purchase":</span><span class="sxs-lookup"><span data-stu-id="4a953-709">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="4a953-710">Esempio di invio di due eventi, "Click" e "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="4a953-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="4a953-711">**Risposta**: Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="4a953-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-712">9.2.</span></span>    <span data-ttu-id="4a953-713">Elencare i file di dati di utilizzo del modello</span><span class="sxs-lookup"><span data-stu-id="4a953-713">List Model Usage Files</span></span>
<span data-ttu-id="4a953-714">Recupera i metadati di tutti i file di dati di utilizzo del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="4a953-715">Hello utilizzo file possono essere recuperati una sola pagina alla volta.</span><span class="sxs-lookup"><span data-stu-id="4a953-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="4a953-716">Ogni pagina contiene 100 elementi.</span><span class="sxs-lookup"><span data-stu-id="4a953-716">Each page containes 100 items.</span></span> <span data-ttu-id="4a953-717">Se si desidera tooget elementi da un indice specifico, è possibile utilizzare il parametro di odata hello $skip.</span><span class="sxs-lookup"><span data-stu-id="4a953-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="4a953-718">Ad esempio se si desidera tooget elementi a partire dalla posizione 100, aggiungere il parametro hello $skip = 100 toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="4a953-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="4a953-719">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-719">HTTP Method</span></span> | <span data-ttu-id="4a953-720">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-721">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-722">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-723">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-723">Parameter Name</span></span> | <span data-ttu-id="4a953-724">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="4a953-725">forModelId</span></span> |<span data-ttu-id="4a953-726">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-727">apiVersion</span></span> |<span data-ttu-id="4a953-728">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-728">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-729">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-729">Request Body</span></span> |<span data-ttu-id="4a953-730">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-730">NONE</span></span> |

<span data-ttu-id="4a953-731">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-731">**Response**:</span></span>

<span data-ttu-id="4a953-732">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-732">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-733">risposta Hello include una voce per ogni file di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="4a953-734">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-735">`feed\entry\content\properties\Id` : ID del file di dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="4a953-736">`feed\entry\content\properties\Length` : lunghezza del file di dati di utilizzo, in MB.</span><span class="sxs-lookup"><span data-stu-id="4a953-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="4a953-737">`feed\entry\content\properties\DateModified`-Data di creazione del file di utilizzo di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="4a953-738">`feed\entry\content\properties\UseInModel`-Se il file di utilizzo di hello viene utilizzato nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="4a953-739">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-739">OData XML</span></span>

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

### <a name="93----get-usage-statistics"></a><span data-ttu-id="4a953-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-740">9.3.</span></span>    <span data-ttu-id="4a953-741">Ottenere statistiche di utilizzo</span><span class="sxs-lookup"><span data-stu-id="4a953-741">Get Usage Statistics</span></span>
<span data-ttu-id="4a953-742">Ottiene le statistiche di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-742">Gets usage statistics.</span></span>

| <span data-ttu-id="4a953-743">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-743">HTTP Method</span></span> | <span data-ttu-id="4a953-744">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-745">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-746">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-747">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-747">Parameter Name</span></span> | <span data-ttu-id="4a953-748">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-749">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-749">modelId</span></span> |<span data-ttu-id="4a953-750">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-751">startDate</span><span class="sxs-lookup"><span data-stu-id="4a953-751">startDate</span></span> |<span data-ttu-id="4a953-752">Data di inizio.</span><span class="sxs-lookup"><span data-stu-id="4a953-752">Start date.</span></span> <span data-ttu-id="4a953-753">Formato: aaaa/MM/ggTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="4a953-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="4a953-754">endDate</span><span class="sxs-lookup"><span data-stu-id="4a953-754">endDate</span></span> |<span data-ttu-id="4a953-755">Data di fine.</span><span class="sxs-lookup"><span data-stu-id="4a953-755">End date.</span></span> <span data-ttu-id="4a953-756">Formato: aaaa/MM/ggTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="4a953-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="4a953-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="4a953-757">eventTypes</span></span> |<span data-ttu-id="4a953-758">Stringa delimitato da virgole di evento tipi o null tooget tutti gli eventi</span><span class="sxs-lookup"><span data-stu-id="4a953-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="4a953-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-759">apiVersion</span></span> |<span data-ttu-id="4a953-760">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-760">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-761">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-761">Request Body</span></span> |<span data-ttu-id="4a953-762">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-762">NONE</span></span> |

<span data-ttu-id="4a953-763">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-763">**Response**:</span></span>

<span data-ttu-id="4a953-764">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-764">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-765">Raccolta di elementi chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="4a953-765">A collection of key/value elements.</span></span> <span data-ttu-id="4a953-766">Ognuno di essi contiene somma hello di eventi per un tipo di evento specifico, raggruppate per ora.</span><span class="sxs-lookup"><span data-stu-id="4a953-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="4a953-767">`feed\entry[i]\content\properties\Key`-Contiene l'ora di hello (raggruppato per ora) e il tipo di evento hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="4a953-768">`feed\entry[i]\content\properties\Value` : numero totale di eventi.</span><span class="sxs-lookup"><span data-stu-id="4a953-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="4a953-769">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-769">OData XML</span></span>

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

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="4a953-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="4a953-770">9.4.</span></span>    <span data-ttu-id="4a953-771">Ottenere un esempio del file di dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="4a953-771">Get Usage File Sample</span></span>
<span data-ttu-id="4a953-772">Recupera hello prima 2KB di utilizzo del contenuto del file.</span><span class="sxs-lookup"><span data-stu-id="4a953-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="4a953-773">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-773">HTTP Method</span></span> | <span data-ttu-id="4a953-774">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-775">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-776">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-777">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-777">Parameter Name</span></span> | <span data-ttu-id="4a953-778">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-779">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-779">modelId</span></span> |<span data-ttu-id="4a953-780">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-781">fileId</span><span class="sxs-lookup"><span data-stu-id="4a953-781">fileId</span></span> |<span data-ttu-id="4a953-782">Identificatore univoco del file di modello di utilizzo hello</span><span class="sxs-lookup"><span data-stu-id="4a953-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="4a953-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-783">apiVersion</span></span> |<span data-ttu-id="4a953-784">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-784">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-785">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-785">Request Body</span></span> |<span data-ttu-id="4a953-786">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-786">NONE</span></span> |

<span data-ttu-id="4a953-787">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-787">**Response**:</span></span>

<span data-ttu-id="4a953-788">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-788">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-789">La risposta viene restituita in un formato di testo non elaborato:</span><span class="sxs-lookup"><span data-stu-id="4a953-789">Response is returned in raw text format:</span></span>

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


### <a name="95----get-model-usage-file"></a><span data-ttu-id="4a953-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="4a953-790">9.5.</span></span>    <span data-ttu-id="4a953-791">Ottenere il file di dati di utilizzo del modello</span><span class="sxs-lookup"><span data-stu-id="4a953-791">Get Model Usage File</span></span>
<span data-ttu-id="4a953-792">Recupera hello contenuto completo del file di utilizzo di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="4a953-793">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-793">HTTP Method</span></span> | <span data-ttu-id="4a953-794">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-795">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-796">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-797">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-797">Parameter Name</span></span> | <span data-ttu-id="4a953-798">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-799">mid</span><span class="sxs-lookup"><span data-stu-id="4a953-799">mid</span></span> |<span data-ttu-id="4a953-800">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-801">fid</span><span class="sxs-lookup"><span data-stu-id="4a953-801">fid</span></span> |<span data-ttu-id="4a953-802">Identificatore univoco del file di modello di utilizzo hello</span><span class="sxs-lookup"><span data-stu-id="4a953-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="4a953-803">download</span><span class="sxs-lookup"><span data-stu-id="4a953-803">download</span></span> |<span data-ttu-id="4a953-804">1</span><span class="sxs-lookup"><span data-stu-id="4a953-804">1</span></span> |
| <span data-ttu-id="4a953-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-805">apiVersion</span></span> |<span data-ttu-id="4a953-806">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-806">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-807">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-807">Request Body</span></span> |<span data-ttu-id="4a953-808">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-808">NONE</span></span> |

<span data-ttu-id="4a953-809">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-809">**Response**:</span></span>

<span data-ttu-id="4a953-810">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-810">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-811">La risposta viene restituita in un formato di testo non elaborato:</span><span class="sxs-lookup"><span data-stu-id="4a953-811">Response is returned in raw text format:</span></span>

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

### <a name="96----delete-usage-file"></a><span data-ttu-id="4a953-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="4a953-812">9.6.</span></span>    <span data-ttu-id="4a953-813">Eliminare il file di dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="4a953-813">Delete Usage File</span></span>
<span data-ttu-id="4a953-814">Elimina i file di utilizzo del modello specificato hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="4a953-815">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-815">HTTP Method</span></span> | <span data-ttu-id="4a953-816">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-817">DELETE</span><span class="sxs-lookup"><span data-stu-id="4a953-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-818">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-819">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-819">Parameter Name</span></span> | <span data-ttu-id="4a953-820">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-821">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-821">modelId</span></span> |<span data-ttu-id="4a953-822">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-823">fileId</span><span class="sxs-lookup"><span data-stu-id="4a953-823">fileId</span></span> |<span data-ttu-id="4a953-824">Identificatore univoco del toobe file hello eliminato</span><span class="sxs-lookup"><span data-stu-id="4a953-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="4a953-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-825">apiVersion</span></span> |<span data-ttu-id="4a953-826">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-826">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-827">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-827">Request Body</span></span> |<span data-ttu-id="4a953-828">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-828">NONE</span></span> |

<span data-ttu-id="4a953-829">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-829">**Response**:</span></span>

<span data-ttu-id="4a953-830">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="4a953-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="4a953-831">9.7.</span></span>    <span data-ttu-id="4a953-832">Eliminare tutti i file di dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="4a953-832">Delete All Usage Files</span></span>
<span data-ttu-id="4a953-833">Elimina tutti i file di dati di utilizzo del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="4a953-834">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-834">HTTP Method</span></span> | <span data-ttu-id="4a953-835">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-836">DELETE</span><span class="sxs-lookup"><span data-stu-id="4a953-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-837">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-838">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-838">Parameter Name</span></span> | <span data-ttu-id="4a953-839">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-840">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-840">modelId</span></span> |<span data-ttu-id="4a953-841">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-842">apiVersion</span></span> |<span data-ttu-id="4a953-843">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-843">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-844">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-844">Request Body</span></span> |<span data-ttu-id="4a953-845">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-845">NONE</span></span> |

<span data-ttu-id="4a953-846">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-846">**Response**:</span></span>

<span data-ttu-id="4a953-847">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="4a953-848">10. Funzionalità</span><span class="sxs-lookup"><span data-stu-id="4a953-848">10. Features</span></span>
<span data-ttu-id="4a953-849">In questa sezione viene illustrato come tooretrieve funzionalità informazioni, ad esempio funzionalità di hello importato e i relativi valori, il numero di dimensioni e quando è stata allocata questa classificazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="4a953-850">Le funzionalità vengono importate come parte di dati del catalogo hello e quindi dal numero di dimensioni è associata quando viene eseguita una compilazione di rango.</span><span class="sxs-lookup"><span data-stu-id="4a953-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="4a953-851">Priorità di funzionalità è possibile modificare secondo toohello modello di dati di utilizzo e tipo di elementi.</span><span class="sxs-lookup"><span data-stu-id="4a953-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="4a953-852">Ma per gli elementi/utilizzo coerenti, rank hello devono avere solo le variazioni di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="4a953-853">funzioni di rango Hello è un numero non negativo.</span><span class="sxs-lookup"><span data-stu-id="4a953-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="4a953-854">Hello numero 0 indica che non è stato classificato funzionalità hello (avviene se si richiama questo completamento toohello precedente API di compilazione rank prima hello).</span><span class="sxs-lookup"><span data-stu-id="4a953-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="4a953-855">Data Hello in corrispondenza del quale è stato attribuito rango hello viene chiamato all'aggiornamento di punteggio hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="4a953-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-856">10.1.</span></span> <span data-ttu-id="4a953-857">Ottenere informazioni sulle funzionalità (per l'ultima compilazione della classifica)</span><span class="sxs-lookup"><span data-stu-id="4a953-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="4a953-858">Recupera le informazioni sulla funzionalità di hello, tra cui classificazione, per hello ultima rank compilazione completata.</span><span class="sxs-lookup"><span data-stu-id="4a953-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="4a953-859">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-859">HTTP Method</span></span> | <span data-ttu-id="4a953-860">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-861">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-862">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-863">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-863">Parameter Name</span></span> | <span data-ttu-id="4a953-864">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-865">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-865">modelId</span></span> |<span data-ttu-id="4a953-866">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="4a953-867">samplingSize</span></span> |<span data-ttu-id="4a953-868">Numero di valori tooinclude per ogni funzionalità in base a dati toohello presenti nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="4a953-869">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="4a953-869">Possible values are:</span></span><br> <span data-ttu-id="4a953-870">-1, tutti i campioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-870">-1 - All samples.</span></span> <br><span data-ttu-id="4a953-871">0, nessun campionamento.</span><span class="sxs-lookup"><span data-stu-id="4a953-871">0 - No sampling.</span></span> <br><span data-ttu-id="4a953-872">N, restituisce N campioni per ogni nome di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="4a953-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-873">apiVersion</span></span> |<span data-ttu-id="4a953-874">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-874">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-875">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-875">Request Body</span></span> |<span data-ttu-id="4a953-876">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-876">NONE</span></span> |

<span data-ttu-id="4a953-877">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-877">**Response**:</span></span>

<span data-ttu-id="4a953-878">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-878">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-879">risposta Hello contiene un elenco di voci di informazioni sulla funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="4a953-880">Ogni voce contiene:</span><span class="sxs-lookup"><span data-stu-id="4a953-880">Each entry contains:</span></span>

* <span data-ttu-id="4a953-881">`feed/entry/content/m:properties/d:Name` : nome della funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="4a953-882">`feed/entry/content/m:properties/d:RankUpdateDate`-Data in cui hello rank è stato allocato toothis funzionalità, anche noto come</span><span class="sxs-lookup"><span data-stu-id="4a953-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="4a953-883">funzionalità di aggiornamento del punteggio.</span><span class="sxs-lookup"><span data-stu-id="4a953-883">score freshness feature.</span></span> <span data-ttu-id="4a953-884">Una data cronologica ("0001-01-01T00:00:00") indica che non è stata eseguita alcuna compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="4a953-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="4a953-885">`feed/entry/content/m:properties/d:Rank` classificazione delle funzionalità (mobile).</span><span class="sxs-lookup"><span data-stu-id="4a953-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="4a953-886">Una classificazione pari ad almeno 2.0 è considerata una funzionalità valida.</span><span class="sxs-lookup"><span data-stu-id="4a953-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="4a953-887">`feed/entry/content/m:properties/d:SampleValues`-Elenco delimitato da virgole dei valori di dimensione di campionamento toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="4a953-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="4a953-888">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
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

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="4a953-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-889">10.2.</span></span> <span data-ttu-id="4a953-890">Ottenere informazioni sulle funzionalità (per la specifica compilazione della classifica)</span><span class="sxs-lookup"><span data-stu-id="4a953-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="4a953-891">Recupera le informazioni sulla funzionalità di hello, tra cui classificazione per una compilazione specifica rank hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="4a953-892">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-892">HTTP Method</span></span> | <span data-ttu-id="4a953-893">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-894">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-895">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-896">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-896">Parameter Name</span></span> | <span data-ttu-id="4a953-897">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-898">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-898">modelId</span></span> |<span data-ttu-id="4a953-899">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="4a953-900">samplingSize</span></span> |<span data-ttu-id="4a953-901">Numero di valori tooinclude per ogni funzionalità in base a dati toohello presenti nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="4a953-902">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="4a953-902">Possible values are:</span></span><br> <span data-ttu-id="4a953-903">-1, tutti i campioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-903">-1 - All samples.</span></span> <br><span data-ttu-id="4a953-904">0, nessun campionamento.</span><span class="sxs-lookup"><span data-stu-id="4a953-904">0 - No sampling.</span></span> <br><span data-ttu-id="4a953-905">N, restituisce N campioni per ogni nome di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="4a953-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="4a953-906">rankBuildId</span></span> |<span data-ttu-id="4a953-907">Identificatore univoco della compilazione rank hello o -1 per la compilazione di rango ultimo hello</span><span class="sxs-lookup"><span data-stu-id="4a953-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="4a953-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-908">apiVersion</span></span> |<span data-ttu-id="4a953-909">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-909">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-910">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-910">Request Body</span></span> |<span data-ttu-id="4a953-911">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-911">NONE</span></span> |

<span data-ttu-id="4a953-912">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-912">**Response**:</span></span>

<span data-ttu-id="4a953-913">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-913">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-914">risposta Hello contiene un elenco di voci di informazioni sulla funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="4a953-915">Ogni voce contiene:</span><span class="sxs-lookup"><span data-stu-id="4a953-915">Each entry contains:</span></span>

* <span data-ttu-id="4a953-916">`feed/entry/content/m:properties/d:Name` : nome della funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="4a953-917">`feed/entry/content/m:properties/d:RankUpdateDate`-Data in cui hello rank è stato allocato toothis funzionalità, anche noto come</span><span class="sxs-lookup"><span data-stu-id="4a953-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="4a953-918">funzionalità di aggiornamento del punteggio.</span><span class="sxs-lookup"><span data-stu-id="4a953-918">score freshness feature.</span></span> <span data-ttu-id="4a953-919">Una data cronologica ("0001-01-01T00:00:00") indica che non è stata eseguita alcuna compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="4a953-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="4a953-920">`feed/entry/content/m:properties/d:Rank` classificazione delle funzionalità (mobile).</span><span class="sxs-lookup"><span data-stu-id="4a953-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="4a953-921">Una classificazione pari ad almeno 2.0 è considerata una funzionalità valida.</span><span class="sxs-lookup"><span data-stu-id="4a953-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="4a953-922">`feed/entry/content/m:properties/d:SampleValues`-Elenco delimitato da virgole dei valori di dimensione di campionamento toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="4a953-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="4a953-923">OData</span><span class="sxs-lookup"><span data-stu-id="4a953-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
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


## <a name="11-build"></a><span data-ttu-id="4a953-924">11. Compilare</span><span class="sxs-lookup"><span data-stu-id="4a953-924">11. Build</span></span>
  <span data-ttu-id="4a953-925">In questa sezione viene hello diverse API correlate toobuilds.</span><span class="sxs-lookup"><span data-stu-id="4a953-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="4a953-926">Esistono tre tipi di compilazione: una compilazione raccomandazione, una compilazione classifica e una compilazione FBT (Frequently Bought Together).</span><span class="sxs-lookup"><span data-stu-id="4a953-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="4a953-927">scopo della generazione dell'indicazione di Hello è toogenerate un modello di raccomandazione utilizzato per le stime.</span><span class="sxs-lookup"><span data-stu-id="4a953-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="4a953-928">Le stime (per questo tipo di compilazione) sono di due tipi:</span><span class="sxs-lookup"><span data-stu-id="4a953-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="4a953-929">I2I, nota anche come</span><span class="sxs-lookup"><span data-stu-id="4a953-929">I2I - a.k.a.</span></span> <span data-ttu-id="4a953-930">Elemento indicazioni tooItem - un elemento o un elenco specificati di elementi di questa opzione verrà stimare un elenco di elementi che sono probabilmente toobe di grande interesse.</span><span class="sxs-lookup"><span data-stu-id="4a953-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="4a953-931">U2I, nota anche come</span><span class="sxs-lookup"><span data-stu-id="4a953-931">U2I - a.k.a.</span></span> <span data-ttu-id="4a953-932">Indicazioni tooItem utente, dati un id utente (ed eventualmente un elenco di elementi) questa opzione verrà stimare un elenco di elementi che sono probabilmente toobe di grande interesse per hello dato utente (e la scelta degli elementi aggiuntiva).</span><span class="sxs-lookup"><span data-stu-id="4a953-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="4a953-933">indicazioni U2I Hello sono basati su Cronologia hello degli elementi che sono stati di interesse per l'utente hello tempo toohello hello modello è stato compilato.</span><span class="sxs-lookup"><span data-stu-id="4a953-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="4a953-934">Una build rank è una tecnica che consente di toolearn sull'utilità hello le caratteristiche.</span><span class="sxs-lookup"><span data-stu-id="4a953-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="4a953-935">In genere, in ordine tooget hello ottenere risultati migliori per un modello di raccomandazione che include le funzionalità, è necessario intraprendere hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4a953-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="4a953-936">Attivare una compilazione rango (a meno che il punteggio di hello le caratteristiche stabile) e attendere che si ottiene il punteggio di funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="4a953-937">Recuperare le funzioni di rango hello dal chiamante hello [Get Info funzionalità](#101-get-features-info-for-last-rank-build) API.</span><span class="sxs-lookup"><span data-stu-id="4a953-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="4a953-938">Configurare una compilazione di raccomandazione con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="4a953-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="4a953-939">`useFeatureInModel`-Impostare tooTrue.</span><span class="sxs-lookup"><span data-stu-id="4a953-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="4a953-940">`ModelingFeatureList`-Set tooa elenco delimitato da virgole delle funzioni con un punteggio pari a 2.0 o superiore (in base intervalli toohello recuperato nel passaggio precedente hello).</span><span class="sxs-lookup"><span data-stu-id="4a953-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="4a953-941">`AllowColdItemPlacement`-Impostare tooTrue.</span><span class="sxs-lookup"><span data-stu-id="4a953-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="4a953-942">Facoltativamente è possibile impostare `EnableFeatureCorrelation` tooTrue e `ReasoningFeatureList` toohello elenco di funzionalità da toouse per una spiegazione (in genere hello stesso elenco di funzionalità utilizzato nella modellazione o un sottoelenco).</span><span class="sxs-lookup"><span data-stu-id="4a953-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="4a953-943">Compilazione di raccomandazione hello trigger con hello configurato i parametri.</span><span class="sxs-lookup"><span data-stu-id="4a953-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="4a953-944">Nota: Se non si configura parametri (ad esempio invoke hello raccomandazione compilazione senza parametri) o non si disabilita in modo esplicito sull'utilizzo di hello delle funzionalità (ad esempio, `UseFeatureInModel` impostare tooFalse), verrà impostato dal sistema hello i parametri correlati alle funzionalità di hello toohello illustrato sopra i valori nel caso in cui esiste una compilazione di rango.</span><span class="sxs-lookup"><span data-stu-id="4a953-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="4a953-945">Non vi è alcuna restrizione sull'esecuzione di una compilazione rank e un'indicazione compilare contemporaneamente per hello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="4a953-946">Tuttavia, è possibile eseguire due generazioni di hello dello stesso tipo in hello stesso modello in parallelo.</span><span class="sxs-lookup"><span data-stu-id="4a953-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="4a953-947">Una compilazione FBT (Frequently Bought Together) è un altro algoritmo di raccomandazione, detto a volte sistema di raccomandazione "conservativo", che risulta appropriato per i cataloghi non omogenei per natura (omogenei: libri, film, alcuni alimenti, moda; non omogenei: computer e dispositivi, interdominio, estremamente diversi).</span><span class="sxs-lookup"><span data-stu-id="4a953-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="4a953-948">Nota: se file di utilizzo caricati hello contengono il campo facoltativo hello "tipo di evento", per rate delle imposte modellazione solo gli eventi "Acquisto" verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="4a953-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="4a953-949">Se non viene specificato alcun tipo di evento, tutti gli eventi verranno considerati come acquisti.</span><span class="sxs-lookup"><span data-stu-id="4a953-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="4a953-950">11.1 Parametri della compilazione</span><span class="sxs-lookup"><span data-stu-id="4a953-950">11.1 Build parameters</span></span>
<span data-ttu-id="4a953-951">Ogni tipo di compilazione può essere configurato con un set di parametri, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4a953-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="4a953-952">Se non si configurano parametri hello, sistema di hello verrà automaticamente attributo parametri toohello valori in base a informazioni toohello presente in fase di hello attiva una compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="4a953-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-953">11.1.1.</span></span> <span data-ttu-id="4a953-954">Concentrazione dei dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="4a953-954">Usage condenser</span></span>
<span data-ttu-id="4a953-955">Gli utenti o gli elementi con pochi punti di utilizzo possono contenere una quantità di dati non significativi maggiore delle informazioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="4a953-956">sistema di Hello tenta toopredict hello il numero minimo di punti di utilizzo per utente o elemento toobe utilizzata in un modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="4a953-957">Questo numero sia nell'intervallo di hello definito da hello ItemCutoffLowerBound e ItemCutoffUpperBound parametri per gli elementi e intervallo di hello definito da hello UserCutOffLowerBound e UserCutoffUpperBound parametri per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="4a953-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="4a953-958">effetto condensatore Hello su elementi o gli utenti può essere ridotto dall'impostazione di almeno una di hello corrispondente limiti toozero.</span><span class="sxs-lookup"><span data-stu-id="4a953-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="4a953-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-959">11.1.2.</span></span> <span data-ttu-id="4a953-960">Parametri di compilazione della classifica</span><span class="sxs-lookup"><span data-stu-id="4a953-960">Rank build parameters</span></span>
<span data-ttu-id="4a953-961">tabella Hello seguente illustra i parametri di compilazione hello per una compilazione di rango.</span><span class="sxs-lookup"><span data-stu-id="4a953-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="4a953-962">Chiave</span><span class="sxs-lookup"><span data-stu-id="4a953-962">Key</span></span> | <span data-ttu-id="4a953-963">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-963">Description</span></span> | <span data-ttu-id="4a953-964">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a953-964">Type</span></span> | <span data-ttu-id="4a953-965">Valore valido</span><span class="sxs-lookup"><span data-stu-id="4a953-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4a953-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="4a953-966">NumberOfModelIterations</span></span> |<span data-ttu-id="4a953-967">numero di Hello di iterazioni esegue modello hello è rappresentato dalle hello complessiva di calcolo tempo e hello accuratezza del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="4a953-968">maggiore hello Hello, una maggiore accuratezza hello che verrà creato, ma hello calcolo richiederà più tempo.</span><span class="sxs-lookup"><span data-stu-id="4a953-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="4a953-969">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-969">Integer</span></span> |<span data-ttu-id="4a953-970">10-50</span><span class="sxs-lookup"><span data-stu-id="4a953-970">10-50</span></span> |
| <span data-ttu-id="4a953-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="4a953-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="4a953-972">numero di Hello di dimensioni riguarda il numero di toohello del modello di hello 'funzionalità' tenterà toofind all'interno dei dati.</span><span class="sxs-lookup"><span data-stu-id="4a953-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="4a953-973">Aumentare il numero di hello dimensioni consente una migliore ottimizzazione dei risultati di hello in cluster più piccoli.</span><span class="sxs-lookup"><span data-stu-id="4a953-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="4a953-974">Tuttavia, troppe dimensioni impedirà modello hello di individuazione delle correlazioni tra gli elementi.</span><span class="sxs-lookup"><span data-stu-id="4a953-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="4a953-975">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-975">Integer</span></span> |<span data-ttu-id="4a953-976">10-40</span><span class="sxs-lookup"><span data-stu-id="4a953-976">10-40</span></span> |
| <span data-ttu-id="4a953-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="4a953-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="4a953-978">Definisce hello elemento limite inferiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="4a953-979">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-979">See usage condenser above.</span></span> |<span data-ttu-id="4a953-980">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-980">Integer</span></span> |<span data-ttu-id="4a953-981">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="4a953-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="4a953-983">Definisce hello elemento limite superiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="4a953-984">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-984">See usage condenser above.</span></span> |<span data-ttu-id="4a953-985">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-985">Integer</span></span> |<span data-ttu-id="4a953-986">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="4a953-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="4a953-988">Definisce hello utente limite inferiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="4a953-989">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-989">See usage condenser above.</span></span> |<span data-ttu-id="4a953-990">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-990">Integer</span></span> |<span data-ttu-id="4a953-991">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="4a953-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="4a953-993">Definisce hello utente limite superiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="4a953-994">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-994">See usage condenser above.</span></span> |<span data-ttu-id="4a953-995">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-995">Integer</span></span> |<span data-ttu-id="4a953-996">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="4a953-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-997">11.1.3.</span></span> <span data-ttu-id="4a953-998">Parametri della compilazione di raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="4a953-998">Recommendation build parameters</span></span>
<span data-ttu-id="4a953-999">tabella Hello seguente illustra i parametri di compilazione hello per la compilazione di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="4a953-1000">Chiave</span><span class="sxs-lookup"><span data-stu-id="4a953-1000">Key</span></span> | <span data-ttu-id="4a953-1001">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-1001">Description</span></span> | <span data-ttu-id="4a953-1002">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a953-1002">Type</span></span> | <span data-ttu-id="4a953-1003">Valore valido</span><span class="sxs-lookup"><span data-stu-id="4a953-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4a953-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="4a953-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="4a953-1005">numero di Hello di iterazioni esegue modello hello è rappresentato dalle hello complessiva di calcolo tempo e hello accuratezza del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="4a953-1006">maggiore hello Hello, una maggiore accuratezza hello che verrà creato, ma hello calcolo richiederà più tempo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="4a953-1007">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1007">Integer</span></span> |<span data-ttu-id="4a953-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="4a953-1008">10-50</span></span> |
| <span data-ttu-id="4a953-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="4a953-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="4a953-1010">numero di Hello di dimensioni riguarda il numero di toohello del modello di hello 'funzionalità' tenterà toofind all'interno dei dati.</span><span class="sxs-lookup"><span data-stu-id="4a953-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="4a953-1011">Aumentare il numero di hello dimensioni consente una migliore ottimizzazione dei risultati di hello in cluster più piccoli.</span><span class="sxs-lookup"><span data-stu-id="4a953-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="4a953-1012">Tuttavia, troppe dimensioni impedirà modello hello di individuazione delle correlazioni tra gli elementi.</span><span class="sxs-lookup"><span data-stu-id="4a953-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="4a953-1013">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1013">Integer</span></span> |<span data-ttu-id="4a953-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="4a953-1014">10-40</span></span> |
| <span data-ttu-id="4a953-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="4a953-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="4a953-1016">Definisce hello elemento limite inferiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="4a953-1017">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1017">See usage condenser above.</span></span> |<span data-ttu-id="4a953-1018">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1018">Integer</span></span> |<span data-ttu-id="4a953-1019">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="4a953-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="4a953-1021">Definisce hello elemento limite superiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="4a953-1022">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1022">See usage condenser above.</span></span> |<span data-ttu-id="4a953-1023">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1023">Integer</span></span> |<span data-ttu-id="4a953-1024">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="4a953-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="4a953-1026">Definisce hello utente limite inferiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="4a953-1027">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1027">See usage condenser above.</span></span> |<span data-ttu-id="4a953-1028">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1028">Integer</span></span> |<span data-ttu-id="4a953-1029">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="4a953-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="4a953-1031">Definisce hello utente limite superiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="4a953-1032">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1032">See usage condenser above.</span></span> |<span data-ttu-id="4a953-1033">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1033">Integer</span></span> |<span data-ttu-id="4a953-1034">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-1035">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-1035">Description</span></span> |<span data-ttu-id="4a953-1036">Descrizione della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1036">Build description.</span></span> |<span data-ttu-id="4a953-1037">String</span><span class="sxs-lookup"><span data-stu-id="4a953-1037">String</span></span> |<span data-ttu-id="4a953-1038">Qualsiasi testo, con un massimo di 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="4a953-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="4a953-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="4a953-1039">EnableModelingInsights</span></span> |<span data-ttu-id="4a953-1040">Consente di metriche toocompute nel modello di raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="4a953-1041">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1041">Boolean</span></span> |<span data-ttu-id="4a953-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="4a953-1042">True/False</span></span> |
| <span data-ttu-id="4a953-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="4a953-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="4a953-1044">Indica se è possano utilizzare le funzionalità nel modello di raccomandazione hello tooenhance ordine.</span><span class="sxs-lookup"><span data-stu-id="4a953-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="4a953-1045">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1045">Boolean</span></span> |<span data-ttu-id="4a953-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="4a953-1046">True/False</span></span> |
| <span data-ttu-id="4a953-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="4a953-1047">ModelingFeatureList</span></span> |<span data-ttu-id="4a953-1048">Elenco delimitato da virgole di toobe di nomi di funzionalità utilizzate nella compilazione di raccomandazione hello, nella raccomandazione di hello tooenhance ordine.</span><span class="sxs-lookup"><span data-stu-id="4a953-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="4a953-1049">String</span><span class="sxs-lookup"><span data-stu-id="4a953-1049">String</span></span> |<span data-ttu-id="4a953-1050">Nomi delle funzionalità, i caratteri too512</span><span class="sxs-lookup"><span data-stu-id="4a953-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="4a953-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="4a953-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="4a953-1052">Indica se raccomandazione hello deve eseguire anche il push agli elementi ignoti tramite somiglianza funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="4a953-1053">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1053">Boolean</span></span> |<span data-ttu-id="4a953-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="4a953-1054">True/False</span></span> |
| <span data-ttu-id="4a953-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="4a953-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="4a953-1056">Indica se le funzionalità possono essere usate nella motivazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="4a953-1057">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1057">Boolean</span></span> |<span data-ttu-id="4a953-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="4a953-1058">True/False</span></span> |
| <span data-ttu-id="4a953-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="4a953-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="4a953-1060">Elenco delimitato da virgole di funzionalità nomi toobe utilizzato per ragionamento frasi (ad esempio, descrizioni di raccomandazione).</span><span class="sxs-lookup"><span data-stu-id="4a953-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="4a953-1061">String</span><span class="sxs-lookup"><span data-stu-id="4a953-1061">String</span></span> |<span data-ttu-id="4a953-1062">Nomi delle funzionalità, i caratteri too512</span><span class="sxs-lookup"><span data-stu-id="4a953-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="4a953-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="4a953-1063">EnableU2I</span></span> |<span data-ttu-id="4a953-1064">Consentire anche noto come raccomandazione hello personalizzato</span><span class="sxs-lookup"><span data-stu-id="4a953-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="4a953-1065">U2I (indicazioni tooitem utente).</span><span class="sxs-lookup"><span data-stu-id="4a953-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="4a953-1066">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1066">Boolean</span></span> |<span data-ttu-id="4a953-1067">True/False (valore predefinito true)</span><span class="sxs-lookup"><span data-stu-id="4a953-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="4a953-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="4a953-1068">11.1.4.</span></span> <span data-ttu-id="4a953-1069">Parametri della compilazione FBT</span><span class="sxs-lookup"><span data-stu-id="4a953-1069">FBT build parameters</span></span>
<span data-ttu-id="4a953-1070">tabella Hello seguente illustra i parametri di compilazione hello per la compilazione di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="4a953-1071">Chiave</span><span class="sxs-lookup"><span data-stu-id="4a953-1071">Key</span></span> | <span data-ttu-id="4a953-1072">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-1072">Description</span></span> | <span data-ttu-id="4a953-1073">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a953-1073">Type</span></span> | <span data-ttu-id="4a953-1074">Valore valido (predefinito)</span><span class="sxs-lookup"><span data-stu-id="4a953-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4a953-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="4a953-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="4a953-1076">Come modello conservativo hello è.</span><span class="sxs-lookup"><span data-stu-id="4a953-1076">How conservative hello model is.</span></span> <span data-ttu-id="4a953-1077">Numero di occorrenze di condivisione di elementi toobe considerati per la modellazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="4a953-1078">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1078">Integer</span></span> |<span data-ttu-id="4a953-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="4a953-1079">3-50 (6)</span></span> |
| <span data-ttu-id="4a953-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="4a953-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="4a953-1081">Limiti hello numero di elementi in un set di frequente.</span><span class="sxs-lookup"><span data-stu-id="4a953-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="4a953-1082">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1082">Integer</span></span> |<span data-ttu-id="4a953-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="4a953-1083">2-3 (2)</span></span> |
| <span data-ttu-id="4a953-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="4a953-1084">FbtMinimalScore</span></span> |<span data-ttu-id="4a953-1085">Punteggio minimo che un set di frequente deve disporre in ordine toobe incluso in hello restituito risultati.</span><span class="sxs-lookup"><span data-stu-id="4a953-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="4a953-1086">hello superiore Hello migliorato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1086">hello higher hello better.</span></span> |<span data-ttu-id="4a953-1087">Double</span><span class="sxs-lookup"><span data-stu-id="4a953-1087">Double</span></span> |<span data-ttu-id="4a953-1088">0 e superiore (0)</span><span class="sxs-lookup"><span data-stu-id="4a953-1088">0 and above (0)</span></span> |
| <span data-ttu-id="4a953-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="4a953-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="4a953-1090">Definisce hello toobe di funzione di somiglianza utilizzato dalla compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="4a953-1091">Accuratezza predilige serendipity CO-occorrenza predilige prevedibilità e Jaccard è un compromesso tra due hello nice.</span><span class="sxs-lookup"><span data-stu-id="4a953-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="4a953-1092">String</span><span class="sxs-lookup"><span data-stu-id="4a953-1092">String</span></span> |<span data-ttu-id="4a953-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="4a953-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="4a953-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-1094">11.2.</span></span> <span data-ttu-id="4a953-1095">Attivare una compilazione di raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="4a953-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="4a953-1096">Per impostazione predefinita, questa API attiverà la compilazione di un modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="4a953-1097">tootrigger una classificazione di compilazione (in funzionalità tooscore ordine), variant di API di compilazione hello con il parametro di tipo di compilazione deve essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="4a953-1098">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1098">HTTP Method</span></span> | <span data-ttu-id="4a953-1099">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1100">POST</span><span class="sxs-lookup"><span data-stu-id="4a953-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1101">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="4a953-1102">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="4a953-1102">HEADER</span></span> |<span data-ttu-id="4a953-1103">`"Content-Type", "text/xml"` (Se si sta inviando il corpo della richiesta)</span><span class="sxs-lookup"><span data-stu-id="4a953-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="4a953-1104">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1104">Parameter Name</span></span> | <span data-ttu-id="4a953-1105">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1106">modelId</span></span> |<span data-ttu-id="4a953-1107">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="4a953-1108">userDescription</span></span> |<span data-ttu-id="4a953-1109">Identificatore testuale del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="4a953-1110">Tenere presente che, se si usano degli spazi, è necessario codificarli con il simbolo %20.</span><span class="sxs-lookup"><span data-stu-id="4a953-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="4a953-1111">Vedere l'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="4a953-1111">See example above.</span></span><br><span data-ttu-id="4a953-1112">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4a953-1112">Max length: 50</span></span> |
| <span data-ttu-id="4a953-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1113">apiVersion</span></span> |<span data-ttu-id="4a953-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-1115">Request Body</span><span class="sxs-lookup"><span data-stu-id="4a953-1115">Request Body</span></span> |<span data-ttu-id="4a953-1116">Se lasciato vuoto compilazione hello verrà eseguito con i parametri di compilazione predefiniti hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="4a953-1117">Se si desidera tooset parametri di compilazione hello, inviare parametri hello come XML nel corpo di hello come hello seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="4a953-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="4a953-1118">(Vedere la sezione hello "parametri di compilazione" per una spiegazione dei parametri di hello).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="4a953-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="4a953-1119">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-1119">**Response**:</span></span>

<span data-ttu-id="4a953-1120">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1121">Questa è un'API asincrona.</span><span class="sxs-lookup"><span data-stu-id="4a953-1121">This is an asynchronous API.</span></span> <span data-ttu-id="4a953-1122">Come risposta si otterrà un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="4a953-1123">tooknow al termine di generazione di hello, è necessario chiamare API "Ottenere compilazioni lo stato di un modello di" hello e individuare questo ID di generazione in risposta hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="4a953-1124">Si noti che una compilazione può richiedere da toohours minuti a seconda delle dimensioni di hello dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="4a953-1125">Impossibile consumare indicazioni finché non termina di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="4a953-1126">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="4a953-1126">Valid build status:</span></span>

* <span data-ttu-id="4a953-1127">Create: è stata creata una richiesta di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="4a953-1128">Queued: la richiesta di compilazione è stata inviata e accodata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="4a953-1129">Building: la compilazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="4a953-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="4a953-1130">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="4a953-1131">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="4a953-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="4a953-1132">Cancelled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="4a953-1133">L'annullamento - è stata inviata una richiesta di annullamento per la compilazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="4a953-1134">Si noti che compilazione hello che ID è reperibile nella hello seguente percorso:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="4a953-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="4a953-1135">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1135">OData XML</span></span>

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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="4a953-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-1136">11.3.</span></span> <span data-ttu-id="4a953-1137">Attivare la compilazione (di raccomandazioni, della classifica o FBT)</span><span class="sxs-lookup"><span data-stu-id="4a953-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="4a953-1138">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1138">HTTP Method</span></span> | <span data-ttu-id="4a953-1139">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1140">POST</span><span class="sxs-lookup"><span data-stu-id="4a953-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1141">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="4a953-1142">INTESTAZIONE</span><span class="sxs-lookup"><span data-stu-id="4a953-1142">HEADER</span></span> |<span data-ttu-id="4a953-1143">`"Content-Type", "text/xml"` (Se si sta inviando il corpo della richiesta)</span><span class="sxs-lookup"><span data-stu-id="4a953-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="4a953-1144">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1144">Parameter Name</span></span> | <span data-ttu-id="4a953-1145">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1146">modelId</span></span> |<span data-ttu-id="4a953-1147">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="4a953-1148">userDescription</span></span> |<span data-ttu-id="4a953-1149">Identificatore testuale del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="4a953-1150">Tenere presente che, se si usano degli spazi, è necessario codificarli con il simbolo %20.</span><span class="sxs-lookup"><span data-stu-id="4a953-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="4a953-1151">Vedere l'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="4a953-1151">See example above.</span></span><br><span data-ttu-id="4a953-1152">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4a953-1152">Max length: 50</span></span> |
| <span data-ttu-id="4a953-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="4a953-1153">buildType</span></span> |<span data-ttu-id="4a953-1154">Tipo di hello compilazione tooinvoke:</span><span class="sxs-lookup"><span data-stu-id="4a953-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="4a953-1155">- "Recommendation" per la compilazione di raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="4a953-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="4a953-1156">- "Ranking" per la compilazione di classifiche</span><span class="sxs-lookup"><span data-stu-id="4a953-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="4a953-1157">- "Fbt" per una compilazione FBT</span><span class="sxs-lookup"><span data-stu-id="4a953-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="4a953-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1158">apiVersion</span></span> |<span data-ttu-id="4a953-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-1160">Request Body</span><span class="sxs-lookup"><span data-stu-id="4a953-1160">Request Body</span></span> |<span data-ttu-id="4a953-1161">Se lasciato vuoto compilazione hello verrà eseguito con i parametri di compilazione predefiniti hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="4a953-1162">Se si desidera tooset parametri di compilazione, è necessario inviarle come XML nel corpo di hello come nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="4a953-1163">(Vedere la sezione hello "parametri di compilazione" per una spiegazione e un elenco completo dei parametri di hello).`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="4a953-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="4a953-1164">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-1164">**Response**:</span></span>

<span data-ttu-id="4a953-1165">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1166">Questa è un'API asincrona.</span><span class="sxs-lookup"><span data-stu-id="4a953-1166">This is an asynchronous API.</span></span> <span data-ttu-id="4a953-1167">Come risposta si otterrà un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="4a953-1168">tooknow al termine di generazione di hello, è necessario chiamare API "Ottenere compilazioni lo stato di un modello di" hello e individuare questo ID di generazione in risposta hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="4a953-1169">Si noti che una compilazione può richiedere da toohours minuti a seconda delle dimensioni di hello dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="4a953-1170">Impossibile consumare indicazioni finché non termina di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="4a953-1171">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="4a953-1171">Valid build status:</span></span>

* <span data-ttu-id="4a953-1172">Create: il modello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1172">Create - Model was created.</span></span>
* <span data-ttu-id="4a953-1173">Queued: la compilazione del modello è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="4a953-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="4a953-1174">Building: la compilazione del modello è in corso.</span><span class="sxs-lookup"><span data-stu-id="4a953-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="4a953-1175">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="4a953-1176">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="4a953-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="4a953-1177">Cancelled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="4a953-1178">Cancelling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="4a953-1179">Si noti che compilazione hello che ID è reperibile nella hello seguente percorso:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="4a953-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="4a953-1180">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1180">OData XML</span></span>

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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="4a953-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="4a953-1181">11.4.</span></span> <span data-ttu-id="4a953-1182">Ottenere lo stato delle compilazioni di un modello</span><span class="sxs-lookup"><span data-stu-id="4a953-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="4a953-1183">Recupera le compilazioni e il relativo stato per un modello specifico.</span><span class="sxs-lookup"><span data-stu-id="4a953-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="4a953-1184">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1184">HTTP Method</span></span> | <span data-ttu-id="4a953-1185">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1186">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1187">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1188">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1188">Parameter Name</span></span> | <span data-ttu-id="4a953-1189">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1190">modelId</span></span> |<span data-ttu-id="4a953-1191">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="4a953-1192">onlyLastBuild</span></span> |<span data-ttu-id="4a953-1193">Indica se tutti hello tooreturn compilare solo stato hello di compilazione più recente di hello o cronologia del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="4a953-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1194">apiVersion</span></span> |<span data-ttu-id="4a953-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1195">1.0</span></span> |

<span data-ttu-id="4a953-1196">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-1196">**Response**:</span></span>

<span data-ttu-id="4a953-1197">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1198">risposta Hello include una voce per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="4a953-1199">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1200">`feed/entry/content/properties/UserName`-Nome dell'utente di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="4a953-1201">`feed/entry/content/properties/ModelName`-Nome del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="4a953-1202">`feed/entry/content/properties/ModelId` : identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="4a953-1203">`feed/entry/content/properties/IsDeployed`-Se hello build è stata distribuita (anche noto come</span><span class="sxs-lookup"><span data-stu-id="4a953-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="4a953-1204">compilazione attiva).</span><span class="sxs-lookup"><span data-stu-id="4a953-1204">active build).</span></span>
* <span data-ttu-id="4a953-1205">`feed/entry/content/properties/BuildId` : identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="4a953-1206">`feed/entry/content/properties/BuildType`-Tipo di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="4a953-1207">`feed/entry/content/properties/Status` : stato della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="4a953-1208">Può essere uno dei seguenti hello: errore di compilazione, in coda, verrà annullata, annullato, esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="4a953-1209">`feed/entry/content/properties/StatusMessage`-Messaggio di stato detailed (si applica solo a toospecific stati).</span><span class="sxs-lookup"><span data-stu-id="4a953-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="4a953-1210">`feed/entry/content/properties/Progress` : stato di avanzamento della compilazione (%).</span><span class="sxs-lookup"><span data-stu-id="4a953-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="4a953-1211">`feed/entry/content/properties/StartTime` : data/ora di inizio della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="4a953-1212">`feed/entry/content/properties/EndTime` : data/ora di fine della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="4a953-1213">`feed/entry/content/properties/ExecutionTime` : durata della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="4a953-1214">`feed/entry/content/properties/ProgressStep`-Informazioni dettagliate sulla fase corrente di hello di una compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="4a953-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="4a953-1215">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="4a953-1215">Valid build status:</span></span>

* <span data-ttu-id="4a953-1216">Created: la voce della richiesta di compilazione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="4a953-1217">Queued: la richiesta di compilazione è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="4a953-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="4a953-1218">Building: la compilazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="4a953-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="4a953-1219">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="4a953-1220">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="4a953-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="4a953-1221">Cancelled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="4a953-1222">Cancelling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="4a953-1223">Valori validi per il tipo di compilazione:</span><span class="sxs-lookup"><span data-stu-id="4a953-1223">Valid values for build type:</span></span>

* <span data-ttu-id="4a953-1224">Rank: compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="4a953-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="4a953-1225">Recommendation: compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="4a953-1226">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1226">OData XML</span></span>

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


### <a name="115-get-builds-status"></a><span data-ttu-id="4a953-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="4a953-1227">11.5.</span></span> <span data-ttu-id="4a953-1228">Ottenere lo stato delle compilazioni</span><span class="sxs-lookup"><span data-stu-id="4a953-1228">Get Builds Status</span></span>
<span data-ttu-id="4a953-1229">Recupera lo stato delle compilazioni di tutti i modelli di un utente.</span><span class="sxs-lookup"><span data-stu-id="4a953-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="4a953-1230">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1230">HTTP Method</span></span> | <span data-ttu-id="4a953-1231">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1232">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1233">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1234">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1234">Parameter Name</span></span> | <span data-ttu-id="4a953-1235">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="4a953-1236">onlyLastBuild</span></span> |<span data-ttu-id="4a953-1237">Indica se tutti hello tooreturn compilare solo stato hello di compilazione più recente di hello o cronologia del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="4a953-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1238">apiVersion</span></span> |<span data-ttu-id="4a953-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1239">1.0</span></span> |

<span data-ttu-id="4a953-1240">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-1240">**Response**:</span></span>

<span data-ttu-id="4a953-1241">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1242">risposta Hello include una voce per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="4a953-1243">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1244">`feed/entry/content/properties/UserName`-Nome dell'utente di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="4a953-1245">`feed/entry/content/properties/ModelName`-Nome del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="4a953-1246">`feed/entry/content/properties/ModelId` : identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="4a953-1247">`feed/entry/content/properties/IsDeployed`-Se hello build è stata distribuita.</span><span class="sxs-lookup"><span data-stu-id="4a953-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="4a953-1248">`feed/entry/content/properties/BuildId` : identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="4a953-1249">`feed/entry/content/properties/BuildType`-Tipo di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="4a953-1250">`feed/entry/content/properties/Status` : stato della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="4a953-1251">Può essere uno dei seguenti hello: errore di compilazione, in coda, annullato, verrà annullata, esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="4a953-1252">`feed/entry/content/properties/StatusMessage`-Messaggio di stato detailed (si applica solo a toospecific stati).</span><span class="sxs-lookup"><span data-stu-id="4a953-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="4a953-1253">`feed/entry/content/properties/Progress` : stato di avanzamento della compilazione (%).</span><span class="sxs-lookup"><span data-stu-id="4a953-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="4a953-1254">`feed/entry/content/properties/StartTime` : data/ora di inizio della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="4a953-1255">`feed/entry/content/properties/EndTime` : data/ora di fine della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="4a953-1256">`feed/entry/content/properties/ExecutionTime` : durata della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="4a953-1257">`feed/entry/content/properties/ProgressStep`-Informazioni dettagliate sulla fase corrente di hello di una compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="4a953-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="4a953-1258">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="4a953-1258">Valid build status:</span></span>

* <span data-ttu-id="4a953-1259">Created: la voce della richiesta di compilazione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="4a953-1260">Queued: la richiesta di compilazione è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="4a953-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="4a953-1261">Building: la compilazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="4a953-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="4a953-1262">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="4a953-1263">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="4a953-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="4a953-1264">Cancelled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="4a953-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="4a953-1265">Cancelling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="4a953-1266">Valori validi per il tipo di compilazione:</span><span class="sxs-lookup"><span data-stu-id="4a953-1266">Valid values for build type:</span></span>

* <span data-ttu-id="4a953-1267">Rank: compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="4a953-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="4a953-1268">Recommendation: compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="4a953-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="4a953-1269">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1269">OData XML</span></span>

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


### <a name="116-delete-build"></a><span data-ttu-id="4a953-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="4a953-1270">11.6.</span></span> <span data-ttu-id="4a953-1271">Eliminare una compilazione</span><span class="sxs-lookup"><span data-stu-id="4a953-1271">Delete Build</span></span>
<span data-ttu-id="4a953-1272">Elimina una compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1272">Deletes a build.</span></span>

<span data-ttu-id="4a953-1273">NOTA: </span><span class="sxs-lookup"><span data-stu-id="4a953-1273">NOTE:</span></span> <br><span data-ttu-id="4a953-1274">Non è possibile eliminare una compilazione attiva.</span><span class="sxs-lookup"><span data-stu-id="4a953-1274">You cannot delete an active build.</span></span> <span data-ttu-id="4a953-1275">il modello Hello deve essere aggiornato compilazione attiva diverse tooa prima di eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="4a953-1276">Non è possibile eliminare una compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="4a953-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="4a953-1277">È necessario annullare prima compilazione hello chiamando <strong>Annulla compilazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="4a953-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="4a953-1278">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1278">HTTP Method</span></span> | <span data-ttu-id="4a953-1279">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1280">DELETE</span><span class="sxs-lookup"><span data-stu-id="4a953-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1281">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1282">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1282">Parameter Name</span></span> | <span data-ttu-id="4a953-1283">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-1284">buildId</span></span> |<span data-ttu-id="4a953-1285">Identificatore univoco della compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="4a953-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1286">apiVersion</span></span> |<span data-ttu-id="4a953-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1287">1.0</span></span> |

<span data-ttu-id="4a953-1288">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1288">**Response:**</span></span>

<span data-ttu-id="4a953-1289">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="4a953-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="4a953-1290">11.7.</span></span> <span data-ttu-id="4a953-1291">Annullare una compilazione</span><span class="sxs-lookup"><span data-stu-id="4a953-1291">Cancel Build</span></span>
<span data-ttu-id="4a953-1292">Annulla una compilazione nello stato di creazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="4a953-1293">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1293">HTTP Method</span></span> | <span data-ttu-id="4a953-1294">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="4a953-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1296">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1297">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1297">Parameter Name</span></span> | <span data-ttu-id="4a953-1298">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-1299">buildId</span></span> |<span data-ttu-id="4a953-1300">Identificatore univoco della compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="4a953-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1301">apiVersion</span></span> |<span data-ttu-id="4a953-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1302">1.0</span></span> |

<span data-ttu-id="4a953-1303">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1303">**Response:**</span></span>

<span data-ttu-id="4a953-1304">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="4a953-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="4a953-1305">11.8.</span></span> <span data-ttu-id="4a953-1306">Ottenere i parametri della compilazione</span><span class="sxs-lookup"><span data-stu-id="4a953-1306">Get Build Parameters</span></span>
<span data-ttu-id="4a953-1307">Recupera i parametri della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="4a953-1308">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1308">HTTP Method</span></span> | <span data-ttu-id="4a953-1309">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1310">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1311">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1312">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1312">Parameter Name</span></span> | <span data-ttu-id="4a953-1313">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-1314">buildId</span></span> |<span data-ttu-id="4a953-1315">Identificatore univoco della compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="4a953-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1316">apiVersion</span></span> |<span data-ttu-id="4a953-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1317">1.0</span></span> |

<span data-ttu-id="4a953-1318">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1318">**Response:**</span></span>

<span data-ttu-id="4a953-1319">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1320">L'API restituisce una raccolta di elementi chiave/valore.</span><span class="sxs-lookup"><span data-stu-id="4a953-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="4a953-1321">Ogni elemento rappresenta un parametro e il relativo valore:</span><span class="sxs-lookup"><span data-stu-id="4a953-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="4a953-1322">`feed/entry/content/properties/Key` : nome del parametro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="4a953-1323">`feed/entry/content/properties/Value` : valore del parametro di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="4a953-1324">tabella Hello riportata di seguito viene illustrata valore hello che rappresenta ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="4a953-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="4a953-1325">Chiave</span><span class="sxs-lookup"><span data-stu-id="4a953-1325">Key</span></span> | <span data-ttu-id="4a953-1326">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-1326">Description</span></span> | <span data-ttu-id="4a953-1327">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a953-1327">Type</span></span> | <span data-ttu-id="4a953-1328">Valore valido</span><span class="sxs-lookup"><span data-stu-id="4a953-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="4a953-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="4a953-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="4a953-1330">numero di Hello di iterazioni esegue modello hello è rappresentato dalle hello complessiva di calcolo tempo e hello accuratezza del modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="4a953-1331">maggiore hello Hello, una maggiore accuratezza hello che verrà creato, ma hello calcolo richiederà più tempo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="4a953-1332">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1332">Integer</span></span> |<span data-ttu-id="4a953-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="4a953-1333">10-50</span></span> |
| <span data-ttu-id="4a953-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="4a953-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="4a953-1335">numero di Hello di dimensioni riguarda il numero di toohello del modello di hello 'funzionalità' tenterà toofind all'interno dei dati.</span><span class="sxs-lookup"><span data-stu-id="4a953-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="4a953-1336">Aumentare il numero di hello dimensioni consente una migliore ottimizzazione dei risultati di hello in cluster più piccoli.</span><span class="sxs-lookup"><span data-stu-id="4a953-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="4a953-1337">Tuttavia, troppe dimensioni impedirà modello hello di individuazione delle correlazioni tra gli elementi.</span><span class="sxs-lookup"><span data-stu-id="4a953-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="4a953-1338">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1338">Integer</span></span> |<span data-ttu-id="4a953-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="4a953-1339">10-40</span></span> |
| <span data-ttu-id="4a953-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="4a953-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="4a953-1341">Definisce hello elemento limite inferiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="4a953-1342">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1342">See usage condenser above.</span></span> |<span data-ttu-id="4a953-1343">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1343">Integer</span></span> |<span data-ttu-id="4a953-1344">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="4a953-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="4a953-1346">Definisce hello elemento limite superiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="4a953-1347">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1347">See usage condenser above.</span></span> |<span data-ttu-id="4a953-1348">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1348">Integer</span></span> |<span data-ttu-id="4a953-1349">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="4a953-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="4a953-1351">Definisce hello utente limite inferiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="4a953-1352">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1352">See usage condenser above.</span></span> |<span data-ttu-id="4a953-1353">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1353">Integer</span></span> |<span data-ttu-id="4a953-1354">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="4a953-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="4a953-1356">Definisce hello utente limite superiore condensatore hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="4a953-1357">Vedere la sezione precedente relativa alla concentrazione dei dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1357">See usage condenser above.</span></span> |<span data-ttu-id="4a953-1358">Integer</span><span class="sxs-lookup"><span data-stu-id="4a953-1358">Integer</span></span> |<span data-ttu-id="4a953-1359">2 o più (0 disabilita la concentrazione)</span><span class="sxs-lookup"><span data-stu-id="4a953-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="4a953-1360">Description</span><span class="sxs-lookup"><span data-stu-id="4a953-1360">Description</span></span> |<span data-ttu-id="4a953-1361">Descrizione della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1361">Build description.</span></span> |<span data-ttu-id="4a953-1362">String</span><span class="sxs-lookup"><span data-stu-id="4a953-1362">String</span></span> |<span data-ttu-id="4a953-1363">Qualsiasi testo, con un massimo di 512 caratteri</span><span class="sxs-lookup"><span data-stu-id="4a953-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="4a953-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="4a953-1364">EnableModelingInsights</span></span> |<span data-ttu-id="4a953-1365">Consente di metriche toocompute nel modello di raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="4a953-1366">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1366">Boolean</span></span> |<span data-ttu-id="4a953-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="4a953-1367">True/False</span></span> |
| <span data-ttu-id="4a953-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="4a953-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="4a953-1369">Indica se è possano utilizzare le funzionalità nel modello di raccomandazione hello tooenhance ordine.</span><span class="sxs-lookup"><span data-stu-id="4a953-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="4a953-1370">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1370">Boolean</span></span> |<span data-ttu-id="4a953-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="4a953-1371">True/False</span></span> |
| <span data-ttu-id="4a953-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="4a953-1372">ModelingFeatureList</span></span> |<span data-ttu-id="4a953-1373">Elenco delimitato da virgole di toobe di nomi di funzionalità utilizzate nella compilazione di raccomandazione hello, nella raccomandazione di hello tooenhance ordine.</span><span class="sxs-lookup"><span data-stu-id="4a953-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="4a953-1374">String</span><span class="sxs-lookup"><span data-stu-id="4a953-1374">String</span></span> |<span data-ttu-id="4a953-1375">Nomi delle funzionalità, i caratteri too512</span><span class="sxs-lookup"><span data-stu-id="4a953-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="4a953-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="4a953-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="4a953-1377">Indica se raccomandazione hello deve eseguire anche il push agli elementi ignoti tramite somiglianza funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="4a953-1378">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1378">Boolean</span></span> |<span data-ttu-id="4a953-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="4a953-1379">True/False</span></span> |
| <span data-ttu-id="4a953-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="4a953-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="4a953-1381">Indica se le funzionalità possono essere usate nella motivazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="4a953-1382">Boolean</span><span class="sxs-lookup"><span data-stu-id="4a953-1382">Boolean</span></span> |<span data-ttu-id="4a953-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="4a953-1383">True/False</span></span> |
| <span data-ttu-id="4a953-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="4a953-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="4a953-1385">Elenco delimitato da virgole di funzionalità nomi toobe utilizzato per ragionamento frasi (ad esempio, descrizioni di raccomandazione).</span><span class="sxs-lookup"><span data-stu-id="4a953-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="4a953-1386">String</span><span class="sxs-lookup"><span data-stu-id="4a953-1386">String</span></span> |<span data-ttu-id="4a953-1387">Nomi delle funzionalità, i caratteri too512</span><span class="sxs-lookup"><span data-stu-id="4a953-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="4a953-1388">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1388">OData XML</span></span>

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

## <a name="12-recommendation"></a><span data-ttu-id="4a953-1389">12. Raccomandazione</span><span class="sxs-lookup"><span data-stu-id="4a953-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="4a953-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-1390">12.1.</span></span> <span data-ttu-id="4a953-1391">Ottenere le raccomandazioni degli elementi (per la compilazione attiva)</span><span class="sxs-lookup"><span data-stu-id="4a953-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="4a953-1392">Consigli di compilazione attiva di hello di tipo "Raccomandazione" o "Delle rate delle imposte" in base a un elenco di elementi i valori di inizializzazione (input).</span><span class="sxs-lookup"><span data-stu-id="4a953-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="4a953-1393">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1393">HTTP Method</span></span> | <span data-ttu-id="4a953-1394">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1395">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1396">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1397">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1397">Parameter Name</span></span> | <span data-ttu-id="4a953-1398">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1399">modelId</span></span> |<span data-ttu-id="4a953-1400">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="4a953-1401">itemIds</span></span> |<span data-ttu-id="4a953-1402">Elenco delimitato da virgole di hello elementi toorecommend per.</span><span class="sxs-lookup"><span data-stu-id="4a953-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="4a953-1403">Se la compilazione attiva hello è di tipo delle rate delle imposte, quindi è possibile inviare un solo elemento.</span><span class="sxs-lookup"><span data-stu-id="4a953-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="4a953-1404">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="4a953-1404">Max length: 1024</span></span> |
| <span data-ttu-id="4a953-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4a953-1405">numberOfResults</span></span> |<span data-ttu-id="4a953-1406">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4a953-1406">Number of required results</span></span> <br> <span data-ttu-id="4a953-1407">Massimo: 150</span><span class="sxs-lookup"><span data-stu-id="4a953-1407">Max: 150</span></span> |
| <span data-ttu-id="4a953-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4a953-1408">includeMetatadata</span></span> |<span data-ttu-id="4a953-1409">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4a953-1409">Future use, always false</span></span> |
| <span data-ttu-id="4a953-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1410">apiVersion</span></span> |<span data-ttu-id="4a953-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1411">1.0</span></span> |

<span data-ttu-id="4a953-1412">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1412">**Response:**</span></span>

<span data-ttu-id="4a953-1413">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1414">risposta Hello include una voce per ogni elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="4a953-1415">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1416">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1417">`Feed\entry\content\properties\Name`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1418">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4a953-1419">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="4a953-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="4a953-1420">risposta di esempio Hello riportata di seguito include 10 elementi consigliati.</span><span class="sxs-lookup"><span data-stu-id="4a953-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="4a953-1421">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1421">OData XML</span></span>

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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="4a953-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-1422">12.2.</span></span> <span data-ttu-id="4a953-1423">Ottenere le raccomandazioni degli elementi (di una compilazione specifica)</span><span class="sxs-lookup"><span data-stu-id="4a953-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="4a953-1424">Ottiene raccomandazioni di una compilazione specifica di tipo "Recommendation" o "Fbt".</span><span class="sxs-lookup"><span data-stu-id="4a953-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="4a953-1425">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1425">HTTP Method</span></span> | <span data-ttu-id="4a953-1426">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1427">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1428">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1429">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1429">Parameter Name</span></span> | <span data-ttu-id="4a953-1430">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1431">modelId</span></span> |<span data-ttu-id="4a953-1432">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="4a953-1433">itemIds</span></span> |<span data-ttu-id="4a953-1434">Elenco delimitato da virgole di hello elementi toorecommend per.</span><span class="sxs-lookup"><span data-stu-id="4a953-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="4a953-1435">Se la compilazione attiva hello è di tipo delle rate delle imposte, quindi è possibile inviare un solo elemento.</span><span class="sxs-lookup"><span data-stu-id="4a953-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="4a953-1436">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="4a953-1436">Max length: 1024</span></span> |
| <span data-ttu-id="4a953-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4a953-1437">numberOfResults</span></span> |<span data-ttu-id="4a953-1438">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4a953-1438">Number of required results</span></span> <br> <span data-ttu-id="4a953-1439">Massimo: 150</span><span class="sxs-lookup"><span data-stu-id="4a953-1439">Max: 150</span></span> |
| <span data-ttu-id="4a953-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4a953-1440">includeMetatadata</span></span> |<span data-ttu-id="4a953-1441">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4a953-1441">Future use, always false</span></span> |
| <span data-ttu-id="4a953-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-1442">buildId</span></span> |<span data-ttu-id="4a953-1443">Hello toouse id per la richiesta di indicazione di compilazione</span><span class="sxs-lookup"><span data-stu-id="4a953-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="4a953-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1444">apiVersion</span></span> |<span data-ttu-id="4a953-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1445">1.0</span></span> |

<span data-ttu-id="4a953-1446">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1446">**Response:**</span></span>

<span data-ttu-id="4a953-1447">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1448">risposta Hello include una voce per ogni elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="4a953-1449">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1450">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1451">`Feed\entry\content\properties\Name`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1452">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4a953-1453">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="4a953-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="4a953-1454">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="4a953-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-1455">12.3.</span></span> <span data-ttu-id="4a953-1456">Ottenere le raccomandazioni FBT (per la compilazione attiva)</span><span class="sxs-lookup"><span data-stu-id="4a953-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="4a953-1457">Consigli di compilazione attiva di hello di tipo "Delle rate delle imposte" basato su un elemento del valore di inizializzazione (input).</span><span class="sxs-lookup"><span data-stu-id="4a953-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="4a953-1458">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1458">HTTP Method</span></span> | <span data-ttu-id="4a953-1459">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1460">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1461">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1462">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1462">Parameter Name</span></span> | <span data-ttu-id="4a953-1463">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1464">modelId</span></span> |<span data-ttu-id="4a953-1465">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="4a953-1466">itemId</span></span> |<span data-ttu-id="4a953-1467">Elemento toorecommend per.</span><span class="sxs-lookup"><span data-stu-id="4a953-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="4a953-1468">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="4a953-1468">Max length: 1024</span></span> |
| <span data-ttu-id="4a953-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4a953-1469">numberOfResults</span></span> |<span data-ttu-id="4a953-1470">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4a953-1470">Number of required results</span></span> <br><span data-ttu-id="4a953-1471">Massimo: 150</span><span class="sxs-lookup"><span data-stu-id="4a953-1471">Max: 150</span></span> |
| <span data-ttu-id="4a953-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="4a953-1472">minimalScore</span></span> |<span data-ttu-id="4a953-1473">Punteggio minimo che un set di frequente deve disporre in ordine toobe incluso in hello restituito risultati</span><span class="sxs-lookup"><span data-stu-id="4a953-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="4a953-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4a953-1474">includeMetatadata</span></span> |<span data-ttu-id="4a953-1475">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4a953-1475">Future use, always false</span></span> |
| <span data-ttu-id="4a953-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1476">apiVersion</span></span> |<span data-ttu-id="4a953-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1477">1.0</span></span> |

<span data-ttu-id="4a953-1478">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1478">**Response:**</span></span>

<span data-ttu-id="4a953-1479">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1480">risposta Hello include una voce per ogni set di elementi raccomandati (un set di elementi che sono in genere acquistati insieme a elemento di valore di inizializzazione/input hello).</span><span class="sxs-lookup"><span data-stu-id="4a953-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="4a953-1481">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1482">`Feed\entry\content\properties\Id1` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1483">`Feed\entry\content\properties\Name1`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1484">`Feed\entry\content\properties\Id2` : ID 2° elemento consigliato (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="4a953-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="4a953-1485">`Feed\entry\content\properties\Name2`-Nome dell'elemento 2 hello (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="4a953-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="4a953-1486">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4a953-1487">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="4a953-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="4a953-1488">risposta di esempio Hello riportata di seguito include 3 set di elementi raccomandati.</span><span class="sxs-lookup"><span data-stu-id="4a953-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="4a953-1489">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1489">OData XML</span></span>

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

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="4a953-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="4a953-1490">12.4.</span></span> <span data-ttu-id="4a953-1491">Ottenere le raccomandazioni FBT (di una compilazione specifica)</span><span class="sxs-lookup"><span data-stu-id="4a953-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="4a953-1492">Ottenere le raccomandazioni di una compilazione specifica di tipo "Fbt".</span><span class="sxs-lookup"><span data-stu-id="4a953-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="4a953-1493">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1493">HTTP Method</span></span> | <span data-ttu-id="4a953-1494">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1495">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1496">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1497">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1497">Parameter Name</span></span> | <span data-ttu-id="4a953-1498">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1499">modelId</span></span> |<span data-ttu-id="4a953-1500">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="4a953-1501">itemId</span></span> |<span data-ttu-id="4a953-1502">Elemento toorecommend per.</span><span class="sxs-lookup"><span data-stu-id="4a953-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="4a953-1503">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="4a953-1503">Max length: 1024</span></span> |
| <span data-ttu-id="4a953-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4a953-1504">numberOfResults</span></span> |<span data-ttu-id="4a953-1505">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4a953-1505">Number of required results</span></span> <br><span data-ttu-id="4a953-1506">Massimo: 150</span><span class="sxs-lookup"><span data-stu-id="4a953-1506">Max: 150</span></span> |
| <span data-ttu-id="4a953-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="4a953-1507">minimalScore</span></span> |<span data-ttu-id="4a953-1508">Punteggio minimo che un set di frequente deve disporre in ordine toobe incluso in hello restituito risultati</span><span class="sxs-lookup"><span data-stu-id="4a953-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="4a953-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4a953-1509">includeMetatadata</span></span> |<span data-ttu-id="4a953-1510">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4a953-1510">Future use, always false</span></span> |
| <span data-ttu-id="4a953-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-1511">buildId</span></span> |<span data-ttu-id="4a953-1512">Hello toouse id per la richiesta di indicazione di compilazione</span><span class="sxs-lookup"><span data-stu-id="4a953-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="4a953-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1513">apiVersion</span></span> |<span data-ttu-id="4a953-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1514">1.0</span></span> |

<span data-ttu-id="4a953-1515">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1515">**Response:**</span></span>

<span data-ttu-id="4a953-1516">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1517">risposta Hello include una voce per ogni set di elementi raccomandati (un set di elementi che sono in genere acquistati insieme a elemento di valore di inizializzazione/input hello).</span><span class="sxs-lookup"><span data-stu-id="4a953-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="4a953-1518">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1519">`Feed\entry\content\properties\Id1` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1520">`Feed\entry\content\properties\Name1`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1521">`Feed\entry\content\properties\Id2` : ID 2° elemento consigliato (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="4a953-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="4a953-1522">`Feed\entry\content\properties\Name2`-Nome dell'elemento 2 hello (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="4a953-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="4a953-1523">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4a953-1524">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="4a953-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="4a953-1525">Vedere un esempio di risposta nella sezione 12.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="4a953-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="4a953-1526">12.5.</span></span> <span data-ttu-id="4a953-1527">Ottenere le raccomandazioni utente (per la compilazione attiva)</span><span class="sxs-lookup"><span data-stu-id="4a953-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="4a953-1528">Ottenere le raccomandazioni utente di una compilazione di tipo "Recommendation" contrassegnata come compilazione attiva.</span><span class="sxs-lookup"><span data-stu-id="4a953-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="4a953-1529">Hello API restituirà un elenco di elementi stimati in base toohello la cronologia di utilizzo dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="4a953-1530">Note:</span><span class="sxs-lookup"><span data-stu-id="4a953-1530">Notes:</span></span> 

1. <span data-ttu-id="4a953-1531">Non esiste alcuna raccomandazione utente per la compilazione FBT.</span><span class="sxs-lookup"><span data-stu-id="4a953-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="4a953-1532">Se compila hello active è delle rate delle imposte, questo metodo verrà restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="4a953-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="4a953-1533">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1533">HTTP Method</span></span> | <span data-ttu-id="4a953-1534">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1535">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1536">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1537">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1537">Parameter Name</span></span> | <span data-ttu-id="4a953-1538">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1539">modelId</span></span> |<span data-ttu-id="4a953-1540">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1541">userId</span><span class="sxs-lookup"><span data-stu-id="4a953-1541">userId</span></span> |<span data-ttu-id="4a953-1542">Identificatore univoco dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="4a953-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4a953-1543">numberOfResults</span></span> |<span data-ttu-id="4a953-1544">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4a953-1544">Number of required results</span></span> |
| <span data-ttu-id="4a953-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4a953-1545">includeMetatadata</span></span> |<span data-ttu-id="4a953-1546">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4a953-1546">Future use, always false</span></span> |
| <span data-ttu-id="4a953-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1547">apiVersion</span></span> |<span data-ttu-id="4a953-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1548">1.0</span></span> |

<span data-ttu-id="4a953-1549">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1549">**Response:**</span></span>

<span data-ttu-id="4a953-1550">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1551">risposta Hello include una voce per ogni elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="4a953-1552">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1553">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1554">`Feed\entry\content\properties\Name`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1555">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4a953-1556">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="4a953-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="4a953-1557">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="4a953-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="4a953-1558">12.6.</span></span> <span data-ttu-id="4a953-1559">Ottenere le raccomandazioni utente con l'elenco di elementi (per la compilazione attiva)</span><span class="sxs-lookup"><span data-stu-id="4a953-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="4a953-1560">Ottenere raccomandazioni utente di una compilazione di tipo "Recommendation" contrassegnata come compilazione attiva con un elenco aggiuntivo di elementi</span><span class="sxs-lookup"><span data-stu-id="4a953-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="4a953-1561">Hello API restituirà un elenco di elementi stimati in base toohello la cronologia di utilizzo di utente hello e gli altri elementi forniti hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="4a953-1562">Note:</span><span class="sxs-lookup"><span data-stu-id="4a953-1562">Notes:</span></span> 

1. <span data-ttu-id="4a953-1563">Non esiste alcuna raccomandazione utente per la compilazione FBT.</span><span class="sxs-lookup"><span data-stu-id="4a953-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="4a953-1564">Se compila hello active è delle rate delle imposte, questo metodo verrà restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="4a953-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="4a953-1565">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1565">HTTP Method</span></span> | <span data-ttu-id="4a953-1566">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1567">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1568">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1569">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1569">Parameter Name</span></span> | <span data-ttu-id="4a953-1570">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1571">modelId</span></span> |<span data-ttu-id="4a953-1572">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1573">userId</span><span class="sxs-lookup"><span data-stu-id="4a953-1573">userId</span></span> |<span data-ttu-id="4a953-1574">Identificatore univoco dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="4a953-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="4a953-1575">itemsIds</span></span> |<span data-ttu-id="4a953-1576">Elenco delimitato da virgole di hello elementi toorecommend per.</span><span class="sxs-lookup"><span data-stu-id="4a953-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="4a953-1577">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="4a953-1577">Max length: 1024</span></span> |
| <span data-ttu-id="4a953-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4a953-1578">numberOfResults</span></span> |<span data-ttu-id="4a953-1579">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4a953-1579">Number of required results</span></span> |
| <span data-ttu-id="4a953-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4a953-1580">includeMetatadata</span></span> |<span data-ttu-id="4a953-1581">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4a953-1581">Future use, always false</span></span> |
| <span data-ttu-id="4a953-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1582">apiVersion</span></span> |<span data-ttu-id="4a953-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1583">1.0</span></span> |

<span data-ttu-id="4a953-1584">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1584">**Response:**</span></span>

<span data-ttu-id="4a953-1585">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1586">risposta Hello include una voce per ogni elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="4a953-1587">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1588">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1589">`Feed\entry\content\properties\Name`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1590">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4a953-1591">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="4a953-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="4a953-1592">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="4a953-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="4a953-1593">12.7.</span></span> <span data-ttu-id="4a953-1594">Ottenere le raccomandazioni utente (di una compilazione specifica)</span><span class="sxs-lookup"><span data-stu-id="4a953-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="4a953-1595">Ottenere le raccomandazioni utente di una compilazione specifica di tipo "Recommendation".</span><span class="sxs-lookup"><span data-stu-id="4a953-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="4a953-1596">Hello API restituirà un elenco di elementi stimati in base toohello la cronologia di utilizzo dell'utente hello (utilizzato in una compilazione specifica hello).</span><span class="sxs-lookup"><span data-stu-id="4a953-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="4a953-1597">Nota: non esiste alcuna raccomandazione utente per la compilazione FBT.</span><span class="sxs-lookup"><span data-stu-id="4a953-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="4a953-1598">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1598">HTTP Method</span></span> | <span data-ttu-id="4a953-1599">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1600">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1601">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1602">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1602">Parameter Name</span></span> | <span data-ttu-id="4a953-1603">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1604">modelId</span></span> |<span data-ttu-id="4a953-1605">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1606">userId</span><span class="sxs-lookup"><span data-stu-id="4a953-1606">userId</span></span> |<span data-ttu-id="4a953-1607">Identificatore univoco dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="4a953-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4a953-1608">numberOfResults</span></span> |<span data-ttu-id="4a953-1609">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4a953-1609">Number of required results</span></span> |
| <span data-ttu-id="4a953-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4a953-1610">includeMetatadata</span></span> |<span data-ttu-id="4a953-1611">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4a953-1611">Future use, always false</span></span> |
| <span data-ttu-id="4a953-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-1612">buildId</span></span> |<span data-ttu-id="4a953-1613">Hello toouse id per la richiesta di indicazione di compilazione</span><span class="sxs-lookup"><span data-stu-id="4a953-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="4a953-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1614">apiVersion</span></span> |<span data-ttu-id="4a953-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1615">1.0</span></span> |

<span data-ttu-id="4a953-1616">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1616">**Response:**</span></span>

<span data-ttu-id="4a953-1617">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1618">risposta Hello include una voce per ogni elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="4a953-1619">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1620">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1621">`Feed\entry\content\properties\Name`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1622">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4a953-1623">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="4a953-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="4a953-1624">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="4a953-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="4a953-1625">12.8.</span></span> <span data-ttu-id="4a953-1626">Ottenere le raccomandazioni utente con l'elenco di elementi (di una compilazione specifica)</span><span class="sxs-lookup"><span data-stu-id="4a953-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="4a953-1627">Ottenere indicazioni utente di una compilazione specifica del tipo "Indicazione" ed elenco hello di elementi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="4a953-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="4a953-1628">Hello API restituirà un elenco di elementi stimati in base toohello la cronologia di utilizzo dell'utente hello ed elenco aggiuntivo di hello di elementi.</span><span class="sxs-lookup"><span data-stu-id="4a953-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="4a953-1629">Nota: non esiste alcuna raccomandazione utente per la compilazione FBT.</span><span class="sxs-lookup"><span data-stu-id="4a953-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="4a953-1630">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1630">HTTP Method</span></span> | <span data-ttu-id="4a953-1631">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1632">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1633">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1634">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1634">Parameter Name</span></span> | <span data-ttu-id="4a953-1635">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1636">modelId</span></span> |<span data-ttu-id="4a953-1637">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1638">userId</span><span class="sxs-lookup"><span data-stu-id="4a953-1638">userId</span></span> |<span data-ttu-id="4a953-1639">Identificatore univoco dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="4a953-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="4a953-1640">itemIds</span></span> |<span data-ttu-id="4a953-1641">Elenco delimitato da virgole di hello elementi toorecommend per.</span><span class="sxs-lookup"><span data-stu-id="4a953-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="4a953-1642">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="4a953-1642">Max length: 1024</span></span> |
| <span data-ttu-id="4a953-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4a953-1643">numberOfResults</span></span> |<span data-ttu-id="4a953-1644">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4a953-1644">Number of required results</span></span> |
| <span data-ttu-id="4a953-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4a953-1645">includeMetatadata</span></span> |<span data-ttu-id="4a953-1646">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4a953-1646">Future use, always false</span></span> |
| <span data-ttu-id="4a953-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-1647">buildId</span></span> |<span data-ttu-id="4a953-1648">Hello toouse id per la richiesta di indicazione di compilazione</span><span class="sxs-lookup"><span data-stu-id="4a953-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="4a953-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1649">apiVersion</span></span> |<span data-ttu-id="4a953-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1650">1.0</span></span> |

<span data-ttu-id="4a953-1651">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1651">**Response:**</span></span>

<span data-ttu-id="4a953-1652">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1653">risposta Hello include una voce per ogni elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="4a953-1654">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1655">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1656">`Feed\entry\content\properties\Name`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1657">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4a953-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4a953-1658">`Feed\entry\content\properties\Reasoning` : motivazione della raccomandazione (ad esempio, spiegazioni delle raccomandazioni).</span><span class="sxs-lookup"><span data-stu-id="4a953-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="4a953-1659">Vedere un esempio di risposta nella sezione 12.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="4a953-1660">13. Cronologia utilizzo utente</span><span class="sxs-lookup"><span data-stu-id="4a953-1660">13. User Usage History</span></span>
<span data-ttu-id="4a953-1661">Una volta che è stato compilato un modello di raccomandazione sistema hello consentirà tooretrieve hello cronologia dell'utente (utente specifico di elementi associati tooa) utilizzata per la compilazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="4a953-1662">Questa API consente cronologia utenti di hello tooretrieve</span><span class="sxs-lookup"><span data-stu-id="4a953-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="4a953-1663">Nota: hello utente cronologia è attualmente disponibile solo per le compilazioni di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="4a953-1664">13.1 Recuperare la cronologia utente</span><span class="sxs-lookup"><span data-stu-id="4a953-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="4a953-1665">Recuperare hello elenco dell'elemento utilizzata in hello active compilazione o compilazione hello specificato per hello l'id utente specificato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="4a953-1666">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1666">HTTP Method</span></span> | <span data-ttu-id="4a953-1667">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1668">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1668">GET</span></span> |<span data-ttu-id="4a953-1669">Ottenere la cronologia di hello utente per la compilazione active hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="4a953-1670">Ottenere la cronologia di utente hello per hello fornito build`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="4a953-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="4a953-1671">Esempio:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="4a953-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="4a953-1672">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1672">Parameter Name</span></span> | <span data-ttu-id="4a953-1673">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1674">modelId</span></span> |<span data-ttu-id="4a953-1675">Identificatore univoco di Hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="4a953-1676">userId</span><span class="sxs-lookup"><span data-stu-id="4a953-1676">userId</span></span> |<span data-ttu-id="4a953-1677">Identificatore univoco dell'utente hello di Hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="4a953-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="4a953-1678">buildId</span></span> |<span data-ttu-id="4a953-1679">parametro facoltativo, consentire la compilazione cronologia utenti hello deve essere fetch tooindicate</span><span class="sxs-lookup"><span data-stu-id="4a953-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="4a953-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1680">apiVersion</span></span> |<span data-ttu-id="4a953-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1681">1.0</span></span> |

<span data-ttu-id="4a953-1682">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1682">**Response:**</span></span>

<span data-ttu-id="4a953-1683">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1684">risposta Hello include una voce per ogni elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="4a953-1685">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a953-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="4a953-1686">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4a953-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4a953-1687">`Feed\entry\content\properties\Name`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="4a953-1688">`Feed\entry\content\properties\Rating` : N/A.</span><span class="sxs-lookup"><span data-stu-id="4a953-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="4a953-1689">`Feed\entry\content\properties\Reasoning` : N/A.</span><span class="sxs-lookup"><span data-stu-id="4a953-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="4a953-1690">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1690">OData XML</span></span>

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

## <a name="14-notifications"></a><span data-ttu-id="4a953-1691">14. Notifiche</span><span class="sxs-lookup"><span data-stu-id="4a953-1691">14. Notifications</span></span>
<span data-ttu-id="4a953-1692">Azure Machine Learning indicazioni crea le notifiche quando si verificano gli errori persistenti nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="4a953-1693">Esistono 3 tipi di notifiche:</span><span class="sxs-lookup"><span data-stu-id="4a953-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="4a953-1694">Build failure: questa notifica viene attivata per ogni errore di compilazione.</span><span class="sxs-lookup"><span data-stu-id="4a953-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="4a953-1695">Acquisizione dei dati, l'elaborazione di errore - questa notifica viene attivata quando si dispone di più di 100 errori in hello ultimi 5 minuti in elaborazione hello degli eventi di utilizzo per ogni modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="4a953-1696">Errore di consumo di raccomandazione - questa notifica viene attivato quando si dispone di più di 100 errori in hello ultimi 5 minuti in elaborazione hello delle richieste di raccomandazione per ogni modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="4a953-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="4a953-1697">14.1.</span></span> <span data-ttu-id="4a953-1698">Ottenere notifiche</span><span class="sxs-lookup"><span data-stu-id="4a953-1698">Get Notifications</span></span>
<span data-ttu-id="4a953-1699">Recupera tutte le notifiche di hello per tutti i modelli o per un singolo modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="4a953-1700">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1700">HTTP Method</span></span> | <span data-ttu-id="4a953-1701">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1702">GET</span><span class="sxs-lookup"><span data-stu-id="4a953-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1703">Per ottenere tutte le notifiche relative a tutti i modelli:</span><span class="sxs-lookup"><span data-stu-id="4a953-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1704">Esempio per ottenere le notifiche relative a un modello specifico:</span><span class="sxs-lookup"><span data-stu-id="4a953-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="4a953-1705">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1705">Parameter Name</span></span> | <span data-ttu-id="4a953-1706">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1707">modelId</span></span> |<span data-ttu-id="4a953-1708">Parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="4a953-1708">Optional parameter.</span></span> <span data-ttu-id="4a953-1709">Se omesso, vengono restituite tutte le notifiche relative a tutti i modelli.</span><span class="sxs-lookup"><span data-stu-id="4a953-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="4a953-1710">Valore valido: identificatore univoco del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="4a953-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1711">apiVersion</span></span> |<span data-ttu-id="4a953-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-1713">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-1713">Request Body</span></span> |<span data-ttu-id="4a953-1714">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-1714">NONE</span></span> |

<span data-ttu-id="4a953-1715">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4a953-1715">**Response:**</span></span>

<span data-ttu-id="4a953-1716">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="4a953-1717">XML OData</span><span class="sxs-lookup"><span data-stu-id="4a953-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
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

### <a name="142-delete-model-notifications"></a><span data-ttu-id="4a953-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="4a953-1718">14.2.</span></span> <span data-ttu-id="4a953-1719">Eliminare le notifiche di modello</span><span class="sxs-lookup"><span data-stu-id="4a953-1719">Delete Model Notifications</span></span>
<span data-ttu-id="4a953-1720">Elimina tutte le notifiche di lettura relative a un modello.</span><span class="sxs-lookup"><span data-stu-id="4a953-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="4a953-1721">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1721">HTTP Method</span></span> | <span data-ttu-id="4a953-1722">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1723">DELETE</span><span class="sxs-lookup"><span data-stu-id="4a953-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4a953-1724">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a953-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1725">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1725">Parameter Name</span></span> | <span data-ttu-id="4a953-1726">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="4a953-1727">modelId</span></span> |<span data-ttu-id="4a953-1728">Identificatore univoco del modello di hello</span><span class="sxs-lookup"><span data-stu-id="4a953-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="4a953-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1729">apiVersion</span></span> |<span data-ttu-id="4a953-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-1731">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-1731">Request Body</span></span> |<span data-ttu-id="4a953-1732">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-1732">NONE</span></span> |

<span data-ttu-id="4a953-1733">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-1733">**Response**:</span></span>

<span data-ttu-id="4a953-1734">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="4a953-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="4a953-1735">14.3.</span></span> <span data-ttu-id="4a953-1736">Eliminare le notifiche utente</span><span class="sxs-lookup"><span data-stu-id="4a953-1736">Delete User Notifications</span></span>
<span data-ttu-id="4a953-1737">Elimina tutte le notifiche relative a tutti i modelli.</span><span class="sxs-lookup"><span data-stu-id="4a953-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="4a953-1738">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4a953-1738">HTTP Method</span></span> | <span data-ttu-id="4a953-1739">URI</span><span class="sxs-lookup"><span data-stu-id="4a953-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1740">DELETE</span><span class="sxs-lookup"><span data-stu-id="4a953-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="4a953-1741">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4a953-1741">Parameter Name</span></span> | <span data-ttu-id="4a953-1742">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4a953-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4a953-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4a953-1743">apiVersion</span></span> |<span data-ttu-id="4a953-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="4a953-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="4a953-1745">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4a953-1745">Request Body</span></span> |<span data-ttu-id="4a953-1746">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4a953-1746">NONE</span></span> |

<span data-ttu-id="4a953-1747">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4a953-1747">**Response**:</span></span>

<span data-ttu-id="4a953-1748">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4a953-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="4a953-1749">15. Note legali</span><span class="sxs-lookup"><span data-stu-id="4a953-1749">15. Legal</span></span>
<span data-ttu-id="4a953-1750">Questo documento viene fornito "così com'è".</span><span class="sxs-lookup"><span data-stu-id="4a953-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="4a953-1751">Le informazioni e le indicazioni riportate nel presente documento, inclusi URL e altri riferimenti a siti Web Internet, sono soggette a modifica senza preavviso.</span><span class="sxs-lookup"><span data-stu-id="4a953-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="4a953-1752">Alcuni esempi usati in questo documento vengono forniti a scopo puramente illustrativo e sono fittizi.</span><span class="sxs-lookup"><span data-stu-id="4a953-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="4a953-1753">Nessuna associazione reale o connessione è intenzionale o può essere desunta.</span><span class="sxs-lookup"><span data-stu-id="4a953-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="4a953-1754">Questo documento non offrono alcun diritto legale tooany proprietà intellettuale in qualsiasi prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4a953-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="4a953-1755">È possibile copiare e usare il presente documento per scopi interni e di riferimento.</span><span class="sxs-lookup"><span data-stu-id="4a953-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="4a953-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4a953-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="4a953-1757">Tutti i diritti sono riservati.</span><span class="sxs-lookup"><span data-stu-id="4a953-1757">All rights reserved.</span></span>

