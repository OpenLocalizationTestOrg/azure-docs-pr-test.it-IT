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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>API di Machine Learning: Analisi del testo per analisi del sentiment, estrazione di frasi chiave, rilevamento della lingua e rilevamento di argomenti
> [!NOTE]
> Questa guida è per la versione 1 di hello API. Per la versione 2, [ **riferimento documento toothis**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Versione 2 è ora versione preferita di hello di questa API.
> 
> 

## <a name="overview"></a>Panoramica
Hello API Analitica del testo è una famiglia di analitica testo [servizi web](https://datamarket.azure.com/dataset/amla/text-analytics) compilati con Azure Machine Learning. Hello API può essere utilizzato tooanalyze testo non strutturato per attività quali l'analisi del sentiment, estrazione di frasi chiave, il rilevamento della lingua e il rilevamento di argomento. Nessun dati di training necessari toouse questa API: importare solo i dati di testo. Questa API viene utilizzato il linguaggio naturale avanzato elaborazione tecniche toodeliver nelle stime di classe.

È possibile visualizzare analitica di testo nell'azione nel nostro [sito demo del](https://text-analytics-demo.azurewebsites.net/), in cui si trovano anche [esempi](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) sull'analitica testo tooimplement in c# e Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Analisi del sentiment
Hello API restituisce un valore numerico compreso tra 0 e 1. Punteggi Chiudi too1 indicare sentiment positivo, mentre punteggi Chiudi too0 indicare sentiment negativo. I valori relativi alla valutazione vengono generati utilizzando tecniche di classificazione. Hello le funzionalità di input toohello classificazione includono n-grammi, funzionalità generata dal tag di parti del discorso e incorporamenti di word. Attualmente, l'inglese è hello solo lingua supportata.

## <a name="key-phrase-extraction"></a>Estrazione di frasi chiave
Hello API restituisce un elenco di stringhe indicano punti talking chiave hello nel testo di input hello. A tale scopo vengono impiegate tecniche del toolkit per l'elaborazione del linguaggio naturale sofisticato Microsoft Office. Attualmente, l'inglese è hello solo lingua supportata.

## <a name="language-detection"></a>Rilevamento della lingua
Hello API restituisce hello rilevato lingua e un valore numerico compreso tra 0 e 1. Punteggi Chiudi too1 indicare 100% certezza che il linguaggio di hello identificato è true. È supportato un totale di 120 lingue.

## <a name="topic-detection"></a>Rilevamento di argomenti
Si tratta di un'API rilasciata di recente, che restituisce hello argomenti rilevato superiore per un elenco di record di testo inviato. Un argomento viene identificato da una frase chiave, che può essere costituita da una o più parole correlate. Questa API richiede un minimo di 100 testo registra toobe inviato, ma è progettata toodetect argomenti centinaia toothousands di record. Si noti che con questa API viene addebitata una transazione per ogni record di testo inviato. API Hello è toowork progettato anche per breve, personale scritti testo, ad esempio revisioni e commenti degli utenti.

- - -
## <a name="api-definition"></a>Definizione dell'API
### <a name="headers"></a>Headers
Assicurarsi di includere le intestazioni corretto hello nella richiesta, che dovrebbe essere come segue:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

È possibile trovare la chiave dell'account dal tuo account in hello [Azure Datamarket](https://datamarket.azure.com/account/keys). Si noti che per i formati di input e output è attualmente accettato solo JSON. XML non è supportato.

- - -
## <a name="single-response-apis"></a>API con risposta singola
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Richiesta di esempio**

Nella chiamata hello riportato di seguito, ti chiediamo di analisi del sentiment per frase hello "Hello World":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Restituirà una risposta come la seguente:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Richiesta di esempio**

Nella chiamata hello riportato di seguito, ti chiediamo di frasi chiave hello trovato nel testo hello "È un ottimo toostay hotel, con la decorazione univoca e descrittivo personale":

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Restituirà una risposta come la seguente:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Richiesta di esempio**

Nella chiamata GET hello riportato di seguito, ti chiediamo sentiment hello per ottenere frasi chiave in testo hello hello *Hello World*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Restituirà una risposta come la seguente:

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**Parametri facoltativi**

`NumberOfLanguagesToDetect` è un parametro facoltativo. Hello predefinito è 1.

- - -
## <a name="batch-apis"></a>API di batch
servizio Analitica testo Hello consente toodo sentiment e le estrazioni di frasi chiave in modalità batch. Si noti che ogni record hello con punteggio conteggi come un'unica transazione. Quindi, ad esempio, se si richiede una valutazione per 1000 record in una singola chiamata, verranno dedotte 1000 transazioni.

Si noti che gli ID hello immesso nel sistema di hello sono ID hello restituiti dal sistema hello. servizio web Hello non verifica che questi ID siano univoci. È responsabilità di hello di univocità di tooverify hello chiamante. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Richiesta di esempio**

Hello POST chiamare seguito, ti chiediamo per i rispettivi hello di frasi hello "Hello World", "Hello World Foo" e "Hello My World" nel corpo di hello di hello richiesta:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Corpo della richiesta:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

Nella risposta hello riportata di seguito, viene visualizzato l'elenco di hello dei punteggi associata con l'ID di testo:

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
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Richiesta di esempio**

In questo esempio, ti chiediamo per elenco hello dei rispettivi per ottenere frasi chiave hello in hello testi seguenti: 

* "È un ottimo toostay hotel, con la decorazione univoca e descrittivo personale"
* "It was an amazing build conference, with very interesting talks"
* "traffico hello terribile, ho trascorso tre ore prevede aeroporto toohello"

Questa richiesta viene eseguita come un endpoint di toohello chiamata POST:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Corpo della richiesta:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

Nella risposta hello riportata di seguito, ottenere l'elenco di hello di frasi chiave associate al testo ID:

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
### <a name="getlanguagebatch"></a>GetLanguageBatch

Nella chiamata POST hello riportato di seguito, ti chiediamo il rilevamento di due input di testo:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Corpo della richiesta:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Restituisce hello seguente risposta, in cui in lingua inglese viene rilevato in francese e hello primo input del secondo input hello:

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
## <a name="topic-detection-apis"></a>API per il rilevamento di argomenti
Si tratta di un'API rilasciata di recente, che restituisce hello argomenti rilevato superiore per un elenco di record di testo inviato. Un argomento viene identificato da una frase chiave, che può essere costituita da una o più parole correlate. Si noti che con questa API viene addebitata una transazione per ogni record di testo inviato.

Questa API richiede un minimo di 100 testo registra toobe inviato, ma è progettata toodetect argomenti centinaia toothousands di record.

### <a name="topics--submit-job"></a>Argomenti: processo di invio
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Richiesta di esempio**

Nella chiamata POST hello riportato di seguito, ti chiediamo di argomenti per una serie di 100 articoli, in cui hello e cognome di input vengono visualizzati gli articoli e sono inclusi due StopPhrases.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Corpo della richiesta:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

Nella risposta hello riportata di seguito, si otterrà hello JobId per processo inviato hello:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Un elenco di parole singole o di frasi costituite da più parole che non dovrebbero essere restituite come argomenti. Può essere utilizzato toofilter gli argomenti molto generici. Ad esempio, in un set di dati riguardante recensioni di alberghi, "albergo" e "ostello" possono esser frasi di stop sensibili.  

### <a name="topics--poll-for-job-results"></a>Argomenti: polling risultati processo
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Richiesta di esempio**

Passare hello che JobID restituito da hello ' Invia ' passaggio toofetch hello risultati. Si consiglia di chiamare questo endpoint ogni minuto fino a quando lo stato = 'Completato' nella risposta hello. Saranno necessari circa 10 minuti per toocomplete un processo, o per i processi con molte migliaia di record.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Durante l'elaborazione, hello risposta sarà come segue:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Hello API restituisce output in formato JSON in hello seguente formato:

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


proprietà Hello per ogni parte della risposta hello sono i seguenti:

**Proprietà TopicInfo**

| Chiave | Descrizione |
|:--- |:--- |
| TopicId |Identificatore univoco di ogni argomento. |
| Score |Numero di record assegnati tootopic. |
| KeyPhrase |Una parola o frase per argomento hello riepilogati. Può essere costituita da una o più parole. |

**Proprietà TopicAssignment**

| Chiave | Descrizione |
|:--- |:--- |
| ID |Identificatore hello record. Equivale a ID toohello inclusi nell'input hello. |
| TopicId |ID argomento Hello record hello è stato assegnato a. |
| Distance |Confidenza record hello appartiene toohello argomento. Distanza più vicino toozero indica una probabilità superiore. |

