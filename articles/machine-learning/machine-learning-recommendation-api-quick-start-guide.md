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
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="4ce77-104">Guida introduttiva per hello Machine Learning indicazioni API (versione 1)</span><span class="sxs-lookup"><span data-stu-id="4ce77-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="4ce77-105">È consigliabile iniziare a utilizzare hello [servizio di suggerimenti API cognitivi](https://www.microsoft.com/cognitive-services/recommendations-api) anziché questa versione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="4ce77-106">Hello servizio cognitivi indicazioni andrà a sostituire questo servizio e tutte le nuove funzionalità hello verranno sviluppate non esiste.</span><span class="sxs-lookup"><span data-stu-id="4ce77-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="4ce77-107">Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.</span><span class="sxs-lookup"><span data-stu-id="4ce77-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="4ce77-108">Altre informazioni, vedere [toohello migrazione nuovo servizio cognitivi](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="4ce77-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="4ce77-109">Questo documento descrive come tooonboard il toouse servizi o applicazioni di Microsoft Azure Machine Learning indicazioni.</span><span class="sxs-lookup"><span data-stu-id="4ce77-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="4ce77-110">È possibile trovare ulteriori informazioni sul Ciao indicazioni API hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="4ce77-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="4ce77-111">Panoramica generale</span><span class="sxs-lookup"><span data-stu-id="4ce77-111">General overview</span></span>
<span data-ttu-id="4ce77-112">toouse indicazioni di Azure Machine Learning, è necessario hello tootake alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ce77-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="4ce77-113">Creare un modello, un modello è un contenitore di dati di utilizzo e dati del catalogo, il modello di raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="4ce77-114">Importazione dei dati del catalogo: un catalogo contiene informazioni sui metadati per gli elementi di hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="4ce77-115">Importare i dati di utilizzo: i dati di utilizzo possono essere caricati usando uno o entrambi i modi seguenti.</span><span class="sxs-lookup"><span data-stu-id="4ce77-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="4ce77-116">Caricando un file che contiene i dati di utilizzo hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="4ce77-117">Inviando eventi di acquisizione dei dati.</span><span class="sxs-lookup"><span data-stu-id="4ce77-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="4ce77-118">In genere si carica un file di utilizzo in ordine toobe in grado di toocreate un modello di raccomandazione iniziale (bootstrap) e utilizzarla fino a quando il sistema hello raccoglie dati sufficienti con formato di acquisizione dati hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="4ce77-119">Compilare un modello di raccomandazione: si tratta di un'operazione asincrona, in cui hello sistema di raccomandazione accetta tutti i dati di utilizzo di hello e crea un modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="4ce77-120">Questa operazione può richiedere alcuni minuti o alcune ore a seconda di hello dimensione dei dati di hello e hello compilare i parametri di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="4ce77-121">Al momento della generazione compilazione hello, si otterrà un ID di generazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="4ce77-122">Utilizzarla toocheck quando il processo di compilazione hello è terminata prima di avviare tooconsume indicazioni.</span><span class="sxs-lookup"><span data-stu-id="4ce77-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="4ce77-123">Utilizzare le raccomandazioni: ottenere raccomandazioni per un elemento o un elenco di elementi specifico.</span><span class="sxs-lookup"><span data-stu-id="4ce77-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="4ce77-124">Tutti i passaggi di hello precedenti vengono eseguiti tramite API di Azure Machine Learning indicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="4ce77-125">È possibile scaricare un'applicazione di esempio che implementa ognuno di questi passaggi da hello [nonché il gallery.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="4ce77-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="4ce77-126">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="4ce77-126">Limitations</span></span>
* <span data-ttu-id="4ce77-127">numero massimo di Hello di modelli per ogni sottoscrizione è 10.</span><span class="sxs-lookup"><span data-stu-id="4ce77-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="4ce77-128">numero massimo di Hello di elementi che può contenere un catalogo è 100.000.</span><span class="sxs-lookup"><span data-stu-id="4ce77-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="4ce77-129">numero massimo di Hello di punti di utilizzo che vengono conservati è ~ 5.000.000.</span><span class="sxs-lookup"><span data-stu-id="4ce77-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="4ce77-130">Hello meno recente verrà eliminato verranno caricati o segnalati nuovi.</span><span class="sxs-lookup"><span data-stu-id="4ce77-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="4ce77-131">dimensione massima di Hello di dati che possono essere inviati in POST (ad esempio, Importa dati del catalogo, importazione dati di utilizzo) è pari a 200MB.</span><span class="sxs-lookup"><span data-stu-id="4ce77-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="4ce77-132">Hello numero di transazioni al secondo per una compilazione del modello di raccomandazione che non è attiva è ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="4ce77-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="4ce77-133">Una build di modello di raccomandazione attivo può contenere fino too20TPS.</span><span class="sxs-lookup"><span data-stu-id="4ce77-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="4ce77-134">Integrazione</span><span class="sxs-lookup"><span data-stu-id="4ce77-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="4ce77-135">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="4ce77-135">Authentication</span></span>
<span data-ttu-id="4ce77-136">Microsoft Azure Marketplace supporta un metodo di autenticazione di base o OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="4ce77-137">È possibile trovare facilmente hello chiavi dell'account passando chiavi toohello nel marketplace hello in [le impostazioni dell'account](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="4ce77-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="4ce77-138">Autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="4ce77-138">Basic Authentication</span></span>
<span data-ttu-id="4ce77-139">Aggiungere un'intestazione Authorization hello:</span><span class="sxs-lookup"><span data-stu-id="4ce77-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="4ce77-140">Convertire tooBase64 (c#)</span><span class="sxs-lookup"><span data-stu-id="4ce77-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="4ce77-141">Convertire tooBase64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="4ce77-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="4ce77-142">URI del servizio</span><span class="sxs-lookup"><span data-stu-id="4ce77-142">Service URI</span></span>
<span data-ttu-id="4ce77-143">Hello URI radice del servizio per le API di Azure Machine Learning indicazioni hello è [qui.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="4ce77-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="4ce77-144">URI del servizio completo Hello viene espresso utilizzando gli elementi della specifica OData hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="4ce77-145">Versione dell'API</span><span class="sxs-lookup"><span data-stu-id="4ce77-145">API version</span></span>
<span data-ttu-id="4ce77-146">Ogni chiamata API avrà, alla fine di hello, un parametro di query denominato apiVersion che deve essere impostata troppo "1.0".</span><span class="sxs-lookup"><span data-stu-id="4ce77-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="4ce77-147">Distinzione tra maiuscole e minuscole negli ID</span><span class="sxs-lookup"><span data-stu-id="4ce77-147">IDs are case-sensitive</span></span>
<span data-ttu-id="4ce77-148">Gli ID, restituiti da una delle API, hello tra maiuscole e minuscole e devono essere usati come tali, quando viene passato come parametro nelle chiamate API successive.</span><span class="sxs-lookup"><span data-stu-id="4ce77-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="4ce77-149">Anche gli ID modello e gli ID catalogo, ad esempio, fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4ce77-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="4ce77-150">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="4ce77-150">Create a model</span></span>
<span data-ttu-id="4ce77-151">Creazione di una richiesta "crea modello":</span><span class="sxs-lookup"><span data-stu-id="4ce77-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="4ce77-152">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4ce77-152">HTTP Method</span></span> | <span data-ttu-id="4ce77-153">URI</span><span class="sxs-lookup"><span data-stu-id="4ce77-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-154">POST</span><span class="sxs-lookup"><span data-stu-id="4ce77-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4ce77-155">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4ce77-156">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4ce77-156">Parameter Name</span></span> | <span data-ttu-id="4ce77-157">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4ce77-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-158">modelName</span><span class="sxs-lookup"><span data-stu-id="4ce77-158">modelName</span></span> |<span data-ttu-id="4ce77-159">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="4ce77-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4ce77-160">Lunghezza massima: 20</span><span class="sxs-lookup"><span data-stu-id="4ce77-160">Max length: 20</span></span> |
| <span data-ttu-id="4ce77-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4ce77-161">apiVersion</span></span> |<span data-ttu-id="4ce77-162">1.0</span><span class="sxs-lookup"><span data-stu-id="4ce77-162">1.0</span></span> |
|  | |
| <span data-ttu-id="4ce77-163">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4ce77-163">Request Body</span></span> |<span data-ttu-id="4ce77-164">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4ce77-164">NONE</span></span> |

<span data-ttu-id="4ce77-165">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4ce77-165">**Response**:</span></span>

<span data-ttu-id="4ce77-166">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4ce77-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="4ce77-167">`feed/entry/content/properties/id`-Contiene l'ID del modello hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="4ce77-168">Si noti che ID modello hello tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4ce77-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="4ce77-169">XML OData</span><span class="sxs-lookup"><span data-stu-id="4ce77-169">OData XML</span></span>

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


### <a name="import-catalog-data"></a><span data-ttu-id="4ce77-170">Importare i dati del catalogo</span><span class="sxs-lookup"><span data-stu-id="4ce77-170">Import catalog data</span></span>
<span data-ttu-id="4ce77-171">Se si carica più catalogo file toohello stesso modello con più chiamate, si verranno inserire hello solo nuovi elementi di catalogo.</span><span class="sxs-lookup"><span data-stu-id="4ce77-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="4ce77-172">Gli elementi esistenti verranno mantenuti con i valori originali di hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="4ce77-173">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4ce77-173">HTTP Method</span></span> | <span data-ttu-id="4ce77-174">URI</span><span class="sxs-lookup"><span data-stu-id="4ce77-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-175">POST</span><span class="sxs-lookup"><span data-stu-id="4ce77-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4ce77-176">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4ce77-177">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4ce77-177">Parameter Name</span></span> | <span data-ttu-id="4ce77-178">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4ce77-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-179">modelId</span><span class="sxs-lookup"><span data-stu-id="4ce77-179">modelId</span></span> |<span data-ttu-id="4ce77-180">Identificatore univoco del modello di hello (maiuscole/minuscole)</span><span class="sxs-lookup"><span data-stu-id="4ce77-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="4ce77-181">filename</span><span class="sxs-lookup"><span data-stu-id="4ce77-181">filename</span></span> |<span data-ttu-id="4ce77-182">Identificatore testuale del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="4ce77-183">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="4ce77-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4ce77-184">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4ce77-184">Max length: 50</span></span> |
| <span data-ttu-id="4ce77-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4ce77-185">apiVersion</span></span> |<span data-ttu-id="4ce77-186">1.0</span><span class="sxs-lookup"><span data-stu-id="4ce77-186">1.0</span></span> |
|  | |
| <span data-ttu-id="4ce77-187">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4ce77-187">Request Body</span></span> |<span data-ttu-id="4ce77-188">Dati del catalogo.</span><span class="sxs-lookup"><span data-stu-id="4ce77-188">Catalog data.</span></span> <span data-ttu-id="4ce77-189">Formato:</span><span class="sxs-lookup"><span data-stu-id="4ce77-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="4ce77-190">Nome</span><span class="sxs-lookup"><span data-stu-id="4ce77-190">Name</span></span></th><th><span data-ttu-id="4ce77-191">Mandatory</span><span class="sxs-lookup"><span data-stu-id="4ce77-191">Mandatory</span></span></th><th><span data-ttu-id="4ce77-192">Tipo</span><span class="sxs-lookup"><span data-stu-id="4ce77-192">Type</span></span></th><th><span data-ttu-id="4ce77-193">Description</span><span class="sxs-lookup"><span data-stu-id="4ce77-193">Description</span></span></th></tr><tr><td><span data-ttu-id="4ce77-194">Item Id</span><span class="sxs-lookup"><span data-stu-id="4ce77-194">Item Id</span></span></td><td><span data-ttu-id="4ce77-195">Sì</span><span class="sxs-lookup"><span data-stu-id="4ce77-195">Yes</span></span></td><td><span data-ttu-id="4ce77-196">Alfanumerico, lunghezza massima: 50 caratteri</span><span class="sxs-lookup"><span data-stu-id="4ce77-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="4ce77-197">Identificatore univoco di un elemento</span><span class="sxs-lookup"><span data-stu-id="4ce77-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="4ce77-198">Item Name</span><span class="sxs-lookup"><span data-stu-id="4ce77-198">Item Name</span></span></td><td><span data-ttu-id="4ce77-199">Sì</span><span class="sxs-lookup"><span data-stu-id="4ce77-199">Yes</span></span></td><td><span data-ttu-id="4ce77-200">Alfanumerico, lunghezza massima: 255 caratteri</span><span class="sxs-lookup"><span data-stu-id="4ce77-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="4ce77-201">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="4ce77-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="4ce77-202">Item Category</span><span class="sxs-lookup"><span data-stu-id="4ce77-202">Item Category</span></span></td><td><span data-ttu-id="4ce77-203">Sì</span><span class="sxs-lookup"><span data-stu-id="4ce77-203">Yes</span></span></td><td><span data-ttu-id="4ce77-204">Alfanumerico, lunghezza massima: 255 caratteri</span><span class="sxs-lookup"><span data-stu-id="4ce77-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="4ce77-205">Categoria toowhich che questo elemento appartiene (ad esempio, documentazione, cucina serie...)</span><span class="sxs-lookup"><span data-stu-id="4ce77-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="4ce77-206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4ce77-206">Description</span></span></td><td><span data-ttu-id="4ce77-207">No</span><span class="sxs-lookup"><span data-stu-id="4ce77-207">No</span></span></td><td><span data-ttu-id="4ce77-208">Alfanumerico, lunghezza massima: 4000 caratteri</span><span class="sxs-lookup"><span data-stu-id="4ce77-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="4ce77-209">Descrizione dell'elemento</span><span class="sxs-lookup"><span data-stu-id="4ce77-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="4ce77-210">La dimensione massima del file è di 200 MB.</span><span class="sxs-lookup"><span data-stu-id="4ce77-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="4ce77-211">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="4ce77-212">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4ce77-212">**Response**:</span></span>

<span data-ttu-id="4ce77-213">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4ce77-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="4ce77-214">`Feed\entry\content\properties\LineCount` : numero di righe accettate.</span><span class="sxs-lookup"><span data-stu-id="4ce77-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="4ce77-215">`Feed\entry\content\properties\ErrorCount`-Numero di righe che non sono state inserite a causa di errore tooan.</span><span class="sxs-lookup"><span data-stu-id="4ce77-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="4ce77-216">XML OData</span><span class="sxs-lookup"><span data-stu-id="4ce77-216">OData XML</span></span>

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


### <a name="import-usage-data"></a><span data-ttu-id="4ce77-217">Importare i dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="4ce77-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="4ce77-218">Caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="4ce77-218">Uploading a file</span></span>
<span data-ttu-id="4ce77-219">Questa sezione viene illustrato come dati di utilizzo tooupload utilizzando un file.</span><span class="sxs-lookup"><span data-stu-id="4ce77-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="4ce77-220">È possibile chiamare l'API più volte con i dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4ce77-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="4ce77-221">Tutti i dati di utilizzo verranno salvati per tutte le chiamate.</span><span class="sxs-lookup"><span data-stu-id="4ce77-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="4ce77-222">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4ce77-222">HTTP Method</span></span> | <span data-ttu-id="4ce77-223">URI</span><span class="sxs-lookup"><span data-stu-id="4ce77-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-224">POST</span><span class="sxs-lookup"><span data-stu-id="4ce77-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4ce77-225">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4ce77-226">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4ce77-226">Parameter Name</span></span> | <span data-ttu-id="4ce77-227">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4ce77-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-228">modelId</span><span class="sxs-lookup"><span data-stu-id="4ce77-228">modelId</span></span> |<span data-ttu-id="4ce77-229">Identificatore univoco del modello di hello (maiuscole/minuscole)</span><span class="sxs-lookup"><span data-stu-id="4ce77-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="4ce77-230">filename</span><span class="sxs-lookup"><span data-stu-id="4ce77-230">filename</span></span> |<span data-ttu-id="4ce77-231">Identificatore testuale del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="4ce77-232">Sono consentiti solo lettere (A-Z, a-z), numeri (0-9), trattini (-) e caratteri di sottolineatura (_).</span><span class="sxs-lookup"><span data-stu-id="4ce77-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4ce77-233">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4ce77-233">Max length: 50</span></span> |
| <span data-ttu-id="4ce77-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4ce77-234">apiVersion</span></span> |<span data-ttu-id="4ce77-235">1.0</span><span class="sxs-lookup"><span data-stu-id="4ce77-235">1.0</span></span> |
|  | |
| <span data-ttu-id="4ce77-236">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4ce77-236">Request Body</span></span> |<span data-ttu-id="4ce77-237">Dati di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4ce77-237">Usage data.</span></span> <span data-ttu-id="4ce77-238">Formato:</span><span class="sxs-lookup"><span data-stu-id="4ce77-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="4ce77-239">Nome</span><span class="sxs-lookup"><span data-stu-id="4ce77-239">Name</span></span></th><th><span data-ttu-id="4ce77-240">Mandatory</span><span class="sxs-lookup"><span data-stu-id="4ce77-240">Mandatory</span></span></th><th><span data-ttu-id="4ce77-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="4ce77-241">Type</span></span></th><th><span data-ttu-id="4ce77-242">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4ce77-242">Description</span></span></th></tr><tr><td><span data-ttu-id="4ce77-243">User Id</span><span class="sxs-lookup"><span data-stu-id="4ce77-243">User Id</span></span></td><td><span data-ttu-id="4ce77-244">Sì</span><span class="sxs-lookup"><span data-stu-id="4ce77-244">Yes</span></span></td><td><span data-ttu-id="4ce77-245">Alfanumerico</span><span class="sxs-lookup"><span data-stu-id="4ce77-245">Alphanumeric</span></span></td><td><span data-ttu-id="4ce77-246">Identificatore univoco di un utente</span><span class="sxs-lookup"><span data-stu-id="4ce77-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="4ce77-247">Item Id</span><span class="sxs-lookup"><span data-stu-id="4ce77-247">Item Id</span></span></td><td><span data-ttu-id="4ce77-248">Sì</span><span class="sxs-lookup"><span data-stu-id="4ce77-248">Yes</span></span></td><td><span data-ttu-id="4ce77-249">Alfanumerico, lunghezza massima: 50 caratteri</span><span class="sxs-lookup"><span data-stu-id="4ce77-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="4ce77-250">Identificatore univoco di un elemento</span><span class="sxs-lookup"><span data-stu-id="4ce77-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="4ce77-251">Time</span><span class="sxs-lookup"><span data-stu-id="4ce77-251">Time</span></span></td><td><span data-ttu-id="4ce77-252">No</span><span class="sxs-lookup"><span data-stu-id="4ce77-252">No</span></span></td><td><span data-ttu-id="4ce77-253">Data in formato: AAAA/MM/GGTHH:MM:SS (ad esempio 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="4ce77-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="4ce77-254">Ora dei dati</span><span class="sxs-lookup"><span data-stu-id="4ce77-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="4ce77-255">Evento</span><span class="sxs-lookup"><span data-stu-id="4ce77-255">Event</span></span></td><td><span data-ttu-id="4ce77-256">No, se fornito deve essere inserita anche la data</span><span class="sxs-lookup"><span data-stu-id="4ce77-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="4ce77-257">Uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="4ce77-257">One of hello following:</span></span><br><span data-ttu-id="4ce77-258">• Click</span><span class="sxs-lookup"><span data-stu-id="4ce77-258">• Click</span></span><br><span data-ttu-id="4ce77-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="4ce77-259">• RecommendationClick</span></span><br><span data-ttu-id="4ce77-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="4ce77-260">•    AddShopCart</span></span><br><span data-ttu-id="4ce77-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="4ce77-261">• RemoveShopCart</span></span><br><span data-ttu-id="4ce77-262">• Acquisto</span><span class="sxs-lookup"><span data-stu-id="4ce77-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="4ce77-263">La dimensione massima del file è di 200 MB.</span><span class="sxs-lookup"><span data-stu-id="4ce77-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="4ce77-264">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="4ce77-265">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4ce77-265">**Response**:</span></span>

<span data-ttu-id="4ce77-266">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4ce77-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="4ce77-267">`Feed\entry\content\properties\LineCount` : numero di righe accettate.</span><span class="sxs-lookup"><span data-stu-id="4ce77-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="4ce77-268">`Feed\entry\content\properties\ErrorCount`-Numero di righe che non sono state inserite a causa di errore tooan.</span><span class="sxs-lookup"><span data-stu-id="4ce77-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="4ce77-269">`Feed\entry\content\properties\FileId` : identificatore del file.</span><span class="sxs-lookup"><span data-stu-id="4ce77-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="4ce77-270">XML OData</span><span class="sxs-lookup"><span data-stu-id="4ce77-270">OData XML</span></span>

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


#### <a name="using-data-acquisition"></a><span data-ttu-id="4ce77-271">Uso dell'acquisizione dei dati</span><span class="sxs-lookup"><span data-stu-id="4ce77-271">Using data acquisition</span></span>
<span data-ttu-id="4ce77-272">In questa sezione viene illustrato come gli eventi toosend reale ora tooAzure Machine Learning indicazioni, in genere il sito Web.</span><span class="sxs-lookup"><span data-stu-id="4ce77-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="4ce77-273">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4ce77-273">HTTP Method</span></span> | <span data-ttu-id="4ce77-274">URI</span><span class="sxs-lookup"><span data-stu-id="4ce77-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-275">POST</span><span class="sxs-lookup"><span data-stu-id="4ce77-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4ce77-276">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4ce77-276">Parameter Name</span></span> | <span data-ttu-id="4ce77-277">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4ce77-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4ce77-278">apiVersion</span></span> |<span data-ttu-id="4ce77-279">1.0</span><span class="sxs-lookup"><span data-stu-id="4ce77-279">1.0</span></span> |
|  | |
| <span data-ttu-id="4ce77-280">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4ce77-280">Request body</span></span> |<span data-ttu-id="4ce77-281">Immissione di dati di evento per ogni evento desiderato toosend.</span><span class="sxs-lookup"><span data-stu-id="4ce77-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="4ce77-282">È necessario inviare per stessa sessione utente o un browser hello hello stesso ID nel campo SessionId hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="4ce77-283">Vedere l'esempio di corpo dell'evento di seguito.</span><span class="sxs-lookup"><span data-stu-id="4ce77-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="4ce77-284">Esempio di evento "Click":</span><span class="sxs-lookup"><span data-stu-id="4ce77-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="4ce77-285">Esempio di evento "RecommendationClick":</span><span class="sxs-lookup"><span data-stu-id="4ce77-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="4ce77-286">Esempio di evento "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="4ce77-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="4ce77-287">Esempio di evento "RemoveShopCart":</span><span class="sxs-lookup"><span data-stu-id="4ce77-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="4ce77-288">Esempio di evento "Purchase":</span><span class="sxs-lookup"><span data-stu-id="4ce77-288">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="4ce77-289">Esempio di invio di due eventi, "Click" e "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="4ce77-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="4ce77-290">**Risposta**: Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4ce77-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="4ce77-291">Compilare un modello di raccomandazione</span><span class="sxs-lookup"><span data-stu-id="4ce77-291">Build a recommendation model</span></span>
| <span data-ttu-id="4ce77-292">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4ce77-292">HTTP Method</span></span> | <span data-ttu-id="4ce77-293">URI</span><span class="sxs-lookup"><span data-stu-id="4ce77-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-294">POST</span><span class="sxs-lookup"><span data-stu-id="4ce77-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4ce77-295">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4ce77-296">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4ce77-296">Parameter Name</span></span> | <span data-ttu-id="4ce77-297">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4ce77-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-298">modelId</span><span class="sxs-lookup"><span data-stu-id="4ce77-298">modelId</span></span> |<span data-ttu-id="4ce77-299">Identificatore univoco del modello di hello (maiuscole/minuscole)</span><span class="sxs-lookup"><span data-stu-id="4ce77-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="4ce77-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="4ce77-300">userDescription</span></span> |<span data-ttu-id="4ce77-301">Identificatore testuale del catalogo hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="4ce77-302">Tenere presente che, se si usano degli spazi, è necessario codificarli con il simbolo %20.</span><span class="sxs-lookup"><span data-stu-id="4ce77-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="4ce77-303">Vedere l'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="4ce77-303">See example above.</span></span><br><span data-ttu-id="4ce77-304">Lunghezza massima: 50</span><span class="sxs-lookup"><span data-stu-id="4ce77-304">Max length: 50</span></span> |
| <span data-ttu-id="4ce77-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4ce77-305">apiVersion</span></span> |<span data-ttu-id="4ce77-306">1.0</span><span class="sxs-lookup"><span data-stu-id="4ce77-306">1.0</span></span> |
|  | |
| <span data-ttu-id="4ce77-307">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="4ce77-307">Request Body</span></span> |<span data-ttu-id="4ce77-308">Nessuno</span><span class="sxs-lookup"><span data-stu-id="4ce77-308">NONE</span></span> |

<span data-ttu-id="4ce77-309">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4ce77-309">**Response**:</span></span>

<span data-ttu-id="4ce77-310">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4ce77-310">HTTP Status code: 200</span></span>

<span data-ttu-id="4ce77-311">Questa è un'API asincrona.</span><span class="sxs-lookup"><span data-stu-id="4ce77-311">This is an asynchronous API.</span></span> <span data-ttu-id="4ce77-312">Come risposta si otterrà un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-312">You will get a build ID as a response.</span></span> <span data-ttu-id="4ce77-313">tooknow al termine di generazione di hello, è necessario chiamare API "Ottenere compilazioni lo stato di un modello di" hello e individuare questo ID di generazione in risposta hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="4ce77-314">Si noti che una compilazione può richiedere da toohours minuti a seconda delle dimensioni di hello dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="4ce77-315">Impossibile consumare indicazioni finché non termina di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="4ce77-316">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="4ce77-316">Valid build status:</span></span>

* <span data-ttu-id="4ce77-317">Create: il modello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="4ce77-317">Create – Model was created.</span></span>
* <span data-ttu-id="4ce77-318">Queued: la compilazione del modello è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="4ce77-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="4ce77-319">Building: la compilazione del modello è in corso.</span><span class="sxs-lookup"><span data-stu-id="4ce77-319">Building – Model is being built.</span></span>
* <span data-ttu-id="4ce77-320">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="4ce77-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="4ce77-321">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="4ce77-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="4ce77-322">Canceled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="4ce77-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="4ce77-323">Canceling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="4ce77-324">Si noti che compilazione hello che ID è reperibile nella hello seguente percorso:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="4ce77-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="4ce77-325">XML OData</span><span class="sxs-lookup"><span data-stu-id="4ce77-325">OData XML</span></span>

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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="4ce77-326">Ottenere lo stato di compilazione di un modello</span><span class="sxs-lookup"><span data-stu-id="4ce77-326">Get build status of a model</span></span>
| <span data-ttu-id="4ce77-327">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4ce77-327">HTTP Method</span></span> | <span data-ttu-id="4ce77-328">URI</span><span class="sxs-lookup"><span data-stu-id="4ce77-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-329">GET</span><span class="sxs-lookup"><span data-stu-id="4ce77-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4ce77-330">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="4ce77-331">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4ce77-331">Parameter Name</span></span> | <span data-ttu-id="4ce77-332">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4ce77-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-333">modelId</span><span class="sxs-lookup"><span data-stu-id="4ce77-333">modelId</span></span> |<span data-ttu-id="4ce77-334">Identificatore univoco del modello di hello (maiuscole/minuscole)</span><span class="sxs-lookup"><span data-stu-id="4ce77-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="4ce77-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="4ce77-335">onlyLastBuild</span></span> |<span data-ttu-id="4ce77-336">Indica se tutti hello tooreturn compilare solo stato hello di compilazione più recente di hello o cronologia del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="4ce77-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4ce77-337">apiVersion</span></span> |<span data-ttu-id="4ce77-338">1.0</span><span class="sxs-lookup"><span data-stu-id="4ce77-338">1.0</span></span> |

<span data-ttu-id="4ce77-339">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4ce77-339">**Response**:</span></span>

<span data-ttu-id="4ce77-340">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4ce77-340">HTTP Status code: 200</span></span>

<span data-ttu-id="4ce77-341">risposta Hello include una voce per ogni compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-341">hello response includes one entry per build.</span></span> <span data-ttu-id="4ce77-342">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ce77-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="4ce77-343">`feed/entry/content/properties/UserName`– Nome dell'utente di hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="4ce77-344">`feed/entry/content/properties/ModelName`– Nome del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="4ce77-345">`feed/entry/content/properties/ModelId` : identificatore univoco del modello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="4ce77-346">`feed/entry/content/properties/IsDeployed`– Se hello build è stata distribuita (anche noto come</span><span class="sxs-lookup"><span data-stu-id="4ce77-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="4ce77-347">compilazione attiva).</span><span class="sxs-lookup"><span data-stu-id="4ce77-347">active build).</span></span>
* <span data-ttu-id="4ce77-348">`feed/entry/content/properties/BuildId` : identificatore univoco della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="4ce77-349">`feed/entry/content/properties/BuildType`-Tipo di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="4ce77-350">`feed/entry/content/properties/Status` : stato della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="4ce77-351">Può essere uno dei seguenti hello: errore, compilazione, in coda, l'annullamento, annullato, operazione riuscita</span><span class="sxs-lookup"><span data-stu-id="4ce77-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="4ce77-352">`feed/entry/content/properties/StatusMessage`: Messaggio di stato dettagliate (si applica solo a toospecific stati).</span><span class="sxs-lookup"><span data-stu-id="4ce77-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="4ce77-353">`feed/entry/content/properties/Progress` : stato di avanzamento della compilazione (%).</span><span class="sxs-lookup"><span data-stu-id="4ce77-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="4ce77-354">`feed/entry/content/properties/StartTime` : ora di inizio della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="4ce77-355">`feed/entry/content/properties/EndTime` : ora di fine della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="4ce77-356">`feed/entry/content/properties/ExecutionTime` : durata della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="4ce77-357">`feed/entry/content/properties/ProgressStep`: Informazioni dettagliate sulla fase corrente di hello che è in una compilazione in corso.</span><span class="sxs-lookup"><span data-stu-id="4ce77-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="4ce77-358">Stati di compilazione validi:</span><span class="sxs-lookup"><span data-stu-id="4ce77-358">Valid build status:</span></span>

* <span data-ttu-id="4ce77-359">Created: la voce della richiesta di compilazione è stata creata.</span><span class="sxs-lookup"><span data-stu-id="4ce77-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="4ce77-360">Queued: la richiesta di compilazione è stata attivata ed è in coda.</span><span class="sxs-lookup"><span data-stu-id="4ce77-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="4ce77-361">Building: la compilazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="4ce77-361">Building – Build is in process.</span></span>
* <span data-ttu-id="4ce77-362">Success: la compilazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="4ce77-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="4ce77-363">Error: la compilazione è terminata con un errore.</span><span class="sxs-lookup"><span data-stu-id="4ce77-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="4ce77-364">Canceled: la compilazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="4ce77-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="4ce77-365">Canceling: è in corso l'annullamento della compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="4ce77-366">Valori validi per il tipo di compilazione:</span><span class="sxs-lookup"><span data-stu-id="4ce77-366">Valid values for build type:</span></span>

* <span data-ttu-id="4ce77-367">Rank: compilazione della classifica.</span><span class="sxs-lookup"><span data-stu-id="4ce77-367">Rank - Rank build.</span></span> <span data-ttu-id="4ce77-368">(Per rango di compilazione dettagli, consultare il documento di "Documentazione di Machine Learning raccomandazione API" toohello).</span><span class="sxs-lookup"><span data-stu-id="4ce77-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="4ce77-369">Recommendation: compilazione di raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="4ce77-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="4ce77-370">Fbt: compilazione Frequently Bought Together.</span><span class="sxs-lookup"><span data-stu-id="4ce77-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="4ce77-371">XML OData</span><span class="sxs-lookup"><span data-stu-id="4ce77-371">OData XML</span></span>

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


### <a name="get-recommendations"></a><span data-ttu-id="4ce77-372">Ottenere raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="4ce77-372">Get recommendations</span></span>
| <span data-ttu-id="4ce77-373">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4ce77-373">HTTP Method</span></span> | <span data-ttu-id="4ce77-374">URI</span><span class="sxs-lookup"><span data-stu-id="4ce77-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-375">GET</span><span class="sxs-lookup"><span data-stu-id="4ce77-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4ce77-376">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="4ce77-377">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4ce77-377">Parameter Name</span></span> | <span data-ttu-id="4ce77-378">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4ce77-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-379">modelId</span><span class="sxs-lookup"><span data-stu-id="4ce77-379">modelId</span></span> |<span data-ttu-id="4ce77-380">Identificatore univoco del modello di hello (maiuscole/minuscole)</span><span class="sxs-lookup"><span data-stu-id="4ce77-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="4ce77-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="4ce77-381">itemIds</span></span> |<span data-ttu-id="4ce77-382">Elenco delimitato da virgole di hello elementi toorecommend per.</span><span class="sxs-lookup"><span data-stu-id="4ce77-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="4ce77-383">Lunghezza massima: 1024</span><span class="sxs-lookup"><span data-stu-id="4ce77-383">Max length: 1024</span></span> |
| <span data-ttu-id="4ce77-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4ce77-384">numberOfResults</span></span> |<span data-ttu-id="4ce77-385">Numero di risultati richiesti </span><span class="sxs-lookup"><span data-stu-id="4ce77-385">Number of required results</span></span> |
| <span data-ttu-id="4ce77-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4ce77-386">includeMetatadata</span></span> |<span data-ttu-id="4ce77-387">Uso futuro, sempre false.</span><span class="sxs-lookup"><span data-stu-id="4ce77-387">Future use, always false</span></span> |
| <span data-ttu-id="4ce77-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4ce77-388">apiVersion</span></span> |<span data-ttu-id="4ce77-389">1.0</span><span class="sxs-lookup"><span data-stu-id="4ce77-389">1.0</span></span> |

<span data-ttu-id="4ce77-390">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="4ce77-390">**Response:**</span></span>

<span data-ttu-id="4ce77-391">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4ce77-391">HTTP Status code: 200</span></span>

<span data-ttu-id="4ce77-392">risposta Hello include una voce per ogni elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4ce77-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="4ce77-393">Ogni voce include hello dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ce77-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="4ce77-394">`Feed\entry\content\properties\Id` : ID elemento consigliato.</span><span class="sxs-lookup"><span data-stu-id="4ce77-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4ce77-395">`Feed\entry\content\properties\Name`-Nome dell'elemento di hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="4ce77-396">`Feed\entry\content\properties\Rating`-Classificazione della raccomandazione hello; numero più alto, maggiore affidabilità.</span><span class="sxs-lookup"><span data-stu-id="4ce77-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4ce77-397">`Feed\entry\content\properties\Reasoning`: motivazione della raccomandazione, ad esempio una spiegazione della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="4ce77-398">XML OData</span><span class="sxs-lookup"><span data-stu-id="4ce77-398">OData XML</span></span>

<span data-ttu-id="4ce77-399">risposta di esempio Hello riportata di seguito include 10 elementi consigliati:</span><span class="sxs-lookup"><span data-stu-id="4ce77-399">hello example response below includes 10 recommended items:</span></span>

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

### <a name="update-model"></a><span data-ttu-id="4ce77-400">Aggiornare il modello</span><span class="sxs-lookup"><span data-stu-id="4ce77-400">Update model</span></span>
<span data-ttu-id="4ce77-401">È possibile aggiornare la descrizione del modello hello o hello ID di generazione attivo.</span><span class="sxs-lookup"><span data-stu-id="4ce77-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="4ce77-402">*ID compilazione attiva* : ogni compilazione per ogni modello ha un ID compilazione.</span><span class="sxs-lookup"><span data-stu-id="4ce77-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="4ce77-403">ID compilazione attiva Hello è hello prima corretta compilazione di ogni nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="4ce77-404">Quando si ha un ID compilazione attiva e si compilazioni aggiuntive per hello stesso modello, è necessario tooexplicitly impostarlo come hello predefinito ID compilazione se si desidera.</span><span class="sxs-lookup"><span data-stu-id="4ce77-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="4ce77-405">Quando si utilizzano indicazioni, se non si specifica l'ID compilazione hello che si desidera toouse, predefinito hello uno verrà utilizzato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4ce77-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="4ce77-406">Questo meccanismo consente - dopo aver un modello di raccomandazione nella produzione - toobuild nuovi modelli e testarli prima si innalza di livello li tooproduction.</span><span class="sxs-lookup"><span data-stu-id="4ce77-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="4ce77-407">Metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="4ce77-407">HTTP Method</span></span> | <span data-ttu-id="4ce77-408">URI</span><span class="sxs-lookup"><span data-stu-id="4ce77-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-409">PUT</span><span class="sxs-lookup"><span data-stu-id="4ce77-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4ce77-410">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4ce77-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4ce77-411">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="4ce77-411">Parameter Name</span></span> | <span data-ttu-id="4ce77-412">Valori validi</span><span class="sxs-lookup"><span data-stu-id="4ce77-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4ce77-413">id</span><span class="sxs-lookup"><span data-stu-id="4ce77-413">id</span></span> |<span data-ttu-id="4ce77-414">Identificatore univoco del modello di hello (maiuscole/minuscole)</span><span class="sxs-lookup"><span data-stu-id="4ce77-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="4ce77-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4ce77-415">apiVersion</span></span> |<span data-ttu-id="4ce77-416">1.0</span><span class="sxs-lookup"><span data-stu-id="4ce77-416">1.0</span></span> |
|  | |
| <span data-ttu-id="4ce77-417">Request Body</span><span class="sxs-lookup"><span data-stu-id="4ce77-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="4ce77-418">Si noti che hello XML tag descrizione ActiveBuildId sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="4ce77-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="4ce77-419">Se non si desidera tooset descrizione o ActiveBuildId, rimuovere i tag intero hello.</span><span class="sxs-lookup"><span data-stu-id="4ce77-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="4ce77-420">**Risposta**:</span><span class="sxs-lookup"><span data-stu-id="4ce77-420">**Response**:</span></span>

<span data-ttu-id="4ce77-421">Codice stato HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="4ce77-421">HTTP Status code: 200</span></span>

<span data-ttu-id="4ce77-422">XML OData</span><span class="sxs-lookup"><span data-stu-id="4ce77-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="4ce77-423">Note legali</span><span class="sxs-lookup"><span data-stu-id="4ce77-423">Legal</span></span>
<span data-ttu-id="4ce77-424">Questo documento viene fornito "così com'è".</span><span class="sxs-lookup"><span data-stu-id="4ce77-424">This document is provided "as-is".</span></span> <span data-ttu-id="4ce77-425">Le informazioni e le indicazioni riportate nel presente documento, inclusi URL e altri riferimenti a siti Internet, sono soggette a modifica senza preavviso.</span><span class="sxs-lookup"><span data-stu-id="4ce77-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="4ce77-426">Alcuni esempi usati in questo documento vengono forniti a scopo puramente illustrativo e sono fittizi.</span><span class="sxs-lookup"><span data-stu-id="4ce77-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="4ce77-427">Nessuna associazione reale o connessione è intenzionale o può essere desunta.</span><span class="sxs-lookup"><span data-stu-id="4ce77-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="4ce77-428">Questo documento non offrono alcun diritto legale tooany proprietà intellettuale in qualsiasi prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4ce77-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="4ce77-429">È possibile copiare e usare il presente documento per scopi interni e di riferimento.</span><span class="sxs-lookup"><span data-stu-id="4ce77-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="4ce77-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4ce77-430">© 2014 Microsoft.</span></span> <span data-ttu-id="4ce77-431">Tutti i diritti sono riservati.</span><span class="sxs-lookup"><span data-stu-id="4ce77-431">All rights reserved.</span></span> 

