---
title: tipi di dati complessi toomodel aaaHow in ricerca di Azure | Documenti Microsoft
description: "È possibile modellare strutture di dati annidate o gerarchiche in un indice di Ricerca di Azure usando un set di righe bidimensionale e il tipo di dati Collection."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Come tipi di dati complessi toomodel in ricerca di Azure
Set di dati esterni utilizzati toopopulate a volte, un indice di ricerca di Azure includono le sottostrutture gerarchiche o annidate che suddivide accuratamente in un set di righe tabulare. Gli esempi di strutture di questo tipo possono includere più ubicazioni e numeri di telefono per un singolo cliente, più colori e dimensioni per un singolo SKU, più autori di un singolo libro e così via. In termini di modellazione, è possibile visualizzare queste strutture di cui tooas *tipi di dati complessi*, *tipi di dati composti*, *tipi di dati compositi*, o *aggregazione tipi di dati*, tooname qualche.

Tipi di dati complessi non sono supportati in modo nativo in ricerca di Azure, ma una soluzione si basa sulla collaudata include fasi di conversione struttura hello e quindi utilizzando un **raccolta** tooreconstitute struttura interna di hello del tipo di dati. Seguendo tecnica hello descritta in questo articolo gli toobe contenuto hello avanzata, con facet, filtrati e ordinati.

## <a name="example-of-a-complex-data-structure"></a>Esempio di struttura di dati complessa
Dati hello in questione si trovano in genere, come un set di documenti JSON o XML o come elementi in un archivio NoSQL, ad esempio Azure Cosmos DB. Richiesta di hello strutturalmente, deriva dalla presenza di più elementi figlio che devono toobe la ricerca e filtrati.  Come punto di partenza per illustrare la soluzione alternativa hello, richiedere hello seguente documento JSON che elenca un set di contatti, ad esempio:

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

Mentre i campi di hello denominato 'id', 'name' e 'società' è possibile associare facilmente uno a uno come campi all'interno di un indice di ricerca di Azure, campo 'locations' hello contiene una matrice di percorsi, avere sia un set di ID di posizione, nonché le descrizioni di percorso. Dato che ricerca di Azure non dispone di un tipo di dati che supporta questa caratteristica, è necessaria toomodel un modo diverso in ricerca di Azure. 

> [!NOTE]
> Questa tecnica è descritto da Kirk Evans in un post di blog [l'indicizzazione di DocumentDB con ricerca di Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), che illustra una tecnica denominata "conversione dati hello", in base al quale è un campo denominato `locationsID` e `locationsDescription` che sono entrambi [raccolte](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matrice di stringhe).   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>Parte 1: Convertire la matrice hello in singoli campi
toocreate un indice di ricerca di Azure che consente di adattare questo set di dati, creare singoli campi per sottostruttura nidificata hello: `locationsID` e `locationsDescription` con un tipo di dati [raccolte](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matrice di stringhe). In questi campi è necessario indicizzare i valori hello '1' e '2' hello `locationsID` campo per i valori di John Smith e hello '3' & '4' in hello `locationsID` field per Jen Campbell.  

I dati in Ricerca di Azure si presenteranno come segue: 

![Dati di esempio, 2 righe](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>Parte 2: Aggiungere un campo di raccolta nella definizione dell'indice hello
Nello schema di indice hello, definizioni di campo hello potrebbero apparire esempio toothis simile.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>Convalidare i comportamenti di ricerca e facoltativamente estendere hello indice
Presupponendo che si indice creato hello e dati hello caricato, è ora possibile testare hello soluzione tooverify ricerca esecuzione delle query in set di dati hello. Ogni campo di tipo **raccolta** dovrà essere **ricercabile**, **filtrabile** e **con facet**. Dovrebbe essere in grado di toorun query come:

* Trovare tutte le persone che lavorano presso hello "Sede centrale Adventureworks".
* Ottenere un conteggio del numero di hello di persone che lavorano in un ufficio di Home' '.  
* Delle persone hello che lavorano in un "Home Office", indicano quali altri uffici funzionano insieme a un numero di persone hello in ogni posizione.  

In questa tecnica rientra distanza è quando è necessario toodo una ricerca che combina id percorso hello nonché a descrizione dell'ubicazione hello. ad esempio:

* Trovare tutte le persone con "Home Office" E con ID ubicazione 4.  

Se si ricorda il contenuto originale di hello simile al seguente:

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

Tuttavia, dopo che è stato suddiviso dati hello in campi separati, non esiste alcun modo di sapere se hello Home Office per Jen Campbell si riferisce troppo`locationsID 3` o `locationsID 4`.  

toohandle questo caso, definire un altro campo nell'indice hello che tutti i dati di hello combina in un'unica raccolta.  Per questo esempio, questo campo verrà chiamata `locationsCombined` e si separano contenuto hello con un `||` anche se è possibile scegliere qualsiasi separatore che si ritiene sarebbe un set univoco di caratteri per il contenuto. ad esempio: 

![Dati di esempio, 2 righe con separatore](./media/search-howto-complex-data-types/sample-data-2.png)

Usando il campo `locationsCombined` , è ora possibile supportare query aggiuntive, ad esempio:

* Visualizzare un conteggio delle persone che lavorano in "Home Office" con ID ubicazione "4".  
* Cercare le persone che lavorano in "Home Office" con ID ubicazione "4". 

## <a name="limitations"></a>Limitazioni
Questa tecnica è utile per diversi scenari, ma non è applicabile in tutti i casi.  ad esempio:

1. Se si dispone di un set statico di campi nel tipo di dati complessi e si è verificato alcun toomap modo tutte le possibili hello tipi tooa singolo campo. 
2. L'aggiornamento degli oggetti annidato hello richiede toodetermine alcune operazioni aggiuntive esattamente cosa toobe aggiornato nell'indice di ricerca di Azure hello

## <a name="sample-code"></a>Codice di esempio
È possibile vedere un esempio sulla configurazione tooindex un complessi dati JSON in ricerca di Azure ed eseguire un numero di query su questo set di dati in questo [repository GitHub](https://github.com/liamca/AzureSearchComplexTypes).

## <a name="next-step"></a>Passaggio successivo
[Voto per il supporto nativo per i tipi di dati complessi](https://feedback.azure.com/forums/263029-azure-search) pagina hello UserVoice di ricerca di Azure e fornire qualsiasi input aggiuntivo che si desidera tooconsider riguardanti l'implementazione delle funzionalità. È inoltre possibile entrare toome direttamente su Twitter in @liamca.

