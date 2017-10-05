---
title: 'API di Machine Learning: Analisi del testo | Documentazione Microsoft'
description: "Le API di Machine Learning Microsoft per l'analisi del testo possono essere usate per analizzare testo non strutturato per attività quali l'analisi del sentiment, l'estrazione di frasi chiave, il rilevamento della lingua e il rilevamento di argomenti."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: TRUE
ms.openlocfilehash: 10eae2ff5624dcb57de1cf72b326147f35bc2a0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="ac11e-103">API di Machine Learning: Analisi del testo per analisi del sentiment, estrazione di frasi chiave, rilevamento della lingua e rilevamento di argomenti</span><span class="sxs-lookup"><span data-stu-id="ac11e-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="ac11e-104">Questa guida riguarda la versione 1 dell'API.</span><span class="sxs-lookup"><span data-stu-id="ac11e-104">This guide is for version 1 of the API.</span></span> <span data-ttu-id="ac11e-105">Per la versione 2, [**fare riferimento a questo documento**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="ac11e-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="ac11e-106">La versione 2 è ora la versione preferita di questa API.</span><span class="sxs-lookup"><span data-stu-id="ac11e-106">Version 2 is now the preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="ac11e-107">Overview</span><span class="sxs-lookup"><span data-stu-id="ac11e-107">Overview</span></span>
<span data-ttu-id="ac11e-108">L'API di analisi del testo è un gruppo di [servizi Web](https://datamarket.azure.com/dataset/amla/text-analytics) per l'analisi del testo creata con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="ac11e-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="ac11e-109">L'API può essere usata per analizzare il testo non strutturato per attività quali l'analisi del sentiment, l'estrazione di frasi chiave, il rilevamento della lingua e il rilevamento di argomenti.</span><span class="sxs-lookup"><span data-stu-id="ac11e-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="ac11e-110">Non sono necessari dati di training per usare questa API, è sufficiente inserire dati di testo.</span><span class="sxs-lookup"><span data-stu-id="ac11e-110">No training data is needed to use this API: just bring your text data.</span></span> <span data-ttu-id="ac11e-111">L'API usa tecniche di elaborazione avanzata del linguaggio naturale per fornire stime avanzate.</span><span class="sxs-lookup"><span data-stu-id="ac11e-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span></span>

