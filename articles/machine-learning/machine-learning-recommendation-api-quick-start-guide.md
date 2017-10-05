---
title: 'Guida introduttiva: API Recommendations di Azure Machine Learning (versione 1) | Documentazione Microsoft'
description: Recommendations di Azure Machine Learning - Guida introduttiva
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="9c625-104">Guida introduttiva per l'API Recommendations di Machine Learning (versione 1)</span><span class="sxs-lookup"><span data-stu-id="9c625-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="9c625-105">È consigliabile iniziare usando l'[API Recommendations dei servizi cognitivi](https://www.microsoft.com/cognitive-services/recommendations-api) invece di questa versione.</span><span class="sxs-lookup"><span data-stu-id="9c625-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="9c625-106">Il Servizio cognitivo di Recommendations sostituirà questo servizio e verranno sviluppate nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9c625-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="9c625-107">Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.</span><span class="sxs-lookup"><span data-stu-id="9c625-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="9c625-108">Per altre informazioni, vedere [Migrating to the new Cognitive Service](http://aka.ms/recomigrate) (Migrazione al nuovo Servizio cognitivo).</span><span class="sxs-lookup"><span data-stu-id="9c625-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="9c625-109">Questo documento descrive come configurare il servizio o l'applicazione per l'uso di Recommendations di Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9c625-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="9c625-110">È possibile trovare ulteriori informazioni sull'API Recommendations in [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="9c625-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="9c625-111">Panoramica generale</span><span class="sxs-lookup"><span data-stu-id="9c625-111">General overview</span></span>
<span data-ttu-id="9c625-112">Per usare Recommendations di Azure Machine Learning, è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c625-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="9c625-113">Creare un modello: un modello è un contenitore per dati di utilizzo, dati del catalogo e modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="9c625-114">Importare dati del catalogo: un catalogo contiene informazioni sui metadati relativi agli elementi.</span><span class="sxs-lookup"><span data-stu-id="9c625-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="9c625-115">Importare i dati di utilizzo: i dati di utilizzo possono essere caricati usando uno o entrambi i modi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9c625-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="9c625-116">Caricando un file contenente i dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9c625-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="9c625-117">Inviando eventi di acquisizione dei dati.</span><span class="sxs-lookup"><span data-stu-id="9c625-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="9c625-118">In genere, si carica un file dei dati di utilizzo per poter creare un modello di raccomandazione iniziale (bootstrap) e usarlo finché il sistema non raccoglie abbastanza dati usando il formato di acquisizione dei dati.</span><span class="sxs-lookup"><span data-stu-id="9c625-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="9c625-119">Compilare un modello di raccomandazione: si tratta di un'operazione asincrona in cui il sistema di raccomandazione accetta tutti i dati di utilizzo e crea un modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="9c625-120">Questa operazione può richiedere diversi minuti o diverse ore a seconda delle dimensioni dei dati e dei parametri di configurazione della build.</span><span class="sxs-lookup"><span data-stu-id="9c625-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="9c625-121">Quando si attiva la compilazione, si ottiene un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="9c625-122">Usarlo per verificare se il processo di compilazione è terminato prima di iniziare a usare raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="9c625-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="9c625-123">Utilizzare le raccomandazioni: ottenere raccomandazioni per un elemento o un elenco di elementi specifico.</span><span class="sxs-lookup"><span data-stu-id="9c625-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="9c625-124">Tutti i passaggi precedenti vengono eseguiti tramite l'API Recommendations di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9c625-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="9c625-125">È possibile scaricare un'applicazione di esempio che implementa anche ognuna delle seguenti operazioni dalla [raccolta](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="9c625-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="9c625-126">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="9c625-126">Limitations</span></span>
* <span data-ttu-id="9c625-127">Il numero massimo di modelli per ogni sottoscrizione è 10.</span><span class="sxs-lookup"><span data-stu-id="9c625-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="9c625-128">Il numero massimo di elementi che possono essere inclusi nel catalogo è 100.000.</span><span class="sxs-lookup"><span data-stu-id="9c625-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="9c625-129">Il numero massimo di punti di utilizzo mantenuti è ~5.000.000.</span><span class="sxs-lookup"><span data-stu-id="9c625-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="9c625-130">I meno recenti saranno eliminati se ne vengono caricati o segnalati di nuovi.</span><span class="sxs-lookup"><span data-stu-id="9c625-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="9c625-131">La dimensione massima dei dati che è possibile inviare in POST, ad esempio l'importazione dei dati di catalogo o dei dati di utilizzo, è 200 MB.</span><span class="sxs-lookup"><span data-stu-id="9c625-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="9c625-132">Il numero di transazioni al secondo per la compilazione di un modello di raccomandazione non attivo è di ~2 TPS.</span><span class="sxs-lookup"><span data-stu-id="9c625-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="9c625-133">Un modello di raccomandazione attivo può includere un massimo di 20 TPS.</span><span class="sxs-lookup"><span data-stu-id="9c625-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="9c625-134">Integrazione</span><span class="sxs-lookup"><span data-stu-id="9c625-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="9c625-135">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="9c625-135">Authentication</span></span>
<span data-ttu-id="9c625-136">Microsoft Azure Marketplace supporta il metodo di autenticazione di base o OAuth.</span><span class="sxs-lookup"><span data-stu-id="9c625-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="9c625-137">È possibile trovare facilmente le chiavi dell'account, passando alle chiavi nel marketplace in [Impostazioni account](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="9c625-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="9c625-138">Autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="9c625-138">Basic Authentication</span></span>
<span data-ttu-id="9c625-139">Aggiungere l'intestazione dell'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="9c625-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="9c625-140">Convertire in Base64 (C#)</span><span class="sxs-lookup"><span data-stu-id="9c625-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="9c625-141">Convertire in Base64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="9c625-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="9c625-142">URI del servizio</span><span class="sxs-lookup"><span data-stu-id="9c625-142">Service URI</span></span>
<span data-ttu-id="9c625-143">L'URI radice del servizio per ogni API Recommendations di Azure Machine Learning è disponibile [qui](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="9c625-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="9c625-144">L'URI del servizio completo è espresso usando elementi della specifica OData.</span><span class="sxs-lookup"><span data-stu-id="9c625-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="9c625-145">Versione dell'API</span><span class="sxs-lookup"><span data-stu-id="9c625-145">API version</span></span>
<span data-ttu-id="9c625-146">Ogni chiamata API terminerà con un parametro di query denominato apiVersion che dovrà essere impostato su "1.0".</span><span class="sxs-lookup"><span data-stu-id="9c625-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="9c625-147">Distinzione tra maiuscole e minuscole negli ID</span><span class="sxs-lookup"><span data-stu-id="9c625-147">IDs are case-sensitive</span></span>
<span data-ttu-id="9c625-148">Gli ID restituiti da una delle API fanno distinzione tra maiuscole e minuscole e devono essere usati esattamente come sono, quando vengono passati come parametri nelle chiamate API successive.</span><span class="sxs-lookup"><span data-stu-id="9c625-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="9c625-149">Anche gli ID modello e gli ID catalogo, ad esempio, fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="9c625-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="9c625-150">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="9c625-150">Create a model</span></span>
<span data-ttu-id="9c625-151">Creazione di una richiesta "crea modello":</span><span class="sxs-lookup"><span data-stu-id="9c625-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="9c625-152">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="9c625-152">HTTP Method</span></span> | <span data-ttu-id="9c625-153">URI</span><span class="sxs-lookup"><span data-stu-id="9c625-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-154">POST</span><span class="sxs-lookup"><span data-stu-id="9c625-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9c625-155">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9c625-156">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="9c625-156">Parameter Name</span></span> | <span data-ttu-id="9c625-157">Valori validi</span><span class="sxs-lookup"><span data-stu-id="9c625-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-158">modelName</span><span class="sxs-lookup"><span data-stu-id="9c625-158">modelName</span></span> |<span data-ttu-id="9c625-159">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="9c625-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="9c625-160">Lunghezza massima: 20</span><span class="sxs-lookup"><span data-stu-id="9c625-160">Max length: 20</span></span> |
| <span data-ttu-id="9c625-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9c625-161">apiVersion</span></span> |<span data-ttu-id="9c625-162">1.0</span><span class="sxs-lookup"><span data-stu-id="9c625-162">1.0</span></span> |
|  | |
| <span data-ttu-id="9c625-163">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="9c625-163">Request Body</span></span> |<span data-ttu-id="9c625-164">Nessuno</span><span class="sxs-lookup"><span data-stu-id="9c625-164">NONE</span></span> |

<span data-ttu-id="9c625-165">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="9c625-165">**Response**:</span></span>

<span data-ttu-id="9c625-166">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9c625-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="9c625-167">`feed/entry/content/properties/id` : contiene l'ID modello.</span><span class="sxs-lookup"><span data-stu-id="9c625-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="9c625-168">Si noti che l'ID modello fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="9c625-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="9c625-169">XML OData</span><span class="sxs-lookup"><span data-stu-id="9c625-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="import-catalog-data"></a><span data-ttu-id="9c625-170">Importare i dati del catalogo</span><span class="sxs-lookup"><span data-stu-id="9c625-170">Import catalog data</span></span>
<span data-ttu-id="9c625-171">Se si caricano diversi file del catalogo nello stesso modello con diverse chiamate, verranno inseriti solo i nuovi elementi del catalogo.</span><span class="sxs-lookup"><span data-stu-id="9c625-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="9c625-172">Gli elementi esistenti manterranno i valori originali.</span><span class="sxs-lookup"><span data-stu-id="9c625-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="9c625-173">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="9c625-173">HTTP Method</span></span> | <span data-ttu-id="9c625-174">URI</span><span class="sxs-lookup"><span data-stu-id="9c625-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-175">POST</span><span class="sxs-lookup"><span data-stu-id="9c625-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9c625-176">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9c625-177">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="9c625-177">Parameter Name</span></span> | <span data-ttu-id="9c625-178">Valori validi</span><span class="sxs-lookup"><span data-stu-id="9c625-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-179">modelId</span><span class="sxs-lookup"><span data-stu-id="9c625-179">modelId</span></span> |<span data-ttu-id="9c625-180">Identificatore univoco del modello con distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="9c625-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9c625-181">filename</span><span class="sxs-lookup"><span data-stu-id="9c625-181">filename</span></span> |<span data-ttu-id="9c625-182">Identificatore testuale del catalogo.</span><span class="sxs-lookup"><span data-stu-id="9c625-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="9c625-183">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="9c625-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="9c625-184">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="9c625-184">Max length: 50</span></span> |
| <span data-ttu-id="9c625-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9c625-185">apiVersion</span></span> |<span data-ttu-id="9c625-186">1.0</span><span class="sxs-lookup"><span data-stu-id="9c625-186">1.0</span></span> |
|  | |
| <span data-ttu-id="9c625-187">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="9c625-187">Request Body</span></span> |<span data-ttu-id="9c625-188">Dati del catalogo.</span><span class="sxs-lookup"><span data-stu-id="9c625-188">Catalog data.</span></span> <span data-ttu-id="9c625-189">Formato:</span><span class="sxs-lookup"><span data-stu-id="9c625-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="9c625-190">Nome</span><span class="sxs-lookup"><span data-stu-id="9c625-190">Name</span></span></th><th><span data-ttu-id="9c625-191">Mandatory</span><span class="sxs-lookup"><span data-stu-id="9c625-191">Mandatory</span></span></th><th><span data-ttu-id="9c625-192">Tipo</span><span class="sxs-lookup"><span data-stu-id="9c625-192">Type</span></span></th><th><span data-ttu-id="9c625-193">Description</span><span class="sxs-lookup"><span data-stu-id="9c625-193">Description</span></span></th></tr><tr><td><span data-ttu-id="9c625-194">Item Id</span><span class="sxs-lookup"><span data-stu-id="9c625-194">Item Id</span></span></td><td><span data-ttu-id="9c625-195">Sì</span><span class="sxs-lookup"><span data-stu-id="9c625-195">Yes</span></span></td><td><span data-ttu-id="9c625-196">Alfanumerico, lunghezza massima: 50 caratteri</span><span class="sxs-lookup"><span data-stu-id="9c625-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="9c625-197">Identificatore univoco di un elemento</span><span class="sxs-lookup"><span data-stu-id="9c625-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="9c625-198">Item Name</span><span class="sxs-lookup"><span data-stu-id="9c625-198">Item Name</span></span></td><td><span data-ttu-id="9c625-199">Sì</span><span class="sxs-lookup"><span data-stu-id="9c625-199">Yes</span></span></td><td><span data-ttu-id="9c625-200">Alfanumerico, lunghezza massima: 255 caratteri</span><span class="sxs-lookup"><span data-stu-id="9c625-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="9c625-201">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="9c625-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="9c625-202">Item Category</span><span class="sxs-lookup"><span data-stu-id="9c625-202">Item Category</span></span></td><td><span data-ttu-id="9c625-203">Sì</span><span class="sxs-lookup"><span data-stu-id="9c625-203">Yes</span></span></td><td><span data-ttu-id="9c625-204">Alfanumerico, lunghezza massima: 255 caratteri</span><span class="sxs-lookup"><span data-stu-id="9c625-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="9c625-205">Categoria alla quale appartiene l'elemento, ad esempio libri di cucina, letteratura e così via</span><span class="sxs-lookup"><span data-stu-id="9c625-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="9c625-206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c625-206">Description</span></span></td><td><span data-ttu-id="9c625-207">No</span><span class="sxs-lookup"><span data-stu-id="9c625-207">No</span></span></td><td><span data-ttu-id="9c625-208">Alfanumerico, lunghezza massima: 4000 caratteri</span><span class="sxs-lookup"><span data-stu-id="9c625-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="9c625-209">Descrizione dell'elemento</span><span class="sxs-lookup"><span data-stu-id="9c625-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="9c625-210">La dimensione massima del file è di 200 MB.</span><span class="sxs-lookup"><span data-stu-id="9c625-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="9c625-211">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="9c625-212">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="9c625-212">**Response**:</span></span>

<span data-ttu-id="9c625-213">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9c625-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="9c625-214">`Feed\entry\content\properties\LineCount` : numero di righe accettate.</span><span class="sxs-lookup"><span data-stu-id="9c625-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="9c625-215">`Feed\entry\content\properties\ErrorCount` : numero di righe non inserite a causa di un errore.</span><span class="sxs-lookup"><span data-stu-id="9c625-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="9c625-216">XML OData</span><span class="sxs-lookup"><span data-stu-id="9c625-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="9c625-217">Importare i dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="9c625-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="9c625-218">Caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="9c625-218">Uploading a file</span></span>
<span data-ttu-id="9c625-219">Queste sezioni mostrano come caricare i dati di utilizzo tramite un file.</span><span class="sxs-lookup"><span data-stu-id="9c625-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="9c625-220">È possibile chiamare l'API più volte con i dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9c625-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="9c625-221">Tutti i dati di utilizzo verranno salvati per tutte le chiamate.</span><span class="sxs-lookup"><span data-stu-id="9c625-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="9c625-222">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="9c625-222">HTTP Method</span></span> | <span data-ttu-id="9c625-223">URI</span><span class="sxs-lookup"><span data-stu-id="9c625-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-224">POST</span><span class="sxs-lookup"><span data-stu-id="9c625-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9c625-225">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9c625-226">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="9c625-226">Parameter Name</span></span> | <span data-ttu-id="9c625-227">Valori validi</span><span class="sxs-lookup"><span data-stu-id="9c625-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-228">modelId</span><span class="sxs-lookup"><span data-stu-id="9c625-228">modelId</span></span> |<span data-ttu-id="9c625-229">Identificatore univoco del modello con distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="9c625-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9c625-230">filename</span><span class="sxs-lookup"><span data-stu-id="9c625-230">filename</span></span> |<span data-ttu-id="9c625-231">Identificatore testuale del catalogo.</span><span class="sxs-lookup"><span data-stu-id="9c625-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="9c625-232">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="9c625-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="9c625-233">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="9c625-233">Max length: 50</span></span> |
| <span data-ttu-id="9c625-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9c625-234">apiVersion</span></span> |<span data-ttu-id="9c625-235">1.0</span><span class="sxs-lookup"><span data-stu-id="9c625-235">1.0</span></span> |
|  | |
| <span data-ttu-id="9c625-236">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="9c625-236">Request Body</span></span> |<span data-ttu-id="9c625-237">Dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9c625-237">Usage data.</span></span> <span data-ttu-id="9c625-238">Formato:</span><span class="sxs-lookup"><span data-stu-id="9c625-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="9c625-239">Nome</span><span class="sxs-lookup"><span data-stu-id="9c625-239">Name</span></span></th><th><span data-ttu-id="9c625-240">Mandatory</span><span class="sxs-lookup"><span data-stu-id="9c625-240">Mandatory</span></span></th><th><span data-ttu-id="9c625-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="9c625-241">Type</span></span></th><th><span data-ttu-id="9c625-242">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c625-242">Description</span></span></th></tr><tr><td><span data-ttu-id="9c625-243">User Id</span><span class="sxs-lookup"><span data-stu-id="9c625-243">User Id</span></span></td><td><span data-ttu-id="9c625-244">Sì</span><span class="sxs-lookup"><span data-stu-id="9c625-244">Yes</span></span></td><td><span data-ttu-id="9c625-245">Alfanumerico</span><span class="sxs-lookup"><span data-stu-id="9c625-245">Alphanumeric</span></span></td><td><span data-ttu-id="9c625-246">Identificatore univoco di un utente</span><span class="sxs-lookup"><span data-stu-id="9c625-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="9c625-247">Item Id</span><span class="sxs-lookup"><span data-stu-id="9c625-247">Item Id</span></span></td><td><span data-ttu-id="9c625-248">Sì</span><span class="sxs-lookup"><span data-stu-id="9c625-248">Yes</span></span></td><td><span data-ttu-id="9c625-249">Alfanumerico, lunghezza massima: 50 caratteri</span><span class="sxs-lookup"><span data-stu-id="9c625-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="9c625-250">Identificatore univoco di un elemento</span><span class="sxs-lookup"><span data-stu-id="9c625-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="9c625-251">Time</span><span class="sxs-lookup"><span data-stu-id="9c625-251">Time</span></span></td><td><span data-ttu-id="9c625-252">No</span><span class="sxs-lookup"><span data-stu-id="9c625-252">No</span></span></td><td><span data-ttu-id="9c625-253">Data in formato: AAAA/MM/GGTHH:MM:SS (ad esempio 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="9c625-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="9c625-254">Ora dei dati</span><span class="sxs-lookup"><span data-stu-id="9c625-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="9c625-255">Evento</span><span class="sxs-lookup"><span data-stu-id="9c625-255">Event</span></span></td><td><span data-ttu-id="9c625-256">No, se fornito deve essere inserita anche la data</span><span class="sxs-lookup"><span data-stu-id="9c625-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="9c625-257">Uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c625-257">One of the following:</span></span><br><span data-ttu-id="9c625-258">• Click</span><span class="sxs-lookup"><span data-stu-id="9c625-258">• Click</span></span><br><span data-ttu-id="9c625-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="9c625-259">• RecommendationClick</span></span><br><span data-ttu-id="9c625-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="9c625-260">•    AddShopCart</span></span><br><span data-ttu-id="9c625-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="9c625-261">• RemoveShopCart</span></span><br><span data-ttu-id="9c625-262">• Acquisto</span><span class="sxs-lookup"><span data-stu-id="9c625-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="9c625-263">La dimensione massima del file è di 200 MB.</span><span class="sxs-lookup"><span data-stu-id="9c625-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="9c625-264">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="9c625-265">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="9c625-265">**Response**:</span></span>

<span data-ttu-id="9c625-266">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9c625-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="9c625-267">`Feed\entry\content\properties\LineCount` : numero di righe accettate.</span><span class="sxs-lookup"><span data-stu-id="9c625-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="9c625-268">`Feed\entry\content\properties\ErrorCount` : numero di righe non inserite a causa di un errore.</span><span class="sxs-lookup"><span data-stu-id="9c625-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="9c625-269">`Feed\entry\content\properties\FileId` : identificatore del file.</span><span class="sxs-lookup"><span data-stu-id="9c625-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="9c625-270">XML OData</span><span class="sxs-lookup"><span data-stu-id="9c625-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="9c625-271">Uso dell'acquisizione dei dati</span><span class="sxs-lookup"><span data-stu-id="9c625-271">Using data acquisition</span></span>
<span data-ttu-id="9c625-272">Questa sezione illustra come inviare eventi in tempo reale a Recommendations di Azure Machine Learning, in genere dal sito Web.</span><span class="sxs-lookup"><span data-stu-id="9c625-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="9c625-273">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="9c625-273">HTTP Method</span></span> | <span data-ttu-id="9c625-274">URI</span><span class="sxs-lookup"><span data-stu-id="9c625-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-275">POST</span><span class="sxs-lookup"><span data-stu-id="9c625-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9c625-276">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="9c625-276">Parameter Name</span></span> | <span data-ttu-id="9c625-277">Valori validi</span><span class="sxs-lookup"><span data-stu-id="9c625-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9c625-278">apiVersion</span></span> |<span data-ttu-id="9c625-279">1.0</span><span class="sxs-lookup"><span data-stu-id="9c625-279">1.0</span></span> |
|  | |
| <span data-ttu-id="9c625-280">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="9c625-280">Request body</span></span> |<span data-ttu-id="9c625-281">Immissione di dati evento per ogni evento da inviare.</span><span class="sxs-lookup"><span data-stu-id="9c625-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="9c625-282">Per lo stesso utente o la stessa sessione del browser si dovrà inviare lo stesso ID nel campo SessionId.</span><span class="sxs-lookup"><span data-stu-id="9c625-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="9c625-283">Vedere l'esempio di corpo dell'evento di seguito.</span><span class="sxs-lookup"><span data-stu-id="9c625-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="9c625-284">Esempio di evento "Click":</span><span class="sxs-lookup"><span data-stu-id="9c625-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="9c625-285">Esempio di evento "RecommendationClick":</span><span class="sxs-lookup"><span data-stu-id="9c625-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="9c625-286">Esempio di evento "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="9c625-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="9c625-287">Esempio di evento "RemoveShopCart":</span><span class="sxs-lookup"><span data-stu-id="9c625-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="9c625-288">Esempio di evento "Purchase":</span><span class="sxs-lookup"><span data-stu-id="9c625-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="9c625-289">Esempio di invio di due eventi, "Click" e "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="9c625-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="9c625-290">**Risposta**: Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9c625-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="9c625-291">Compilare un modello di raccomandazione</span><span class="sxs-lookup"><span data-stu-id="9c625-291">Build a recommendation model</span></span>
| <span data-ttu-id="9c625-292">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="9c625-292">HTTP Method</span></span> | <span data-ttu-id="9c625-293">URI</span><span class="sxs-lookup"><span data-stu-id="9c625-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-294">POST</span><span class="sxs-lookup"><span data-stu-id="9c625-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9c625-295">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9c625-296">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="9c625-296">Parameter Name</span></span> | <span data-ttu-id="9c625-297">Valori validi</span><span class="sxs-lookup"><span data-stu-id="9c625-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-298">modelId</span><span class="sxs-lookup"><span data-stu-id="9c625-298">modelId</span></span> |<span data-ttu-id="9c625-299">Identificatore univoco del modello con distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="9c625-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9c625-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="9c625-300">userDescription</span></span> |<span data-ttu-id="9c625-301">Identificatore testuale del catalogo.</span><span class="sxs-lookup"><span data-stu-id="9c625-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="9c625-302">Tenere presente che, se si usano degli spazi, è necessario codificarli con il simbolo %20.</span><span class="sxs-lookup"><span data-stu-id="9c625-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="9c625-303">Vedere l'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="9c625-303">See example above.</span></span><br><span data-ttu-id="9c625-304">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="9c625-304">Max length: 50</span></span> |
| <span data-ttu-id="9c625-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9c625-305">apiVersion</span></span> |<span data-ttu-id="9c625-306">1.0</span><span class="sxs-lookup"><span data-stu-id="9c625-306">1.0</span></span> |
|  | |
| <span data-ttu-id="9c625-307">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="9c625-307">Request Body</span></span> |<span data-ttu-id="9c625-308">Nessuno</span><span class="sxs-lookup"><span data-stu-id="9c625-308">NONE</span></span> |

<span data-ttu-id="9c625-309">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="9c625-309">**Response**:</span></span>

<span data-ttu-id="9c625-310">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9c625-310">HTTP Status code: 200</span></span>

<span data-ttu-id="9c625-311">Questa è un'API asincrona.</span><span class="sxs-lookup"><span data-stu-id="9c625-311">This is an asynchronous API.</span></span> <span data-ttu-id="9c625-312">Come risposta si otterrà un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-312">You will get a build ID as a response.</span></span> <span data-ttu-id="9c625-313">Per sapere quando termina l'esecuzione della compilazione, è necessario chiamare l'API "Get Builds Status of a Model" e individuare l'ID compilazione nella risposta.</span><span class="sxs-lookup"><span data-stu-id="9c625-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="9c625-314">Tenere presente che una compilazione può richiedere minuti o ore, a seconda delle dimensioni dei dati.</span><span class="sxs-lookup"><span data-stu-id="9c625-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="9c625-315">Non è possibile usare raccomandazioni finché la compilazione non viene completata.</span><span class="sxs-lookup"><span data-stu-id="9c625-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="9c625-316">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="9c625-316">Valid build status:</span></span>

* <span data-ttu-id="9c625-317">Create: il modello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="9c625-317">Create – Model was created.</span></span>
* <span data-ttu-id="9c625-318">Queued: la compilazione del modello è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="9c625-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="9c625-319">Building: la compilazione del modello è in corso.</span><span class="sxs-lookup"><span data-stu-id="9c625-319">Building – Model is being built.</span></span>
* <span data-ttu-id="9c625-320">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="9c625-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="9c625-321">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="9c625-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="9c625-322">Canceled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="9c625-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="9c625-323">Canceling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="9c625-324">È possibile trovare l'ID compilazione nel percorso seguente: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="9c625-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="9c625-325">XML OData</span><span class="sxs-lookup"><span data-stu-id="9c625-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="9c625-326">Ottenere lo stato di compilazione di un modello</span><span class="sxs-lookup"><span data-stu-id="9c625-326">Get build status of a model</span></span>
| <span data-ttu-id="9c625-327">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="9c625-327">HTTP Method</span></span> | <span data-ttu-id="9c625-328">URI</span><span class="sxs-lookup"><span data-stu-id="9c625-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-329">GET</span><span class="sxs-lookup"><span data-stu-id="9c625-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="9c625-330">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="9c625-331">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="9c625-331">Parameter Name</span></span> | <span data-ttu-id="9c625-332">Valori validi</span><span class="sxs-lookup"><span data-stu-id="9c625-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-333">modelId</span><span class="sxs-lookup"><span data-stu-id="9c625-333">modelId</span></span> |<span data-ttu-id="9c625-334">Identificatore univoco del modello (con distinzione tra maiuscole e minuscole)</span><span class="sxs-lookup"><span data-stu-id="9c625-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="9c625-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="9c625-335">onlyLastBuild</span></span> |<span data-ttu-id="9c625-336">Indica se restituire l'intera cronologia di compilazioni del modello o solo lo stato della compilazione più recente.</span><span class="sxs-lookup"><span data-stu-id="9c625-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="9c625-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9c625-337">apiVersion</span></span> |<span data-ttu-id="9c625-338">1.0</span><span class="sxs-lookup"><span data-stu-id="9c625-338">1.0</span></span> |

<span data-ttu-id="9c625-339">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="9c625-339">**Response**:</span></span>

<span data-ttu-id="9c625-340">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9c625-340">HTTP Status code: 200</span></span>

<span data-ttu-id="9c625-341">La risposta include una voce per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-341">The response includes one entry per build.</span></span> <span data-ttu-id="9c625-342">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c625-342">Each entry has the following data:</span></span>

* <span data-ttu-id="9c625-343">`feed/entry/content/properties/UserName` : nome dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9c625-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="9c625-344">`feed/entry/content/properties/ModelName` : nome del modello.</span><span class="sxs-lookup"><span data-stu-id="9c625-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="9c625-345">`feed/entry/content/properties/ModelId` : identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="9c625-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="9c625-346">`feed/entry/content/properties/IsDeployed`: indica se la compilazione viene distribuita, anche detta</span><span class="sxs-lookup"><span data-stu-id="9c625-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="9c625-347">compilazione attiva.</span><span class="sxs-lookup"><span data-stu-id="9c625-347">active build).</span></span>
* <span data-ttu-id="9c625-348">`feed/entry/content/properties/BuildId` : identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="9c625-349">`feed/entry/content/properties/BuildType` : tipo della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="9c625-350">`feed/entry/content/properties/Status` : stato della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="9c625-351">I valori possibili sono: Error, Building, Queued, Cancelling, Cancelled, Success.</span><span class="sxs-lookup"><span data-stu-id="9c625-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="9c625-352">`feed/entry/content/properties/StatusMessage` : messaggio di stato dettagliato (si applica solo a stati specifici).</span><span class="sxs-lookup"><span data-stu-id="9c625-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="9c625-353">`feed/entry/content/properties/Progress` : stato di avanzamento della compilazione (%).</span><span class="sxs-lookup"><span data-stu-id="9c625-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="9c625-354">`feed/entry/content/properties/StartTime` : ora di inizio della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="9c625-355">`feed/entry/content/properties/EndTime` : ora di fine della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="9c625-356">`feed/entry/content/properties/ExecutionTime` : durata della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="9c625-357">`feed/entry/content/properties/ProgressStep` : dettagli relativi alla fase corrente di una compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="9c625-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="9c625-358">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="9c625-358">Valid build status:</span></span>

* <span data-ttu-id="9c625-359">Created: la voce della richiesta di compilazione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="9c625-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="9c625-360">Queued: la richiesta di compilazione è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="9c625-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="9c625-361">Building: la compilazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="9c625-361">Building – Build is in process.</span></span>
* <span data-ttu-id="9c625-362">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="9c625-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="9c625-363">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="9c625-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="9c625-364">Canceled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="9c625-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="9c625-365">Canceling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="9c625-366">Valori validi per il tipo di compilazione:</span><span class="sxs-lookup"><span data-stu-id="9c625-366">Valid values for build type:</span></span>

* <span data-ttu-id="9c625-367">Rank: compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="9c625-367">Rank - Rank build.</span></span> <span data-ttu-id="9c625-368">Per informazioni dettagliate sulla compilazione della classifica, fare riferimento al documento "Documentazione relativa all'API Recommendations di Azure Machine Learning".</span><span class="sxs-lookup"><span data-stu-id="9c625-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="9c625-369">Recommendation: compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="9c625-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="9c625-370">Fbt: compilazione Frequently Bought Together.</span><span class="sxs-lookup"><span data-stu-id="9c625-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="9c625-371">XML OData</span><span class="sxs-lookup"><span data-stu-id="9c625-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="get-recommendations"></a><span data-ttu-id="9c625-372">Ottenere raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="9c625-372">Get recommendations</span></span>
| <span data-ttu-id="9c625-373">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="9c625-373">HTTP Method</span></span> | <span data-ttu-id="9c625-374">URI</span><span class="sxs-lookup"><span data-stu-id="9c625-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-375">GET</span><span class="sxs-lookup"><span data-stu-id="9c625-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="9c625-376">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="9c625-377">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="9c625-377">Parameter Name</span></span> | <span data-ttu-id="9c625-378">Valori validi</span><span class="sxs-lookup"><span data-stu-id="9c625-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-379">modelId</span><span class="sxs-lookup"><span data-stu-id="9c625-379">modelId</span></span> |<span data-ttu-id="9c625-380">Identificatore univoco del modello con distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="9c625-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9c625-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="9c625-381">itemIds</span></span> |<span data-ttu-id="9c625-382">Elenco con valori delimitati da virgole degli elementi per i quali aggiungere raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="9c625-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="9c625-383">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="9c625-383">Max length: 1024</span></span> |
| <span data-ttu-id="9c625-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="9c625-384">numberOfResults</span></span> |<span data-ttu-id="9c625-385">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="9c625-385">Number of required results</span></span> |
| <span data-ttu-id="9c625-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="9c625-386">includeMetatadata</span></span> |<span data-ttu-id="9c625-387">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="9c625-387">Future use, always false</span></span> |
| <span data-ttu-id="9c625-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9c625-388">apiVersion</span></span> |<span data-ttu-id="9c625-389">1.0</span><span class="sxs-lookup"><span data-stu-id="9c625-389">1.0</span></span> |

<span data-ttu-id="9c625-390">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="9c625-390">**Response:**</span></span>

<span data-ttu-id="9c625-391">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9c625-391">HTTP Status code: 200</span></span>

<span data-ttu-id="9c625-392">La risposta include una voce per ogni elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="9c625-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="9c625-393">Ogni voce include i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="9c625-393">Each entry has the following data:</span></span>

* <span data-ttu-id="9c625-394">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="9c625-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="9c625-395">`Feed\entry\content\properties\Name` : nome dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="9c625-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="9c625-396">`Feed\entry\content\properties\Rating` : classificazione della raccomandazione; un numero più alto significa maggiore confidenza.</span><span class="sxs-lookup"><span data-stu-id="9c625-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="9c625-397">`Feed\entry\content\properties\Reasoning`: motivazione della raccomandazione, ad esempio una spiegazione della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="9c625-398">XML OData</span><span class="sxs-lookup"><span data-stu-id="9c625-398">OData XML</span></span>

<span data-ttu-id="9c625-399">La risposta di esempio seguente include 10 elementi consigliati:</span><span class="sxs-lookup"><span data-stu-id="9c625-399">The example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="update-model"></a><span data-ttu-id="9c625-400">Aggiornare il modello</span><span class="sxs-lookup"><span data-stu-id="9c625-400">Update model</span></span>
<span data-ttu-id="9c625-401">È possibile aggiornare la descrizione del modello o l'ID compilazione attivo.</span><span class="sxs-lookup"><span data-stu-id="9c625-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="9c625-402">*ID compilazione attiva* : ogni compilazione per ogni modello ha un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="9c625-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="9c625-403">Con il termine ID compilazione attiva si identifica la prima compilazione riuscita di ogni nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="9c625-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="9c625-404">Se dopo avere ottenuto un ID compilazione attiva si eseguono altre compilazioni per lo stesso modello, è necessario impostarlo in modo esplicito come ID compilazione predefinito.</span><span class="sxs-lookup"><span data-stu-id="9c625-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="9c625-405">Quando si usano raccomandazioni, se non si specifica l'ID compilazione da usare, verrà usato automaticamente quello predefinito.</span><span class="sxs-lookup"><span data-stu-id="9c625-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="9c625-406">Dopo avere implementato un modello di raccomandazione nell'ambiente di produzione, questo meccanismo consente di compilare nuovi modelli e testarli prima di alzarli di livello e passarli in produzione.</span><span class="sxs-lookup"><span data-stu-id="9c625-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="9c625-407">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="9c625-407">HTTP Method</span></span> | <span data-ttu-id="9c625-408">URI</span><span class="sxs-lookup"><span data-stu-id="9c625-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-409">PUT</span><span class="sxs-lookup"><span data-stu-id="9c625-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="9c625-410">Esempio:</span><span class="sxs-lookup"><span data-stu-id="9c625-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="9c625-411">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="9c625-411">Parameter Name</span></span> | <span data-ttu-id="9c625-412">Valori validi</span><span class="sxs-lookup"><span data-stu-id="9c625-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="9c625-413">id</span><span class="sxs-lookup"><span data-stu-id="9c625-413">id</span></span> |<span data-ttu-id="9c625-414">Identificatore univoco del modello con distinzione tra maiuscole e minuscole</span><span class="sxs-lookup"><span data-stu-id="9c625-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="9c625-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9c625-415">apiVersion</span></span> |<span data-ttu-id="9c625-416">1.0</span><span class="sxs-lookup"><span data-stu-id="9c625-416">1.0</span></span> |
|  | |
| <span data-ttu-id="9c625-417">Request Body</span><span class="sxs-lookup"><span data-stu-id="9c625-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="9c625-418">Si noti che i tag XML Description e ActiveBuildId sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="9c625-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="9c625-419">Se non si vuole impostare Description o ActiveBuildId, rimuovere l'intero tag.</span><span class="sxs-lookup"><span data-stu-id="9c625-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="9c625-420">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="9c625-420">**Response**:</span></span>

<span data-ttu-id="9c625-421">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="9c625-421">HTTP Status code: 200</span></span>

<span data-ttu-id="9c625-422">XML OData</span><span class="sxs-lookup"><span data-stu-id="9c625-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="9c625-423">Note legali</span><span class="sxs-lookup"><span data-stu-id="9c625-423">Legal</span></span>
<span data-ttu-id="9c625-424">Questo documento viene fornito "così com'è".</span><span class="sxs-lookup"><span data-stu-id="9c625-424">This document is provided "as-is".</span></span> <span data-ttu-id="9c625-425">Le informazioni e le indicazioni riportate nel presente documento, inclusi URL e altri riferimenti a siti Internet, sono soggette a modifica senza preavviso.</span><span class="sxs-lookup"><span data-stu-id="9c625-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="9c625-426">Alcuni esempi usati in questo documento vengono forniti a scopo puramente illustrativo e sono fittizi.</span><span class="sxs-lookup"><span data-stu-id="9c625-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="9c625-427">Nessuna associazione reale o connessione è intenzionale o può essere desunta.</span><span class="sxs-lookup"><span data-stu-id="9c625-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="9c625-428">Il presente documento non fornisce all'utente alcun diritto legale rispetto a qualsiasi proprietà intellettuale in qualsiasi prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9c625-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="9c625-429">È possibile copiare e usare il presente documento per scopi interni e di riferimento.</span><span class="sxs-lookup"><span data-stu-id="9c625-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="9c625-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9c625-430">© 2014 Microsoft.</span></span> <span data-ttu-id="9c625-431">Tutti i diritti sono riservati.</span><span class="sxs-lookup"><span data-stu-id="9c625-431">All rights reserved.</span></span> 

