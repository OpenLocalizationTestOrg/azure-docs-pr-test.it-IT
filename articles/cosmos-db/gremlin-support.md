---
title: supporto per Cosmos DB Gremlin aaaAzure | Documenti Microsoft
description: "Informazioni su hello lingua Gremlin TinkerPop Apache, funzionalità e i passaggi e disponibile in Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Supporto Gremlin Graph di Azure Cosmos DB
Azure Cosmos DB supporta il linguaggio di attraversamento di grafi [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps) di [Apache Tinkerpop](http://tinkerpop.apache.org), ovvero un'API Graph per la creazione di entità di grafi e l'esecuzione di operazioni di query sui grafi. È possibile utilizzare hello Gremlin toocreate grafico entità language (vertici e bordi), modificare le proprietà all'interno di tali entità, eseguire query e attraversamenti ed eliminare entità. 

Azure DB Cosmos porta per le aziende toograph database. Questo include distribuzione globale, scalabilità indipendente di archiviazione e velocità effettiva, latenze stimabili in pochissimi millisecondi, indicizzazione automatica e contratti di servizio pari al 99,99%. Poiché Azure Cosmos DB supporta TinkerPop/Gremlin, è possibile eseguire facilmente la migrazione di applicazioni scritte in un altro database grafico senza modifiche al codice toomake. In più, grazie al supporto Gremlin, Azure Cosmos DB si integra facilmente con framework di analisi abilitati per TinkerPop come [Apache Spark GraphX](http://spark.apache.org/graphx/). 

In questo articolo è fornire un'esercitazione rapida di Gremlin ed enumerare funzionalità Gremlin hello e i passaggi che sono supportati in anteprima hello del supporto di API Graph.

## <a name="gremlin-by-example"></a>Esempio di Gremlin
Consente di usare un toounderstand grafico di esempio come query possono essere espresse in Gremlin. Hello nella figura seguente mostra un'applicazione aziendale che gestisce i dati sugli utenti, interessi e i dispositivi sotto forma di hello di un grafico.  

![Database di esempio che mostra persone, dispositivi e interessi](./media/gremlin-support/sample-graph.png) 

Questo grafico è hello seguenti tipi di vertice (denominati "label" nelle Gremlin):

- Gli utenti: il grafico di hello con tre persone, Round Robin, Thomas e Ben
- : Interessi relativi interessi, in questo esempio, hello del gioco del calcio
- Dispositivi: i dispositivi hello utilizzato dagli utenti
- Sistemi operativi: i sistemi operativi hello eseguibili su dispositivi hello

Abbiamo rappresentano le relazioni di hello tra queste entità tramite i seguenti tipi/etichette sui bordi hello:

- Conosce: ad esempio, "Thomas conosce Robin"
- Interessati: interessi di hello toorepresent di persone hello in questo grafico, ad esempio, "Ben è interessato Football"
- RunsOS: Portatile esegue hello del sistema operativo Windows
- Usi: toorepresent utilizza la periferica che un utente. Ad esempio, Robin usa un telefono Motorola con numero di serie 77

Eseguire alcune operazioni su questo grafico utilizzando hello [Gremlin Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console). È anche possibile eseguire queste operazioni utilizzando il driver Gremlin nella piattaforma hello di propria scelta (Java, Node.js, Python o .NET).  Prima di esaminare cosa è supportata nel database Cosmos di Azure, esaminiamo alcuni esempi tooget, familiarità con la sintassi di hello.

Verrà dapprima esaminato CRUD. Hello istruzione Gremlin seguente inserisce hello vertice "Thomas" grafico hello:

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

Successivamente, hello Gremlin istruzione inserisce un bordo "sa" tra Thomas e Round Robin.

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

Hello nella query seguente restituisce vertici "person" hello in ordine decrescente i relativi nomi:
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

Dove lucentezza grafici è quando è necessario tooanswer domande quali "quali sistemi operativi usano gli elementi Friend di Thomas?". È possibile eseguire questa semplice tooget attraversamento Gremlin tali informazioni dal grafico hello:

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
Ora verrà esaminato cosa Azure Cosmos DB offre agli sviluppatori di Gremlin.

## <a name="gremlin-features"></a>Funzionalità di Gremlin
TinkerPop è uno standard che copre un'ampia gamma di tecnologie a grafi. Pertanto, ha toodescribe terminologia standard quali funzionalità sono fornite da un provider di grafico. Azure Cosmos DB offre un database a grafi scrivibile, ad alta concorrenza, persistente, che può essere partizionato tra più server o cluster. 

Hello nella tabella seguente sono elencate le funzionalità TinkerPop hello vengono implementate da Azure Cosmos DB: 

| Categoria | Implementazione di Azure Cosmos DB |  Note | 
| --- | --- | --- |
| Funzionalità del grafo | Offre persistenza e accesso simultaneo in anteprima. Toosupport progettato transazioni | Metodi di computer possono essere implementati tramite il connettore Spark hello. |
| Funzionalità della variabile | Supporta Boolean, Integer, Byte, Double, Float, Integer, Long, String | Supporta i tipi primitivi, è compatibile con i tipi complessi tramite modello di dati |
| Funzionalità del vertice | Supporta RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty  | Supporta la creazione, la modifica e l'eliminazione di vertici |
| Funzionalità della proprietà del vertice | StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Supporta la creazione, la modifica e l'eliminazione di proprietà di vertici |
| Funzionalità dell'arco | AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty | Supporta la creazione, la modifica e l'eliminazione di archi |
| Funzionalità della proprietà dell'arco | Properties, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Supporta la creazione, la modifica e l'eliminazione di proprietà dell'arco |

## <a name="gremlin-wire-format-graphson"></a>Formato wire Gremlin: GraphSON

Azure DB Cosmos utilizza hello [GraphSON formato](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) la restituzione di risultati da operazioni Gremlin. GraphSON è formato standard di hello Gremlin per la rappresentazione di vertici, bordi e proprietà (singolo e multivalore) usando JSON. 

Ad esempio, hello frammento di codice seguente mostra una rappresentazione GraphSON di un vertice *restituito client toohello* da Azure Cosmos DB. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

le proprietà di Hello utilizzati dalle GraphSON per vertici sono seguente hello:

| Proprietà | Descrizione |
| --- | --- |
| id | ID di Hello per vertice hello. Deve essere univoco (in combinazione con il valore di hello di _partition se applicabile) |
| label | etichetta Hello del vertice hello. Si tratta di tipo di entità hello toodescribe facoltativo e l'utilizzo. |
| type | Vertici toodistinguish utilizzato dai documenti non grafico |
| properties | Elenco di proprietà definite dall'utente associato al vertice hello. Ogni proprietà può avere più valori. |
| _partition (configurabile) | chiave di partizione Hello del vertice hello. Può essere utilizzato tooscale out grafici toomultiple server |
| outE | Contiene un elenco degli archi uscenti da un vertice. L'archiviazione delle informazioni di adiacenza hello con vertice consente l'esecuzione rapida delle attraversamenti. Gli archi vengono raggruppati in base alle relative etichette. |

E bordo hello contiene hello seguente toohelp informazioni con le parti tooother di navigazione del grafico hello.

| Proprietà | Descrizione |
| --- | --- |
| id | ID di Hello per edge hello. Deve essere univoco (in combinazione con il valore di hello di _partition se applicabile) |
| label | etichetta Hello del bordo hello. Questa proprietà è di tipo di relazione hello toodescribe facoltativo e l'utilizzo. |
| inV | Contiene un elenco di vertici per un bordo. L'archiviazione delle informazioni adiacenza hello con bordo hello consente l'esecuzione rapida delle attraversamenti. I vertici vengono raggruppati in base alle relative etichette. |
| properties | Contenitore di proprietà definite dall'utente associato hello bordo. Ogni proprietà può avere più valori. |

Ogni proprietà può archiviare più valori all'interno di una matrice. 

| Proprietà | Descrizione |
| --- | --- |
| value | valore proprietà hello Hello

## <a name="gremlin-partitioning"></a>Partizionamento di Gremlin

In Azure Cosmos DB i grafi vengono archiviati all'interno di contenitori che possono essere scalati in modo indipendente in termini di memoria e velocità effettiva (espressa in richieste normalizzate al secondo). Ogni contenitore deve definire una proprietà della chiave di partizione facoltativa, ma consigliata, che determina un limite della partizione logica per i dati correlati. Ogni vertice/arco deve possedere una proprietà `id` univoca per le entità all'interno del valore della chiave di partizione. sono disponibili dettagli Hello in [partizionamento nel database di Azure Cosmos](partition-data.md).

Le operazioni Gremlin funzionano senza problemi su dati a grafo che si estendono su più partizioni in Azure Cosmos DB. Tuttavia, è consigliabile toochoose una chiave di partizione per i grafici che è in genere utilizzato come un filtro della query, ha molti valori distinti e frequenza simile di accedere a questi valori. 

## <a name="gremlin-steps"></a>Step di Gremlin
Ora esaminiamo hello passaggi Gremlin supportati da Azure Cosmos DB. Per informazioni complete su Gremlin, vedere [TinkerPop reference](http://tinkerpop.apache.org/docs/current/reference) (Riferimento a TinkerPop).

| step | Descrizione | Documentazione TinkerPop 3.2 | Note |
| --- | --- | --- | --- |
| `addE` | Aggiunge un arco tra due vertici | [addE step](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | Aggiunge un grafico toohello vertex | [addV step](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest che tutti gli attraversamenti hello restituiscono un valore | [and step](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | Tooassign di modulatore un output toohello variabile di un passaggio di un passaggio | [as step](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | Modulatore di step usato con `group` e `order` | [by step](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | Restituisce l'attraversamento prima hello che restituisce un risultato | [coalesce step](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | Restituisce un valore costante. Usato con `coalesce`| [constant step](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Restituisce il conteggio di hello dall'attraversamento hello | [count step](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | Restituisce i valori di hello con i duplicati di hello rimossi | [dedup step](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | Elimina hello valori (vertex/bordo) | [drop step](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | Si comporta come un ostacolo che calcola l'aggregazione di hello dei risultati| [fold step](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | Gruppi di hello valori in base alle etichette hello specificate| [group step](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Proprietà toofilter usato, vertici e bordi. Supporta `hasLabel`, `hasId`, `hasNot` e le varianti `has`. | [has step](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | Inserisce i valori in un flusso| [inject step](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Utilizzato tooperform un filtro utilizzando un'espressione booleana | [is step](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | Utilizzato toolimit numero di elementi nell'attraversamento hello| [limit step](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | Locale esegue il wrapping di una sezione di una sottoquery tooa trasversale, in modo analogo | [local step](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | Negazione di hello tooproduce di un filtro utilizzato | [not step](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | Restituisce hello risultato hello specificato attraversamento se produce un risultato else restituisce hello elemento chiamante | [optional step](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Garantisce almeno uno dei attraversamenti hello restituisce un valore | [or step](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | Restituisce i risultati in hello specificato ordinamento | [order step](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Restituisce il percorso completo di attraversamento hello di hello | [path step](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | Proprietà hello progetti come una mappa | [project step](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Restituisce le proprietà di hello per hello etichette specificate | [properties step](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | I filtri toohello specificato intervallo di valori| [range step](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Passaggio di hello viene ripetuto per hello specificato numero di volte. Usato per eseguire i cicli | [repeat step](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Risultati toosample dall'attraversamento hello utilizzati | [sample step](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Risultati tooproject dall'attraversamento hello utilizzati |  [select step](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Utilizzato per le aggregazioni non bloccante dall'attraversamento hello | [store step](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | Aggrega i percorsi da un vertice a una struttura ad albero | [tree step](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | Srotola un iteratore come step| [unfold step](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | Unisce i risultati di più attraversamenti| [union step](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Include i passaggi di hello necessari per gli attraversamenti tra vertici e bordi `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, e `otherV` per | [vertex steps](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Utilizzare toofilter risultati dall'attraversamento hello. Supporta `eq`, `neq`, `lt`, `lte`, `gt`, `gte` e gli operatori `between`  | [where step](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

Il motore ottimizzato per la scrittura di Azure Cosmos DB supporta l'indicizzazione automatica di tutte le proprietà all'interno di vertici e archi per impostazione predefinita. Pertanto, una query con filtri di intervallo query, ordinamento, o le aggregazioni specificate a qualsiasi proprietà vengono elaborate dall'indice hello e gestite in modo efficiente. Per altre informazioni sul funzionamento dell'indicizzazione in Azure Cosmos DB, vedere il documento sull'[indicizzazione senza schema](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).

## <a name="next-steps"></a>Passaggi successivi
* Iniziare a creare un'applicazione Graph [tramite SDK](create-graph-dotnet.md) 
* Altre informazioni sul [supporto Graph di Azure Cosmos DB](graph-introduction.md)