<span data-ttu-id="ac11e-112">È possibile vedere il funzionamento dell'analisi del testo nel [sito di demo](https://text-analytics-demo.azurewebsites.net/), in cui si trovano anche [esempi](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) dell'implementazione di analisi del testo in C# e Python.</span><span class="sxs-lookup"><span data-stu-id="ac11e-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="ac11e-113">Analisi del sentiment</span><span class="sxs-lookup"><span data-stu-id="ac11e-113">Sentiment analysis</span></span>
<span data-ttu-id="ac11e-114">L'API restituisce un valore numerico compreso tra 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="ac11e-114">The API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="ac11e-115">I valori prossimi a 1 indicano una valutazione positiva, mentre i valori prossimi a 0 indicano una valutazione negativa.</span><span class="sxs-lookup"><span data-stu-id="ac11e-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="ac11e-116">I valori relativi alla valutazione vengono generati utilizzando tecniche di classificazione.</span><span class="sxs-lookup"><span data-stu-id="ac11e-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="ac11e-117">Le funzionalità di input per la funzione di classificazione includono n-grams, funzionalità generate da tag parti del discorso e incorporamenti di parole.</span><span class="sxs-lookup"><span data-stu-id="ac11e-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="ac11e-118">Attualmente l'inglese è l'unica lingua supportata.</span><span class="sxs-lookup"><span data-stu-id="ac11e-118">Currently, English is the only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="ac11e-119">Estrazione di frasi chiave</span><span class="sxs-lookup"><span data-stu-id="ac11e-119">Key phrase extraction</span></span>
<span data-ttu-id="ac11e-120">L'API restituisce un elenco di stringhe che indicano i punti principali di discussione nel testo di input.</span><span class="sxs-lookup"><span data-stu-id="ac11e-120">The API returns a list of strings denoting the key talking points in the input text.</span></span> <span data-ttu-id="ac11e-121">A tale scopo vengono impiegate tecniche del toolkit per l'elaborazione del linguaggio naturale sofisticato Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="ac11e-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="ac11e-122">Attualmente l'inglese è l'unica lingua supportata.</span><span class="sxs-lookup"><span data-stu-id="ac11e-122">Currently, English is the only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="ac11e-123">Rilevamento della lingua</span><span class="sxs-lookup"><span data-stu-id="ac11e-123">Language detection</span></span>
<span data-ttu-id="ac11e-124">L'API restituisce la lingua rilevata e un valore punteggio numerico compreso tra 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="ac11e-124">The API returns the detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="ac11e-125">I punteggi prossimi a 1 indicano con una certezza del 100% che la lingua identificata è true.</span><span class="sxs-lookup"><span data-stu-id="ac11e-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span></span> <span data-ttu-id="ac11e-126">È supportato un totale di 120 lingue.</span><span class="sxs-lookup"><span data-stu-id="ac11e-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="ac11e-127">Rilevamento di argomenti</span><span class="sxs-lookup"><span data-stu-id="ac11e-127">Topic detection</span></span>
<span data-ttu-id="ac11e-128">Si tratta di un'API rilasciata di recente che restituisce i primi argomenti rilevati a fronte di un elenco di record di testo inviati.</span><span class="sxs-lookup"><span data-stu-id="ac11e-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="ac11e-129">Un argomento viene identificato da una frase chiave, che può essere costituita da una o più parole correlate.</span><span class="sxs-lookup"><span data-stu-id="ac11e-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="ac11e-130">Questa API richiede un minimo di 100 record di testo da inviare, ma è progettata per rilevare gli argomenti in centinaia o addirittura migliaia di record.</span><span class="sxs-lookup"><span data-stu-id="ac11e-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="ac11e-131">Si noti che con questa API viene addebitata una transazione per ogni record di testo inviato.</span><span class="sxs-lookup"><span data-stu-id="ac11e-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="ac11e-132">L'API è progettata per funzionare al meglio con testi brevi in linguaggio naturale, ad esempio recensioni e commenti degli utenti.</span><span class="sxs-lookup"><span data-stu-id="ac11e-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="ac11e-133">Definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="ac11e-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="ac11e-134">Headers</span><span class="sxs-lookup"><span data-stu-id="ac11e-134">Headers</span></span>
<span data-ttu-id="ac11e-135">Assicurarsi di includere le intestazioni corrette nella richiesta, che dovrebbe essere come la seguente:</span><span class="sxs-lookup"><span data-stu-id="ac11e-135">Ensure that you include the correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="ac11e-136">È possibile trovare la chiave dell'account relativa al proprio account in [Azure Marketplace](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="ac11e-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="ac11e-137">Si noti che per i formati di input e output è attualmente accettato solo JSON.</span><span class="sxs-lookup"><span data-stu-id="ac11e-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="ac11e-138">XML non è supportato.</span><span class="sxs-lookup"><span data-stu-id="ac11e-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="ac11e-139">API con risposta singola</span><span class="sxs-lookup"><span data-stu-id="ac11e-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="ac11e-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="ac11e-140">GetSentiment</span></span>
<span data-ttu-id="ac11e-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="ac11e-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="ac11e-142">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="ac11e-142">**Example request**</span></span>

<span data-ttu-id="ac11e-143">Nella chiamata seguente viene richiesta l'analisi del sentiment per la frase "Hello World":</span><span class="sxs-lookup"><span data-stu-id="ac11e-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="ac11e-144">Restituirà una risposta come la seguente:</span><span class="sxs-lookup"><span data-stu-id="ac11e-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="ac11e-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="ac11e-145">GetKeyPhrases</span></span>
<span data-ttu-id="ac11e-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="ac11e-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="ac11e-147">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="ac11e-147">**Example request**</span></span>

