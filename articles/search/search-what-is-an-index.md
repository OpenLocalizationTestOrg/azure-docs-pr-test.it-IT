---
title: un indice di ricerca di Azure aaaCreate | Microsoft Azure | Servizio di ricerca di cloud ospitato
description: Informazioni su un indice in Ricerca di Azure e su come viene usato.
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Creare un indice di Ricerca di Azure
> [!div class="op_single_selector"]
> * [Panoramica](search-what-is-an-index.md)
> * [Portale](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>Informazioni sugli indici
Un *indice* è un archivio persistente di *documenti* e altri costrutti usati da un servizio di Ricerca di Azure. Un documento è un singola unità di dati ricercabili nell'indice. Ad esempio, un rivenditore di e-commerce può avere un documento per ogni elemento in vendita, un'agenzia di stampa può avere un documento per ogni articolo e così via. Mapping equivalenti di database familiari toomore questi concetti: un *indice* è concettualmente simile tooa *tabella*, e *documenti* equivalgono troppo*righe* in una tabella.

Quando si aggiungono/caricare documenti e inviare le query di ricerca tooAzure ricerca, inviare l'indice specifico di tooa le richieste nel servizio di ricerca.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Tipi di campo e attributi in un indice di Ricerca di Azure
Durante la definizione dello schema, è necessario specificare il nome di hello, tipo e gli attributi di ogni campo nell'indice. tipo di campo Hello classifica hello i dati archiviati in tale campo. Gli attributi sono impostati su singoli campi toospecify utilizzo campo hello. Hello nelle tabelle seguenti enumerare tipi hello e attributi che è possibile specificare.

### <a name="field-types"></a>Tipi di campo
| Tipo | Descrizione |
| --- | --- |
| *Edm.String* |Testo facoltativamente soggetto a tokenizzazione per la ricerca full-text (suddivisione delle parole, stemming e così via). |
| *Collection(Edm.String)* |Elenco di stringhe facoltativamente soggette a tokenizzazione per la ricerca full-text. Non vi è alcun limite teorico numero hello di elementi in una raccolta, ma limite superiore di hello 16 MB per le dimensioni del payload applica toocollections. |
| *Edm.Boolean* |Contiene valori true/false. |
| *Edm.Int32* |Valori integer a 32 bit. |
| *Edm.Int64* |Valori integer a 64 bit. |
| *Edm.Double* |Dati numerici a precisione doppia. |
| *Edm.DateTimeOffset* |I valori di tempo rappresentati in formato OData V4 hello di data (ad esempio `yyyy-MM-ddTHH:mm:ss.fffZ` o `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Un punto che rappresenta una posizione geografica globo hello. |

È possibile trovare altre informazioni sui [tipi di dati supportati di Ricerca di Azure qui](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types).

### <a name="field-attributes"></a>Attributi dei campi
| Attributo | Descrizione |
| --- | --- |
| *Chiave* |Stringa che fornisce hello ID univoco di ciascun documento, utilizzato per cercare di documento. Ogni indice deve avere una chiave. Un solo campo può essere una chiave di hello e il relativo tipo deve essere impostato tooEdm.String. |
| *Recuperabile* |Specifica se il campo può essere restituito nel risultato di una ricerca. |
| *Filtrabile* |Consente di hello campo toobe utilizzati nelle query di filtro. |
| *Ordinabile* |Consente a una query risultati della ricerca toosort l'utilizzo del campo. |
| *Con facet* |Consente di toobe un campo utilizzato un [navigazione con facet](search-faceted-navigation.md) struttura per il filtro utente Self-diretto. In genere i campi contenenti valori ricorrenti che è possibile utilizzare toogroup insieme più documenti, ad esempio, più documenti che rientrano in una categoria di servizio o un marchio singolo, funzionano meglio come facet. |
| *Ricercabile* |I segni di hello campo come disponibile per la ricerca full-text. |

È possibile trovare altre informazioni sugli [attributi di indice di Ricerca di Azure qui](https://docs.microsoft.com/rest/api/searchservice/Create-Index).

## <a name="guidance-for-defining-an-index-schema"></a>Indicazioni per la definizione di uno schema di indice
Quando si progetta l'indice, richiedere del tempo in hello pianificazione fase toothink tramite ogni decisione. È importante tenere le esigenze di business e di esperienza utente ricerca presenti quando si progetta l'indice di ogni campo deve essere assegnato hello [agli attributi](https://docs.microsoft.com/rest/api/searchservice/Create-Index). La modifica di un indice dopo la distribuzione comporta la ricompilazione e ricaricare i dati di hello.

Se i requisiti per l'archiviazione dei dati cambiano nel tempo, è possibile aumentare o ridurre la capacità aggiungendo o spostando le partizioni. Per informazioni dettagliate, vedere [Gestire il servizio di ricerca in Microsoft Azure](search-manage.md) o [Limiti dei servizi](search-limits-quotas-capacity.md) in Ricerca di Azure.

