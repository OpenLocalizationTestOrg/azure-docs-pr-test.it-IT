---
title: BLOB JSON aaaIndexing con un indicizzatore di ricerca di Azure blob
description: Indicizzazione di BLOB JSON con l'indicizzatore di BLOB di Ricerca di Azure
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Indicizzazione di BLOB JSON con l'indicizzatore di BLOB di Ricerca di Azure
Questo articolo illustra come tooconfigure ricerca di Azure blob indicizzatore tooextract strutturati il contenuto di blob che contengono JSON.

## <a name="scenarios"></a>Scenari
Per impostazione predefinita, l' [indicizzatore BLOB di Ricerca di Azure](search-howto-indexing-azure-blob-storage.md) analizza i BLOB di tipo JSON come blocco singolo di testo. Spesso, è necessario struttura hello toopreserve di documenti JSON. Si consideri ad esempio documento JSON hello

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

è possibile tooparse in una ricerca di Azure il documento con "text", "Data di pubblicazione" e "tag" campi.

In alternativa, quando il BLOB contiene un **matrice di oggetti JSON**, si consiglia di ogni elemento della matrice di hello toobecome un documento di ricerca di Azure separato. Ad esempio, considerato un BLOB con questo JSON:  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

È possibile popolare l'indice di Ricerca di Azure con 3 documenti separati, ognuno con i campi "id" e "text".

> [!IMPORTANT]
> Matrice JSON Hello la funzionalità di analisi è attualmente in anteprima. È disponibile solo nelle API REST hello utilizzando versione **2015-02-28-Preview**. Si ricordi che le API di anteprima servono per il test e la valutazione e non devono essere usate negli ambienti di produzione.
>
>

## <a name="setting-up-json-indexing"></a>Configurazione dell'indicizzazione JSON
L'indicizzazione BLOB JSON è l'estrazione di documento normale toohello simile. Creare innanzitutto l'origine dati hello esattamente come di consueto: 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

Quindi creare l'indice di ricerca di destinazione hello se non si dispone già uno. 

Infine, creare un indicizzatore e impostare hello `parsingMode` parametro troppo`json` (tooindex ogni blob come un singolo documento) o `jsonArray` (se il BLOB di contenere matrici JSON, sono necessari ogni elemento di una matrice di toobe trattato come documento separato):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

Se necessario, utilizzare **campo mapping** toopick hello le proprietà di hello origine JSON documento utilizzato toopopulate l'indice di ricerca di destinazione, come illustrato nella sezione successiva hello.

> [!IMPORTANT]
> Quando si usa la modalità di analisi `json` o `jsonArray`, Ricerca di Azure presuppone che tutti i BLOB nell'origine dati siano di tipo JSON. Se è necessario toosupport una combinazione di JSON e sui blob non JSON in hello stessa origine dati, informare Microsoft in [il sito UserVoice](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>Utilizzo di documenti ricerca toobuild i mapping di campo
Ricerca di Azure non può attualmente indicizzare direttamente documenti JSON arbitrari, perché supporta solo tipi di dati primitivi, matrici di stringhe e punti GeoJSON. Tuttavia, è possibile utilizzare **campo mapping** toopick parte il file JSON di documenti e "accuratezza" li in campi di livello superiore del documento di ricerca hello. vedere toolearn sui concetti di base con i mapping di campo [mapping dei campi dell'indicizzatore di ricerca di Azure bridge differenze hello tra origini dati e gli indici di ricerca](search-indexer-field-mappings.md).

Confermata documento JSON di esempio tooour:

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Si supponga che si dispone di un indice di ricerca con hello seguenti campi: `text` di tipo `Edm.String`, `date` di tipo `Edm.DateTimeOffset`, e `tags` di tipo `Collection(Edm.String)`. toomap il file JSON in hello forma desiderata, utilizzare hello mapping dei campi seguenti:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Hello nomi dei campi di origine nei mapping hello vengono specificati mediante hello [puntatore JSON](http://tools.ietf.org/html/rfc6901) notazione. Iniziare con una radice di toohello barra toorefer del documento JSON, quindi selezionare proprietà hello desiderato (livello arbitrario di annidamento) usando il percorso di barra separati in avanti.

È anche possibile fare riferimento a elementi di matrice tooindividual usando un indice in base zero. Primo elemento hello toopick della matrice "tags" hello da hello sopra riportato, ad esempio, utilizzare il mapping di un campo simile al seguente:

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Se un nome di campo di origine in un percorso di mapping del campo fa riferimento a proprietà tooa che non esiste in JSON, tale mapping verrà ignorato senza errori. Ciò consente di supportare documenti con schemi diversi, ovvero un caso di utilizzo comune. Poiché non esiste alcuna convalida, è necessario tootake errori di digitazione tooavoid attenzione nella specifica dei mapping campi.
>
>

Se i documenti JSON contengono solo semplici proprietà di livello superiore, è possibile che i mapping dei campi non siano necessari. Ad esempio, se il file JSON è simile, questa proprietà di primo livello hello "text", "Data di pubblicazione" e "tag" è mappata direttamente toohello campi corrispondenti nell'indice di ricerca hello:

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Ecco un payload di indicizzatore completo con mapping dei campi:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>Indicizzazione delle matrici JSON annidate
Cosa accade se si desidera tooindex una matrice di oggetti JSON, ma tale matrice è annidato in un punto qualsiasi nel documento hello? È possibile scegliere quali proprietà contiene la matrice di hello utilizzando hello `documentRoot` proprietà di configurazione. Ad esempio, se i BLOB sono simili a questo:

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

Utilizzare questa matrice hello tooindex di configurazione contenuta in hello `level2` proprietà:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Come contribuire al miglioramento di Ricerca di Azure
Se si dispone delle richieste di funzionalità o le proprie idee per migliorare, raggiungere toous nel nostro [sito UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