<span data-ttu-id="ac11e-148">Nella chiamata seguente vengono richieste le frasi chiave trovate nel testo "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span><span class="sxs-lookup"><span data-stu-id="ac11e-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="ac11e-149">Restituirà una risposta come la seguente:</span><span class="sxs-lookup"><span data-stu-id="ac11e-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="ac11e-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="ac11e-150">GetLanguage</span></span>
<span data-ttu-id="ac11e-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="ac11e-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="ac11e-152">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="ac11e-152">**Example request**</span></span>

<span data-ttu-id="ac11e-153">Nella chiamata GET seguente viene richiesta la valutazione per le frasi chiave nel testo *Hello World*</span><span class="sxs-lookup"><span data-stu-id="ac11e-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="ac11e-154">Restituirà una risposta come la seguente:</span><span class="sxs-lookup"><span data-stu-id="ac11e-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="ac11e-155">**Parametri facoltativi**</span><span class="sxs-lookup"><span data-stu-id="ac11e-155">**Optional parameters**</span></span>

<span data-ttu-id="ac11e-156">`NumberOfLanguagesToDetect` è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ac11e-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="ac11e-157">Il valore predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="ac11e-157">The default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="ac11e-158">API di batch</span><span class="sxs-lookup"><span data-stu-id="ac11e-158">Batch APIs</span></span>
<span data-ttu-id="ac11e-159">Il servizio di Analisi del testo consente di eseguire estrazioni di sentiment e frase chiave in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="ac11e-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="ac11e-160">Si noti che ogni record con punteggio conta come un'unica transazione.</span><span class="sxs-lookup"><span data-stu-id="ac11e-160">Note that each of the records scored counts as one transaction.</span></span> <span data-ttu-id="ac11e-161">Quindi, ad esempio, se si richiede una valutazione per 1000 record in una singola chiamata, verranno dedotte 1000 transazioni.</span><span class="sxs-lookup"><span data-stu-id="ac11e-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="ac11e-162">Gli ID immessi nel sistema corrispondono agli ID restituiti dal sistema.</span><span class="sxs-lookup"><span data-stu-id="ac11e-162">Note that the IDs entered into the system are the IDs returned by the system.</span></span> <span data-ttu-id="ac11e-163">Il servizio Web non verifica che gli ID siano univoci.</span><span class="sxs-lookup"><span data-stu-id="ac11e-163">The web service does not check that these IDs are unique.</span></span> <span data-ttu-id="ac11e-164">È responsabilità del chiamante verificarne l'univocità.</span><span class="sxs-lookup"><span data-stu-id="ac11e-164">It is the responsibility of the caller to verify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="ac11e-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="ac11e-165">GetSentimentBatch</span></span>
<span data-ttu-id="ac11e-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="ac11e-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="ac11e-167">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="ac11e-167">**Example request**</span></span>

<span data-ttu-id="ac11e-168">Nella chiamata POST seguente vengono richieste le valutazioni delle frasi "Hello World", "Hello Foo World" e "Hello My World" nel corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="ac11e-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="ac11e-169">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="ac11e-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="ac11e-170">Nella risposta di seguito viene ottenuto l'elenco dei punteggi associati agli ID testo:</span><span class="sxs-lookup"><span data-stu-id="ac11e-170">In the response below, you get the list of scores associated with your text Ids:</span></span>

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="ac11e-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="ac11e-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="ac11e-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="ac11e-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="ac11e-173">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="ac11e-173">**Example request**</span></span>

<span data-ttu-id="ac11e-174">In questo esempio viene richiesto l'elenco delle valutazioni delle frasi chiave nei testi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac11e-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span></span> 

* <span data-ttu-id="ac11e-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span><span class="sxs-lookup"><span data-stu-id="ac11e-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="ac11e-176">"It was an amazing build conference, with very interesting talks"</span><span class="sxs-lookup"><span data-stu-id="ac11e-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="ac11e-177">"The traffic was terrible, I spent three hours going to the airport"</span><span class="sxs-lookup"><span data-stu-id="ac11e-177">"The traffic was terrible, I spent three hours going to the airport"</span></span>

