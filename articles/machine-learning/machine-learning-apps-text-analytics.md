---
title: 'API di Machine Learning: Analisi del testo | Documentazione Microsoft'
description: "API di Microsoft Machine Learning testo Analitica può essere utilizzato tooanalyze testo non strutturato per l'analisi del sentiment, estrazione di frasi chiave, il rilevamento della lingua e il rilevamento di argomento."
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
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="16e40-103">API di Machine Learning: Analisi del testo per analisi del sentiment, estrazione di frasi chiave, rilevamento della lingua e rilevamento di argomenti</span><span class="sxs-lookup"><span data-stu-id="16e40-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="16e40-104">Questa guida è per la versione 1 di hello API.</span><span class="sxs-lookup"><span data-stu-id="16e40-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="16e40-105">Per la versione 2, [ **riferimento documento toothis**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="16e40-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="16e40-106">Versione 2 è ora versione preferita di hello di questa API.</span><span class="sxs-lookup"><span data-stu-id="16e40-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="16e40-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="16e40-107">Overview</span></span>
<span data-ttu-id="16e40-108">Hello API Analitica del testo è una famiglia di analitica testo [servizi web](https://datamarket.azure.com/dataset/amla/text-analytics) compilati con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="16e40-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="16e40-109">Hello API può essere utilizzato tooanalyze testo non strutturato per attività quali l'analisi del sentiment, estrazione di frasi chiave, il rilevamento della lingua e il rilevamento di argomento.</span><span class="sxs-lookup"><span data-stu-id="16e40-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="16e40-110">Nessun dati di training necessari toouse questa API: importare solo i dati di testo.</span><span class="sxs-lookup"><span data-stu-id="16e40-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="16e40-111">Questa API viene utilizzato il linguaggio naturale avanzato elaborazione tecniche toodeliver nelle stime di classe.</span><span class="sxs-lookup"><span data-stu-id="16e40-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="16e40-112">È possibile visualizzare analitica di testo nell'azione nel nostro [sito demo del](https://text-analytics-demo.azurewebsites.net/), in cui si trovano anche [esempi](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) sull'analitica testo tooimplement in c# e Python.</span><span class="sxs-lookup"><span data-stu-id="16e40-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="16e40-113">Analisi del sentiment</span><span class="sxs-lookup"><span data-stu-id="16e40-113">Sentiment analysis</span></span>
<span data-ttu-id="16e40-114">Hello API restituisce un valore numerico compreso tra 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="16e40-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="16e40-115">Punteggi Chiudi too1 indicare sentiment positivo, mentre punteggi Chiudi too0 indicare sentiment negativo.</span><span class="sxs-lookup"><span data-stu-id="16e40-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="16e40-116">I valori relativi alla valutazione vengono generati utilizzando tecniche di classificazione.</span><span class="sxs-lookup"><span data-stu-id="16e40-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="16e40-117">Hello le funzionalità di input toohello classificazione includono n-grammi, funzionalità generata dal tag di parti del discorso e incorporamenti di word.</span><span class="sxs-lookup"><span data-stu-id="16e40-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="16e40-118">Attualmente, l'inglese è hello solo lingua supportata.</span><span class="sxs-lookup"><span data-stu-id="16e40-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="16e40-119">Estrazione di frasi chiave</span><span class="sxs-lookup"><span data-stu-id="16e40-119">Key phrase extraction</span></span>
<span data-ttu-id="16e40-120">Hello API restituisce un elenco di stringhe indicano punti talking chiave hello nel testo di input hello.</span><span class="sxs-lookup"><span data-stu-id="16e40-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="16e40-121">A tale scopo vengono impiegate tecniche del toolkit per l'elaborazione del linguaggio naturale sofisticato Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="16e40-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="16e40-122">Attualmente, l'inglese è hello solo lingua supportata.</span><span class="sxs-lookup"><span data-stu-id="16e40-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="16e40-123">Rilevamento della lingua</span><span class="sxs-lookup"><span data-stu-id="16e40-123">Language detection</span></span>
<span data-ttu-id="16e40-124">Hello API restituisce hello rilevato lingua e un valore numerico compreso tra 0 e 1.</span><span class="sxs-lookup"><span data-stu-id="16e40-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="16e40-125">Punteggi Chiudi too1 indicare 100% certezza che il linguaggio di hello identificato è true.</span><span class="sxs-lookup"><span data-stu-id="16e40-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="16e40-126">È supportato un totale di 120 lingue.</span><span class="sxs-lookup"><span data-stu-id="16e40-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="16e40-127">Rilevamento di argomenti</span><span class="sxs-lookup"><span data-stu-id="16e40-127">Topic detection</span></span>
<span data-ttu-id="16e40-128">Si tratta di un'API rilasciata di recente, che restituisce hello argomenti rilevato superiore per un elenco di record di testo inviato.</span><span class="sxs-lookup"><span data-stu-id="16e40-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="16e40-129">Un argomento viene identificato da una frase chiave, che può essere costituita da una o più parole correlate.</span><span class="sxs-lookup"><span data-stu-id="16e40-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="16e40-130">Questa API richiede un minimo di 100 testo registra toobe inviato, ma è progettata toodetect argomenti centinaia toothousands di record.</span><span class="sxs-lookup"><span data-stu-id="16e40-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="16e40-131">Si noti che con questa API viene addebitata una transazione per ogni record di testo inviato.</span><span class="sxs-lookup"><span data-stu-id="16e40-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="16e40-132">API Hello è toowork progettato anche per breve, personale scritti testo, ad esempio revisioni e commenti degli utenti.</span><span class="sxs-lookup"><span data-stu-id="16e40-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="16e40-133">Definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="16e40-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="16e40-134">Headers</span><span class="sxs-lookup"><span data-stu-id="16e40-134">Headers</span></span>
<span data-ttu-id="16e40-135">Assicurarsi di includere le intestazioni corretto hello nella richiesta, che dovrebbe essere come segue:</span><span class="sxs-lookup"><span data-stu-id="16e40-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="16e40-136">È possibile trovare la chiave dell'account dal tuo account in hello [Azure Datamarket](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="16e40-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="16e40-137">Si noti che per i formati di input e output è attualmente accettato solo JSON.</span><span class="sxs-lookup"><span data-stu-id="16e40-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="16e40-138">XML non è supportato.</span><span class="sxs-lookup"><span data-stu-id="16e40-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="16e40-139">API con risposta singola</span><span class="sxs-lookup"><span data-stu-id="16e40-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="16e40-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="16e40-140">GetSentiment</span></span>
<span data-ttu-id="16e40-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="16e40-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="16e40-142">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="16e40-142">**Example request**</span></span>

<span data-ttu-id="16e40-143">Nella chiamata hello riportato di seguito, ti chiediamo di analisi del sentiment per frase hello "Hello World":</span><span class="sxs-lookup"><span data-stu-id="16e40-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="16e40-144">Restituirà una risposta come la seguente:</span><span class="sxs-lookup"><span data-stu-id="16e40-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="16e40-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="16e40-145">GetKeyPhrases</span></span>
<span data-ttu-id="16e40-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="16e40-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="16e40-147">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="16e40-147">**Example request**</span></span>

<span data-ttu-id="16e40-148">Nella chiamata hello riportato di seguito, ti chiediamo di frasi chiave hello trovato nel testo hello "È un ottimo toostay hotel, con la decorazione univoca e descrittivo personale":</span><span class="sxs-lookup"><span data-stu-id="16e40-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="16e40-149">Restituirà una risposta come la seguente:</span><span class="sxs-lookup"><span data-stu-id="16e40-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="16e40-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="16e40-150">GetLanguage</span></span>
<span data-ttu-id="16e40-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="16e40-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="16e40-152">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="16e40-152">**Example request**</span></span>

<span data-ttu-id="16e40-153">Nella chiamata GET hello riportato di seguito, ti chiediamo sentiment hello per ottenere frasi chiave in testo hello hello *Hello World*</span><span class="sxs-lookup"><span data-stu-id="16e40-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="16e40-154">Restituirà una risposta come la seguente:</span><span class="sxs-lookup"><span data-stu-id="16e40-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="16e40-155">**Parametri facoltativi**</span><span class="sxs-lookup"><span data-stu-id="16e40-155">**Optional parameters**</span></span>

<span data-ttu-id="16e40-156">`NumberOfLanguagesToDetect` è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="16e40-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="16e40-157">Hello predefinito è 1.</span><span class="sxs-lookup"><span data-stu-id="16e40-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="16e40-158">API di batch</span><span class="sxs-lookup"><span data-stu-id="16e40-158">Batch APIs</span></span>
<span data-ttu-id="16e40-159">servizio Analitica testo Hello consente toodo sentiment e le estrazioni di frasi chiave in modalità batch.</span><span class="sxs-lookup"><span data-stu-id="16e40-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="16e40-160">Si noti che ogni record hello con punteggio conteggi come un'unica transazione.</span><span class="sxs-lookup"><span data-stu-id="16e40-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="16e40-161">Quindi, ad esempio, se si richiede una valutazione per 1000 record in una singola chiamata, verranno dedotte 1000 transazioni.</span><span class="sxs-lookup"><span data-stu-id="16e40-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="16e40-162">Si noti che gli ID hello immesso nel sistema di hello sono ID hello restituiti dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="16e40-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="16e40-163">servizio web Hello non verifica che questi ID siano univoci.</span><span class="sxs-lookup"><span data-stu-id="16e40-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="16e40-164">È responsabilità di hello di univocità di tooverify hello chiamante.</span><span class="sxs-lookup"><span data-stu-id="16e40-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="16e40-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="16e40-165">GetSentimentBatch</span></span>
<span data-ttu-id="16e40-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="16e40-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="16e40-167">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="16e40-167">**Example request**</span></span>

<span data-ttu-id="16e40-168">Hello POST chiamare seguito, ti chiediamo per i rispettivi hello di frasi hello "Hello World", "Hello World Foo" e "Hello My World" nel corpo di hello di hello richiesta:</span><span class="sxs-lookup"><span data-stu-id="16e40-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="16e40-169">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="16e40-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="16e40-170">Nella risposta hello riportata di seguito, viene visualizzato l'elenco di hello dei punteggi associata con l'ID di testo:</span><span class="sxs-lookup"><span data-stu-id="16e40-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="16e40-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="16e40-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="16e40-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="16e40-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="16e40-173">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="16e40-173">**Example request**</span></span>

<span data-ttu-id="16e40-174">In questo esempio, ti chiediamo per elenco hello dei rispettivi per ottenere frasi chiave hello in hello testi seguenti:</span><span class="sxs-lookup"><span data-stu-id="16e40-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="16e40-175">"È un ottimo toostay hotel, con la decorazione univoca e descrittivo personale"</span><span class="sxs-lookup"><span data-stu-id="16e40-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="16e40-176">"It was an amazing build conference, with very interesting talks"</span><span class="sxs-lookup"><span data-stu-id="16e40-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="16e40-177">"traffico hello terribile, ho trascorso tre ore prevede aeroporto toohello"</span><span class="sxs-lookup"><span data-stu-id="16e40-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="16e40-178">Questa richiesta viene eseguita come un endpoint di toohello chiamata POST:</span><span class="sxs-lookup"><span data-stu-id="16e40-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="16e40-179">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="16e40-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="16e40-180">Nella risposta hello riportata di seguito, ottenere l'elenco di hello di frasi chiave associate al testo ID:</span><span class="sxs-lookup"><span data-stu-id="16e40-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="16e40-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="16e40-181">GetLanguageBatch</span></span>

<span data-ttu-id="16e40-182">Nella chiamata POST hello riportato di seguito, ti chiediamo il rilevamento di due input di testo:</span><span class="sxs-lookup"><span data-stu-id="16e40-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="16e40-183">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="16e40-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="16e40-184">Restituisce hello seguente risposta, in cui in lingua inglese viene rilevato in francese e hello primo input del secondo input hello:</span><span class="sxs-lookup"><span data-stu-id="16e40-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="16e40-185">API per il rilevamento di argomenti</span><span class="sxs-lookup"><span data-stu-id="16e40-185">Topic Detection APIs</span></span>
<span data-ttu-id="16e40-186">Si tratta di un'API rilasciata di recente, che restituisce hello argomenti rilevato superiore per un elenco di record di testo inviato.</span><span class="sxs-lookup"><span data-stu-id="16e40-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="16e40-187">Un argomento viene identificato da una frase chiave, che può essere costituita da una o più parole correlate.</span><span class="sxs-lookup"><span data-stu-id="16e40-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="16e40-188">Si noti che con questa API viene addebitata una transazione per ogni record di testo inviato.</span><span class="sxs-lookup"><span data-stu-id="16e40-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="16e40-189">Questa API richiede un minimo di 100 testo registra toobe inviato, ma è progettata toodetect argomenti centinaia toothousands di record.</span><span class="sxs-lookup"><span data-stu-id="16e40-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="16e40-190">Argomenti: processo di invio</span><span class="sxs-lookup"><span data-stu-id="16e40-190">Topics – Submit job</span></span>
<span data-ttu-id="16e40-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="16e40-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="16e40-192">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="16e40-192">**Example request**</span></span>

<span data-ttu-id="16e40-193">Nella chiamata POST hello riportato di seguito, ti chiediamo di argomenti per una serie di 100 articoli, in cui hello e cognome di input vengono visualizzati gli articoli e sono inclusi due StopPhrases.</span><span class="sxs-lookup"><span data-stu-id="16e40-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="16e40-194">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="16e40-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="16e40-195">Nella risposta hello riportata di seguito, si otterrà hello JobId per processo inviato hello:</span><span class="sxs-lookup"><span data-stu-id="16e40-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="16e40-196">Un elenco di parole singole o di frasi costituite da più parole che non dovrebbero essere restituite come argomenti.</span><span class="sxs-lookup"><span data-stu-id="16e40-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="16e40-197">Può essere utilizzato toofilter gli argomenti molto generici.</span><span class="sxs-lookup"><span data-stu-id="16e40-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="16e40-198">Ad esempio, in un set di dati riguardante recensioni di alberghi, "albergo" e "ostello" possono esser frasi di stop sensibili.</span><span class="sxs-lookup"><span data-stu-id="16e40-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="16e40-199">Argomenti: polling risultati processo</span><span class="sxs-lookup"><span data-stu-id="16e40-199">Topics – Poll for job results</span></span>
<span data-ttu-id="16e40-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="16e40-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="16e40-201">**Richiesta di esempio**</span><span class="sxs-lookup"><span data-stu-id="16e40-201">**Example request**</span></span>

<span data-ttu-id="16e40-202">Passare hello che JobID restituito da hello ' Invia ' passaggio toofetch hello risultati.</span><span class="sxs-lookup"><span data-stu-id="16e40-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="16e40-203">Si consiglia di chiamare questo endpoint ogni minuto fino a quando lo stato = 'Completato' nella risposta hello.</span><span class="sxs-lookup"><span data-stu-id="16e40-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="16e40-204">Saranno necessari circa 10 minuti per toocomplete un processo, o per i processi con molte migliaia di record.</span><span class="sxs-lookup"><span data-stu-id="16e40-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="16e40-205">Durante l'elaborazione, hello risposta sarà come segue:</span><span class="sxs-lookup"><span data-stu-id="16e40-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="16e40-206">Hello API restituisce output in formato JSON in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="16e40-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="16e40-207">proprietà Hello per ogni parte della risposta hello sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="16e40-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="16e40-208">**Proprietà TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="16e40-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="16e40-209">Chiave</span><span class="sxs-lookup"><span data-stu-id="16e40-209">Key</span></span> | <span data-ttu-id="16e40-210">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16e40-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="16e40-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="16e40-211">TopicId</span></span> |<span data-ttu-id="16e40-212">Identificatore univoco di ogni argomento.</span><span class="sxs-lookup"><span data-stu-id="16e40-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="16e40-213">Score</span><span class="sxs-lookup"><span data-stu-id="16e40-213">Score</span></span> |<span data-ttu-id="16e40-214">Numero di record assegnati tootopic.</span><span class="sxs-lookup"><span data-stu-id="16e40-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="16e40-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="16e40-215">KeyPhrase</span></span> |<span data-ttu-id="16e40-216">Una parola o frase per argomento hello riepilogati.</span><span class="sxs-lookup"><span data-stu-id="16e40-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="16e40-217">Può essere costituita da una o più parole.</span><span class="sxs-lookup"><span data-stu-id="16e40-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="16e40-218">**Proprietà TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="16e40-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="16e40-219">Chiave</span><span class="sxs-lookup"><span data-stu-id="16e40-219">Key</span></span> | <span data-ttu-id="16e40-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="16e40-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="16e40-221">ID</span><span class="sxs-lookup"><span data-stu-id="16e40-221">Id</span></span> |<span data-ttu-id="16e40-222">Identificatore hello record.</span><span class="sxs-lookup"><span data-stu-id="16e40-222">Identifier for hello record.</span></span> <span data-ttu-id="16e40-223">Equivale a ID toohello inclusi nell'input hello.</span><span class="sxs-lookup"><span data-stu-id="16e40-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="16e40-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="16e40-224">TopicId</span></span> |<span data-ttu-id="16e40-225">ID argomento Hello record hello è stato assegnato a.</span><span class="sxs-lookup"><span data-stu-id="16e40-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="16e40-226">Distance</span><span class="sxs-lookup"><span data-stu-id="16e40-226">Distance</span></span> |<span data-ttu-id="16e40-227">Confidenza record hello appartiene toohello argomento.</span><span class="sxs-lookup"><span data-stu-id="16e40-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="16e40-228">Distanza più vicino toozero indica una probabilità superiore.</span><span class="sxs-lookup"><span data-stu-id="16e40-228">Distance closer toozero indicates higher confidence.</span></span> |

