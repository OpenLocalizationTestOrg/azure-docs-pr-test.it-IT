---
title: i BLOB con un indicizzatore di ricerca di Azure blob aaaIndexing CSV | Documenti Microsoft
description: Informazioni su come tooindex CSV BLOB con ricerca di Azure
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Indicizzazione di BLOB CSV con l'indicizzatore di BLOB di Ricerca di Azure
Per impostazione predefinita, l' [indicizzatore di BLOB di Ricerca di Azure](search-howto-indexing-azure-blob-storage.md) analizza i BLOB di testo delimitato come blocco singolo di testo. Tuttavia, con i BLOB contenenti dati CSV, è spesso necessario tootreat ogni riga nell'oggetto blob hello come documento separato. Ad esempio, dato hello seguente testo delimitato da: 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

potrebbe essere necessario tooparse, 2 dei documenti, ciascuno contenente i campi "tags", "Data di pubblicazione" e "id".

In questo articolo si apprenderà come tooparse CSV BLOB con un indicizzatore di ricerca di Azure blob. 

> [!IMPORTANT]
> Questa funzionalità è attualmente disponibile in anteprima. È disponibile solo nelle API REST hello utilizzando versione **2015-02-28-Preview**. Si ricordi che le API di anteprima servono per il test e la valutazione e non devono essere usate negli ambienti di produzione. 
> 
> 

## <a name="setting-up-csv-indexing"></a>Configurazione dell'indicizzazione di CSV
BLOB CSV tooindex, creare o aggiornare una definizione di indicizzatore hello `delimitedText` modalità di analisi:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Per ulteriori informazioni su hello creare API di indicizzatore, estrarre [indicizzatore creare](search-api-indexers-2015-02-28-preview.md#create-indexer).

`firstLineContainsHeaders`indica che prima riga (non vuoto) hello di ciascun blob contiene intestazioni.
Se i BLOB non contengono una riga di intestazione iniziali, le intestazioni di hello devono essere specificate nella configurazione di indicizzatore hello: 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

Attualmente è supportata solo la codifica UTF-8 hello. Inoltre, solo hello virgola `','` carattere è supportato come hello delimitatore. Se si necessita di supporto per altre codifiche o altri delimitatori, inviare commenti nel [sito UserVoice](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> Quando si usa ricerca di Azure, la modalità di analisi del testo hello delimitato si presuppone che tutti i BLOB nell'origine dati saranno CSV. Se è necessario toosupport una combinazione del volume condiviso cluster e non CSV oggetti BLOB di hello stessa origine dati, per informare Microsoft in [il sito UserVoice](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>Esempi di richiesta
Riepilogando, ecco alcuni esempi di payload completo hello. 

Origine dati: 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Indicizzatore:

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Come contribuire al miglioramento di Ricerca di Azure
Se si dispone delle richieste di funzionalità o le proprie idee per migliorare, per raggiungere toous nel nostro [sito UserVoice](https://feedback.azure.com/forums/263029-azure-search/).