<span data-ttu-id="ac11e-178">Questa richiesta viene effettuata come una chiamata POST all'endpoint:</span><span class="sxs-lookup"><span data-stu-id="ac11e-178">This request is made as a POST call to the endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="ac11e-179">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="ac11e-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

<span data-ttu-id="ac11e-180">Nella risposta di seguito viene ottenuto l'elenco delle frasi chiave associate agli ID testo:</span><span class="sxs-lookup"><span data-stu-id="ac11e-180">In the response below, you get the list of key phrases associated with your text Ids:</span></span>

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a><span data-ttu-id="ac11e-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="ac11e-181">GetLanguageBatch</span></span>

<span data-ttu-id="ac11e-182">Nella chiamata POST seguente si richiede il rilevamento delle lingua per due input di testo:</span><span class="sxs-lookup"><span data-stu-id="ac11e-182">In the POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="ac11e-183">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="ac11e-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="ac11e-184">Restituisce la risposta seguente, in cui inglese viene rilevato nel primo parametro di input e francese nel secondo input:</span><span class="sxs-lookup"><span data-stu-id="ac11e-184">This returns the following response, where English is detected in the first input and French in the second input:</span></span>

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a><span data-ttu-id="ac11e-185">API per il rilevamento di argomenti</span><span class="sxs-lookup"><span data-stu-id="ac11e-185">Topic Detection APIs</span></span>
<span data-ttu-id="ac11e-186">Si tratta di un'API rilasciata di recente che restituisce i primi argomenti rilevati a fronte di un elenco di record di testo inviati.</span><span class="sxs-lookup"><span data-stu-id="ac11e-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="ac11e-187">Un argomento viene identificato da una frase chiave, che può essere costituita da una o più parole correlate.</span><span class="sxs-lookup"><span data-stu-id="ac11e-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="ac11e-188">Si noti che con questa API viene addebitata una transazione per ogni record di testo inviato.</span><span class="sxs-lookup"><span data-stu-id="ac11e-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="ac11e-189">Questa API richiede un minimo di 100 record di testo da inviare, ma è progettata per rilevare gli argomenti in centinaia o addirittura migliaia di record.</span><span class="sxs-lookup"><span data-stu-id="ac11e-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="ac11e-190">Argomenti: processo di invio</span><span class="sxs-lookup"><span data-stu-id="ac11e-190">Topics – Submit job</span></span>
<span data-ttu-id="ac11e-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="ac11e-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="ac11e-192">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="ac11e-192">**Example request**</span></span>

<span data-ttu-id="ac11e-193">Nella chiamata POST riportata di seguito vengono richiesti gli argomenti per un insieme di 100 articoli. Vengono visualizzati il primo e l'ultimo articolo di input e sono incluse due frasi di stop.</span><span class="sxs-lookup"><span data-stu-id="ac11e-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="ac11e-194">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="ac11e-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="ac11e-195">Nella risposta seguente si ottiene l'ID processo (JobId) per il processo inviato:</span><span class="sxs-lookup"><span data-stu-id="ac11e-195">In the response below, you get the JobId for the submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="ac11e-196">Un elenco di parole singole o di frasi costituite da più parole che non dovrebbero essere restituite come argomenti.</span><span class="sxs-lookup"><span data-stu-id="ac11e-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="ac11e-197">Può essere usato per filtrare argomenti molto generici.</span><span class="sxs-lookup"><span data-stu-id="ac11e-197">Can be used to filter out very generic topics.</span></span> <span data-ttu-id="ac11e-198">Ad esempio, in un set di dati riguardante recensioni di alberghi, "albergo" e "ostello" possono esser frasi di stop sensibili.</span><span class="sxs-lookup"><span data-stu-id="ac11e-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="ac11e-199">Argomenti: polling risultati processo</span><span class="sxs-lookup"><span data-stu-id="ac11e-199">Topics – Poll for job results</span></span>
<span data-ttu-id="ac11e-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="ac11e-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="ac11e-201">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="ac11e-201">**Example request**</span></span>

