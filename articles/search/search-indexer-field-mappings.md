---
title: mapping di aaaField negli indicizzatori di ricerca di Azure
description: Configurare ricerca di Azure indicizzatore campo mapping tooaccount le differenze in rappresentazioni di dati e i nomi di campo
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Mapping dei campi negli indicizzatori di Ricerca di Azure
Quando si usano gli indicizzatori di ricerca di Azure, è possibile trovare occasionalmente manualmente nelle situazioni in cui i dati di input non corrispondano piuttosto schema hello dell'indice di destinazione. In questi casi, è possibile utilizzare **campo mapping** tootransform i dati in hello forma desiderata.

Alcune situazioni in cui i mapping dei campi sono utili:

* L'origine dati include un campo `_id`, ma Ricerca di Azure non consente nomi di campo che iniziano con un carattere di sottolineatura. Un mapping dei campi consente troppo "rename" un campo.
* Si desidera indicizzare diversi campi di hello con hello toopopulate stessi dati di origine dati, ad esempio perché si desidera tooapply analizzatori diversi toothose campi. I mapping dei campi consentono di "biforcare" un campo dell'origine dati.
* È necessario tooBase64 codificare o decodificare i dati. I mapping dei campi supportano diverse **funzioni di mapping**, incluse quelle per la codifica e decodifica Base64.   

## <a name="setting-up-field-mappings"></a>Configurazione del mapping dei campi
È possibile aggiungere i mapping dei campi quando si crea un nuovo indicizzatore utilizzando hello [creare indicizzatore](https://msdn.microsoft.com/library/azure/dn946899.aspx) API. È possibile gestire i mapping dei campi in un indicizzatore di indicizzazione utilizzando hello [aggiornamento indicizzatore](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.

Un mapping dei campi è costituito da tre parti:

1. `sourceFieldName`, che rappresenta un campo nell'origine dati. Questa proprietà è obbligatoria.
2. `targetFieldName`facoltativo, che rappresenta un campo nell'indice di ricerca. Se omesso, hello stesso nome utilizzato hello viene utilizzata l'origine dati.
3. `mappingFunction`facoltativo, che può trasformare i dati usando una delle varie funzioni predefinite. l'elenco completo delle funzioni Hello è [sotto](#mappingFunctions).

Mapping dei campi vengono aggiunti toohello `fieldMappings` matrice nella definizione di indicizzatore hello.

L'esempio seguente mostra come gestire le differenze nei nomi di campo:

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Un indicizzatore può avere più mapping dei campi. L'esempio seguente mostra come "biforcare" un campo:

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Ricerca di Azure Usa il confronto tra maiuscole e minuscole tooresolve hello funzione nomi di campo e nel mapping dei campi. Questa operazione è utile (non è necessario tooget tutte maiuscole e minuscole hello destra), ma significa che l'origine dati o un indice non può avere campi che differiscono solo per i casi.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Funzioni del mapping dei campi
Queste funzioni sono attualmente supportate:

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Esegue *URL safe* codifica Base64 di hello stringa di input. Si presuppone che hello input con codificata UTF-8.

#### <a name="sample-use-case"></a>Caso d'uso di esempio
Solo i caratteri URL-safe possono apparire in una chiave di documento di ricerca di Azure (perché i clienti devono essere in grado di tooaddress documento di hello usando hello API di ricerca, ad esempio). Se i dati contengono caratteri non sicuri URL e si desidera toouse è toopopulate un campo chiave nell'indice di ricerca, utilizzare questa funzione.   

#### <a name="example"></a>Esempio
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Esegue la decodifica Base64 della stringa di input hello. Hello input presuppone tooa *URL safe* stringa con codifica Base64.

#### <a name="sample-use-case"></a>Caso d'uso di esempio
I valori di metadati personalizzati BLOB devono essere codificati in ASCII. È possibile utilizzare Base64 codifica toorepresent arbitrario le stringhe Unicode nel blob di metadati personalizzati. Tuttavia, ricerca toomake significativa, è possibile utilizzare dati funzione tooturn hello codificato in stringhe "normali" durante la compilazione di indice di ricerca.  

#### <a name="example"></a>Esempio
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Un campo stringa usando hello specificato delimitatore e token hello prelievi divisioni hello posizione specificata in suddivisione risultante hello.

Ad esempio, se hello input è `Jane Doe`, hello `delimiter` è `" "`(spazio) e hello `position` è 0, il risultato di hello è `Jane`; se hello `position` è 1, risultato hello è `Doe`. Se posizione hello fa riferimento il token tooa che non esiste, verrà restituito un errore.

#### <a name="sample-use-case"></a>Caso d'uso di esempio
L'origine dati contiene un `PersonName` campo e si desidera tooindex come due `FirstName` e `LastName` campi. È possibile utilizzare questo hello toosplit funzione di input utilizzando il carattere di spazio hello come hello delimitatore.

#### <a name="parameters"></a>parameters
* `delimiter`: toouse una stringa come separatore di hello quando suddivisione hello stringa di input.
* `position`: una posizione in base zero di integer di hello toopick token dopo la stringa di input hello viene suddiviso.    

#### <a name="example"></a>Esempio
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Trasformazioni di una stringa formattata come una matrice JSON di stringhe in una matrice di stringhe che può essere utilizzati toopopulate un `Collection(Edm.String)` campo indice hello.

Ad esempio, se hello stringa di input è `["red", "white", "blue"]`, quindi il campo di destinazione hello di tipo `Collection(Edm.String)` verrà popolato con i valori hello tre `red`, `white` e `blue`. Per i valori di input che non possono essere analizzati come matrici di stringhe JSON, viene restituito un errore.

#### <a name="sample-use-case"></a>Caso d'uso di esempio
Database SQL di Azure non dispone di un tipo di dati incorporato che naturalmente esegue il mapping troppo`Collection(Edm.String)` campi di ricerca di Azure. toopopulate campi della raccolta di stringhe, formattare i dati di origine come matrice di stringhe JSON e utilizzare questa funzione.

#### <a name="example"></a>Esempio
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Come contribuire al miglioramento di Ricerca di Azure
Se si dispone delle richieste di funzionalità o le proprie idee per migliorare, per raggiungere toous nel nostro [sito UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