<span data-ttu-id="ac11e-202">Passare l'ID processo (JobId) restituito al passaggio relativo al processo di invio per recuperare i risultati.</span><span class="sxs-lookup"><span data-stu-id="ac11e-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span></span> <span data-ttu-id="ac11e-203">È consigliabile chiamare questo endpoint ogni minuto, fino a quando nella risposta viene visualizzato Status='Complete'.</span><span class="sxs-lookup"><span data-stu-id="ac11e-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span></span> <span data-ttu-id="ac11e-204">Per completare un processo sono necessari circa 10 minuti. Nel caso di processi con diverse migliaia di record, può essere necessario un periodo di tempo maggiore.</span><span class="sxs-lookup"><span data-stu-id="ac11e-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="ac11e-205">Durante l'elaborazione, la risposta avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ac11e-205">While it is processing, the response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="ac11e-206">L'API restituisce un output in formato JSON, come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ac11e-206">The API returns output in JSON format in the following format:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


<span data-ttu-id="ac11e-207">Le proprietà di ciascuna parte della risposta sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac11e-207">The properties for each part of the response are as follows:</span></span>

<span data-ttu-id="ac11e-208">**Proprietà TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="ac11e-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="ac11e-209">Chiave</span><span class="sxs-lookup"><span data-stu-id="ac11e-209">Key</span></span> | <span data-ttu-id="ac11e-210">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ac11e-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ac11e-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="ac11e-211">TopicId</span></span> |<span data-ttu-id="ac11e-212">Identificatore univoco di ogni argomento.</span><span class="sxs-lookup"><span data-stu-id="ac11e-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="ac11e-213">Score</span><span class="sxs-lookup"><span data-stu-id="ac11e-213">Score</span></span> |<span data-ttu-id="ac11e-214">Numero di record assegnati all'argomento.</span><span class="sxs-lookup"><span data-stu-id="ac11e-214">Count of records assigned to topic.</span></span> |
| <span data-ttu-id="ac11e-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="ac11e-215">KeyPhrase</span></span> |<span data-ttu-id="ac11e-216">Parola o frase di riepilogo dell'argomento.</span><span class="sxs-lookup"><span data-stu-id="ac11e-216">A summarizing word or phrase for the topic.</span></span> <span data-ttu-id="ac11e-217">Può essere costituita da una o più parole.</span><span class="sxs-lookup"><span data-stu-id="ac11e-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="ac11e-218">**Proprietà TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="ac11e-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="ac11e-219">Chiave</span><span class="sxs-lookup"><span data-stu-id="ac11e-219">Key</span></span> | <span data-ttu-id="ac11e-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ac11e-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ac11e-221">ID</span><span class="sxs-lookup"><span data-stu-id="ac11e-221">Id</span></span> |<span data-ttu-id="ac11e-222">Identificatore del record.</span><span class="sxs-lookup"><span data-stu-id="ac11e-222">Identifier for the record.</span></span> <span data-ttu-id="ac11e-223">Equivale all'ID incluso nell'input.</span><span class="sxs-lookup"><span data-stu-id="ac11e-223">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="ac11e-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="ac11e-224">TopicId</span></span> |<span data-ttu-id="ac11e-225">ID dell'argomento a cui sono stati assegnati i record.</span><span class="sxs-lookup"><span data-stu-id="ac11e-225">The topic ID which the record has been assigned to.</span></span> |
| <span data-ttu-id="ac11e-226">Distance</span><span class="sxs-lookup"><span data-stu-id="ac11e-226">Distance</span></span> |<span data-ttu-id="ac11e-227">Probabilità che il record appartenga all'argomento.</span><span class="sxs-lookup"><span data-stu-id="ac11e-227">Confidence that the record belongs to the topic.</span></span> <span data-ttu-id="ac11e-228">Un valore vicino a zero indica una probabilità elevata.</span><span class="sxs-lookup"><span data-stu-id="ac11e-228">Distance closer to zero indicates higher confidence.</span></span> |

