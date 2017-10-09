---
title: query aaaSQL per l'API DocumentDB DB Cosmos Azure | Documenti Microsoft
description: "Informazioni sulla sintassi SQL, sui concetti relativi ai database e sulle query SQL per Cosmos DB. SQL può essere usato come linguaggio di query JSON in Cosmos DB."
keywords: sintassi sql, query sql, linguaggio di query json, concetti relativi ai database e query sql, funzioni di aggregazione
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>Query SQL per l'API di DocumentDB di Azure Cosmos DB
Microsoft Azure Cosmos DB supporta l'esecuzione di query di documenti mediante SQL (Structured Query Language) come linguaggio di query JSON. Cosmos DB è effettivamente privo di schema. In virtù del relativo commit toohello JSON modello di dati direttamente nel motore di database hello, fornisce l'indicizzazione automatica di documenti JSON senza richiedere uno schema esplicito o la creazione di indici secondari. 

Durante la progettazione di linguaggio di query hello per Cosmos DB, abbiamo due obiettivi:

* Invece di realizzazione di un nuovo linguaggio di query JSON, Desideravamo toosupport SQL. SQL è uno dei linguaggi di query più più comuni di hello. Il linguaggio di query SQL di Cosmos DB fornisce un modello di programmazione formale per le query complesse sui documenti JSON.
* Come un database di documenti JSON in grado di eseguire JavaScript direttamente nel motore di database hello, Desideravamo modello di programmazione toouse JavaScript di base hello per il linguaggio di query. Hello DocumentDB API SQL è una radice nel sistema di tipi di JavaScript, la valutazione dell'espressione e chiamata di funzione. Questo rappresenta a sua volta un modello di programmazione naturale per le proiezioni relazionali, la navigazione gerarchica attraverso i documenti JSON, i self join, query spaziali e la chiamata di funzioni definite dall'utente (UDF) scritte interamente in JavaScript, tra le altre funzionalità. 

Riteniamo che queste funzionalità sono tooreducing chiave le forze di attrito hello tra un'applicazione hello e database hello e sono fondamentali per la produttività degli sviluppatori.

Si consiglia di introduzione osservando i seguenti video, in cui Aravind Ramachandran illustra le funzionalità di query del DB Cosmos, hello e visitare il nostro [Query Playground](http://www.documentdb.com/sql/demo), in cui è possibile provare Cosmos DB ed eseguire query SQL il set di dati.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

Tornare quindi toothis articolo, in cui si inizia con un'esercitazione di query SQL che illustra alcune semplici documenti JSON e i comandi SQL.

## <a id="GettingStarted"></a>Guida introduttiva ai comandi SQL in Cosmos DB
toosee Cosmos DB SQL a livello di lavoro, si inizia con alcuni documenti JSON semplici e seguire i passaggi alcune semplici query su di esso. Considerare questi due documenti JSON come se riguardassero due famiglie. Con Cosmos DB, non è necessario toocreate eventuali schemi o gli indici secondari in modo esplicito. È sufficiente tooinsert hello JSON documenti tooa DB Cosmos raccolta e quindi eseguire una query. Qui abbiamo un JSON semplice documento per hello famiglia Andersen, hello padri, figli (e gli animali domestici), l'indirizzo e informazioni di registrazione. documento di Hello contiene stringhe, numeri, valori booleani, matrici e proprietà annidate. 

**Documento**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

Ecco un secondo documento con una sottile differenza: vengono usati `givenName` e `familyName` invece di `firstName` e `lastName`.

**Documento**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Ora provare alcune query su questa toounderstand dati alcune hello agli aspetti principali di SQL API DocumentDB. Ad esempio, eseguire una query restituisce i documenti hello in campo id hello corrisponde seguente hello `AndersenFamily`. Poiché si tratta di un `SELECT *`, output di hello di query hello è documento JSON completo hello:

**Query**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Risultati**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


Ora si consideri il caso di hello in cui è necessario tooreformat hello output JSON in una forma diversa. Questa query progetti JSON un nuovo oggetto con due campi selezionati, nome e la città, quando hello degli città ha hello stesso nome come stato hello. In questo caso, "NY, NY" corrispondono.

**Query**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**Risultati**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


la query successiva Hello restituisce tutti i nomi di hello specificato di elementi figlio nella famiglia di hello il cui id corrisponde `WakefieldFamily` ordinati in base alla città hello di residenza.

**Query**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**Risultati**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


Desideriamo toodraw attenzione tooa alcuni aspetti importanti di hello Cosmos DB linguaggio esempi hello che abbiamo visto finora di query:  

* Poiché l'API SQL di DocumentDB elabora i valori JSON, deve gestire entità con struttura ad albero invece di righe e colonne. Di conseguenza, il linguaggio di hello consente di fare riferimento toonodes della struttura ad albero hello a qualsiasi profondità arbitraria, ad esempio `Node1.Node2.Node3…..Nodem`, simile toorelational SQL che fa riferimento toohello due riferimento alla parte di `<table>.<column>`.   
* Hello structured query language funziona con i dati senza schema. Pertanto, hello toobe associazione di tipo sistema esigenze in modo dinamico. Hello stessa espressione potrebbe restituire tipi diversi in diversi documenti. risultato Hello di una query è un valore JSON valido, ma non è garantito toobe di uno schema fisso.  
* Cosmos DB supporta solo i documenti JSON completi. Ciò significa espressioni e il sistema di tipi di hello toodeal limitate solo con tipi JSON. Fare riferimento toohello [specifica JSON](http://www.json.org/) per altri dettagli.  
* Una raccolta di Cosmos DB è un contenitore senza schema dei documenti JSON. le relazioni di Hello in entità di dati all'interno di documenti in una raccolta in modo implicito vengono acquisite dal contenuto e non da chiave primaria e relazioni di chiave esterne. Questo è un aspetto importante importante precisare alla luce di join tra più documenti hello descritto più avanti in questo articolo.

## <a id="Indexing"></a> Indicizzatore di Cosmos DB
Prima di passare a hello sintassi SQL API DocumentDB, vale la pena esplorazione hello l'indicizzazione di progettazione in DB Cosmos. 

scopo di Hello degli indici dei database è tooserve query nei vari moduli e forme con un consumo di risorse minime (ad esempio CPU e di input/output) fornendo una velocità effettiva ottimale e a bassa latenza. Spesso, scelta hello dell'indice di destra hello per le query di un database richiede una quantità pianificazione e sperimentazione. Questo approccio pone un problema per i database senza schema in cui i dati hello tooa strict schema non è conforme e si evolve rapidamente. 

Pertanto, quando è stato progettato sottosistema di indicizzazione Cosmos DB hello, impostiamo hello seguenti obiettivi:

* Indicizzare i documenti senza schema: hello indicizzazione sottosistema non richiede alcuna informazione sullo schema o supposizioni sullo schema di documenti hello. 
* Supporto per le query relazionale e gerarchiche efficiente e complesse: indice hello supporta il linguaggio di query Cosmos DB hello in modo efficiente, incluso il supporto per le proiezioni relazionale e gerarchiche.
* Supporto per le query coerente riscontri un volume velocità delle operazioni di scrittura: per la scrittura ad alta velocità effettiva dei carichi di lavoro con query coerente, hello indice viene aggiornato in modo incrementale, in modo efficiente e online in faccia hello di un volume velocità delle operazioni di scrittura. aggiornamento di un indice coerente Hello è query hello tooserve fondamentale a livello di coerenza hello in quale servizio di documenti hello hello configurato dall'utente.
* Supporto per multi-tenancy: dato modello basato su prenotazione hello di governance delle risorse tra i tenant, gli aggiornamenti dell'indice vengono eseguiti all'interno del budget hello delle risorse di sistema (CPU, memoria e operazioni di input/output al secondo) allocata per ogni replica. 
* L'efficienza di archiviazione: per convenienza economica rispetto a, hello archiviazione su disco overhead dell'indice hello è limitata e prevedibile. Ciò è fondamentale poiché DB Cosmos consente hello developer toomake basato sui costi dei compromessi tra overhead delle prestazioni delle query di relazione toohello dell'indice.  

Fare riferimento toohello [esempi Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) in MSDN per gli esempi che mostra come tooconfigure hello criteri di indicizzazione per una raccolta. Consente ora ottenere i dettagli di hello di hello sintassi SQL di Azure Cosmos DB.

## <a id="Basics"></a>Elementi di base di una query SQL di Cosmos DB
Ogni query consiste in una clausola SELECT e clausole FROM e WHERE facoltative in base agli standard ANSI-SQL. In genere, per ogni query, hello source nella clausola FROM hello enumerato. Quindi hello applicare un filtro nella clausola WHERE viene applicata in hello origine tooretrieve hello un sottoinsieme di documenti JSON. Infine, in cui viene utilizzata la clausola SELECT hello hello tooproject richiesti i valori JSON nel hello selezionare nell'elenco.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>Clausola FROM
Hello `FROM <from_specification>` clausola è facoltativa a meno che l'origine hello è filtrato o previsto in un secondo momento nella query di hello. scopo di Hello di questa clausola è origine di dati di hello toospecify al quale hello deve utilizzare query. In genere insieme hello è origine hello, ma uno può specificare un subset della raccolta hello invece. 

Ad esempio una query `SELECT * FROM Families` indica che l'intera raccolta di gruppi hello è origine hello su quali tooenumerate. Un identificatore speciale radice può essere utilizzato toorepresent hello insieme anziché il nome di raccolta hello. Hello elenco seguente contiene le regole di hello che vengono applicate per ogni query:

* raccolta di Hello può essere utilizzato un alias, ad esempio `SELECT f.id FROM Families AS f` o semplicemente `SELECT f.id FROM Families f`. Qui `f` equivalente hello `Families`. `AS`è un identificatore di hello tooalias la parola chiave facoltativa.
* Una volta associato un alias, non è possibile associare l'origine originale hello. Ad esempio, `SELECT Families.id FROM Families f` la sintassi è valida perché non è possibile risolvere più identificatore hello "Gruppi".
* Tutte le proprietà che devono toobe a cui fa riferimento devono essere completi. In assenza di hello di conformità rigorosa dello schema, questo viene imposto tooavoid tutte le associazioni ambigue. Pertanto, `SELECT id FROM Families f` la sintassi è valida perché la proprietà hello `id` non è associato.

### <a name="subdocuments"></a>Documenti secondari
origine Hello può rivelarsi sottoinsieme più piccolo tooa ridotta. Ad esempio, solo un sottoalbero in ogni documento tooenumerating, subroot hello quindi causare origine hello, come illustrato nell'esempio seguente hello:

**Query**

    SELECT * 
    FROM Families.children

**Risultati**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

Mentre hello sopra riportato di seguito viene utilizzata una matrice come origine di hello, un oggetto potrebbe inoltre essere utilizzato come origine di hello, ovvero quello mostrato nell'esempio seguente hello: qualsiasi valore JSON valido (non definito) che può essere trovati nell'origine hello viene considerato per l'inclusione nel risultato hello query Hello. Se non dispone di alcune famiglie un `address.state` valore, sono escluse hello risultato della query.

**Query**

    SELECT * 
    FROM Families.address.state

**Risultati**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>Clausola WHERE
clausola WHERE Hello (**`WHERE <filter_condition>`**) è facoltativo. Specifica hello verificate che documenti JSON hello forniti dall'origine hello devono soddisfare in ordine toobe incluso come parte del risultato hello. Deve restituire un documento JSON hello specificato condizioni troppo "true" toobe presi in considerazione per il risultato di hello. Hello dove clausola viene utilizzata dal livello di indice hello in ordine toodetermine hello assoluto subset più piccolo di documenti di origine che possono far parte del risultato hello. 

la query seguente Hello richiede documenti che contengono una proprietà name il cui valore è `AndersenFamily`. Qualsiasi altro tipo di documento che non dispone di una proprietà name, o in cui non corrisponde al valore di hello `AndersenFamily` è escluso. 

**Query**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Risultati**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


Hello precedente riportato di seguito viene riportata una query semplice uguaglianza. L'API SQL di DocumentDB supporta anche una varietà di espressioni scalari. Hello più comunemente usato sono espressioni di binari e unari. Anche i riferimenti di proprietà da un oggetto JSON di origine hello sono espressioni valide. 

Hello dopo gli operatori binari è attualmente supportato e possa essere utilizzata nelle query come illustrato nell'hello seguono esempi:  

<table>
<tr>
<td>Aritmetico</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>Bit per bit</td>    
<td>|, &, ^, <<, >>, >>> (spostamento a destra riempimento zero)</td>
</tr>
<tr>
<td>Logico</td>
<td>AND, OR, NOT</td>
</tr>
<tr>
<td>Confronto</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>String</td>    
<td>|| (concatenazione)</td>
</tr>
</table>  


Saranno ora prese in esame alcune query che usano gli operatori binari.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


Hello operatori unari +,-, ~ non sono supportate anche e può essere utilizzata all'interno di query come illustrato nell'esempio seguente hello:

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



Toobinary e gli operatori unari, sono inoltre consentiti anche i riferimenti di proprietà. Ad esempio, `SELECT * FROM Families f WHERE f.isRegistered` restituisce hello documento JSON che contiene proprietà hello `isRegistered` in cui il valore della proprietà hello è uguale toohello JSON `true` valore. Tutti gli altri valori (false, null, non è definito, `<number>`, `<string>`, `<object>`, `<array>`e così via) comporta i documento di origine toohello viene escluso dal risultato hello. 

### <a name="equality-and-comparison-operators"></a>Operatori di confronto e uguaglianza
Hello nella tabella seguente mostra hello risultato dei confronti di uguaglianza in DocumentDB API SQL tra qualsiasi due tipi JSON.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>Op</strong>
         </td>
         <td valign="top">
            <strong>Undefined</strong>
         </td>
         <td valign="top">
            <strong>Null</strong>
         </td>
         <td valign="top">
            <strong>Boolean</strong>
         </td>
         <td valign="top">
            <strong>Number</strong>
         </td>
         <td valign="top">
            <strong>String</strong>
         </td>
         <td valign="top">
            <strong>Object</strong>
         </td>
         <td valign="top">
            <strong>Array</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Undefined<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Null<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Boolean<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Number<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>String<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Object<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Array<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
      </tr>
   </tbody>
</table>

Per altri operatori di confronto, ad esempio >, > =,! =, < e < =, hello si applicano le regole seguenti:   

* Confronto tra risultati dei tipi in Undefined.
* Confronto tra i risultati di due oggetti o due matrici in Undefined.   

Se il risultato di hello dell'espressione scalare di hello nel filtro hello è definito, documento corrispondente hello non viene incluso nel risultato hello, poiché non definito in modo logico non equivalgono troppo "true".

### <a name="between-keyword"></a>Parola chiave BETWEEN
È inoltre possibile utilizzare hello BETWEEN parola chiave tooexpress le query su intervalli di valori come in SQL ANSI. La parola BETWEEN può essere utilizzata con stringhe o numeri.

Ad esempio, questa query restituisce tutti i documenti della famiglia in cui hello livello prima del bambino è compreso tra 1 e 5 (inclusi). 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

A differenza di ANSI-SQL, è possibile utilizzare anche clausola BETWEEN hello nella clausola FROM di hello come nell'esempio seguente hello.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

Per i tempi di esecuzione query, tenere presente che un criterio di indicizzazione che utilizza un tipo di indice di intervallo su qualsiasi proprietà o i percorsi numerici che vengono filtrati nella clausola BETWEEN hello toocreate. 

Hello la differenza principale tra l'utilizzo di BETWEEN API DocumentDB e di SQL ANSI è che è possibile esprimere le query di intervallo rispetto alle proprietà di tipi misti: ad esempio, potrebbe essere "livello" essere un numero (5) alcuni documenti e le stringhe in altri ambienti ("grade4"). In questi casi, ad esempio in JavaScript, un confronto tra due tipi diversi risultati "undefined" e il documento hello verrà ignorato.

### <a name="logical-and-or-and-not-operators"></a>Operatori logici (AND, OR e NOT)
Gli operatori logici funzionano con valori booleani. tabelle verità logiche Hello per questi operatori vengono visualizzate in hello le tabelle seguenti.

| OPPURE | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |True |True |
| False |True |False |Undefined |
| Undefined |True |Undefined |Undefined |

| AND | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |False |Undefined |
| False |False |False |False |
| Undefined |Undefined |False |Undefined |

| NOT |  |
| --- | --- |
| True |False |
| False |True |
| Undefined |Undefined |

### <a name="in-keyword"></a>Parola chiave IN
la parola chiave IN Hello può essere utilizzato toocheck se un valore specificato corrisponde a qualsiasi valore in un elenco. Ad esempio, questa query restituisce tutti i documenti della famiglia dove id hello è uno di "WakefieldFamily" o "AndersenFamily". 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

In questo esempio restituisce tutti i documenti in cui è stato hello qualsiasi hello specificato i valori.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>Operatori Ternary (?) e Coalesce (??)
gli operatori ternario e Coalesce Hello possono essere utilizzato toobuild espressioni condizionali, simile toopopular linguaggi di programmazione quali c# e JavaScript. 

operatore ternario (?) Hello può essere molto utile quando si creano nuove proprietà JSON in hello veloce. Ad esempio, ora è possibile scrivere i livelli di classe query tooclassify hello in un formato leggibile umano simile per principianti/intermedio/avanzate, come illustrato di seguito.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

È inoltre possibile annidare hello chiamate toohello operatore like in query hello seguente.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

Come con altri operatori di query, se hello proprietà a cui fa riferimento nell'espressione condizionale hello non sono presenti in qualsiasi documento o se i tipi di hello confrontati sono diversi, quindi tali documenti sono esclusi nei risultati della query hello.

Hello operatore Coalesce (?) può essere utilizzato il controllo tooefficiently presenza hello di una proprietà (anche noto come (definita) in un documento. Questo risulta utile per le query su dati semistrutturati o di tipo misto Ad esempio, questa query restituisce hello "Cognome" se è presente o hello "Cognome" Se non è presente.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>Funzione di accesso della proprietà di delimitazione
È inoltre possibile accedere utilizzando l'operatore tra virgolette proprietà hello proprietà `[]`. Ad esempio, la sintassi di `SELECT c.grade` and `SELECT c["grade"]` sono equivalenti. Questa sintassi è utile quando è necessario tooescape una proprietà che contiene spazi, caratteri speciali, o si verifica hello tooshare stesso nome come una parola chiave SQL o una parola riservata.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>Clausola SELECT
clausola SELECT Hello (**`SELECT <select_list>`**) è obbligatorio e specifica quali valori vengono recuperati dalla query hello, esattamente come in SQL ANSI. subset di Hello che è stato filtrato su documenti di origine hello vengono passate in fase di proiezione hello, in cui hello specificato vengono recuperati i valori JSON e viene costruito un nuovo oggetto JSON, per ogni input passato su di esso. 

Hello di esempio seguente mostra una tipico query SELECT. 

**Query**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Risultati**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>Proprietà annidate
Nell'esempio seguente di hello, ci stiamo proiezione due proprietà annidate `f.address.state` e `f.address.city`.

**Query**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Risultati**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


Proiezione supporta anche le espressioni di JSON, come illustrato nell'esempio seguente hello:

**Query**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Risultati**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


Diamo un'occhiata ruolo hello di `$1` qui. Hello `SELECT` clausola deve toocreate un oggetto JSON e poiché non viene fornita alcuna chiave, si utilizzano i nomi delle variabili di argomento implicito a partire da `$1`. Ad esempio, questa query restituisce due variabili di argomento implicite, etichettate `$1` and `$2`.

**Query**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Risultati**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>Aliasing
Ora è possibile estendere l'esempio hello precedente con l'aliasing esplicita dei valori. ESEMPIO hello parola chiave utilizzata per l'alias. È facoltativo, come illustrato durante la proiezione secondo valore hello come `NameInfo`. 

Nel caso in cui una query contiene due proprietà con hello stesso nome, l'alias devono essere toorename utilizzati uno o entrambi hello proprietà in modo che vengono disambiguati hello proiettato risultato.

**Query**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Risultati**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>Espressioni scalari
Inoltre tooproperty fa riferimento a, la clausola SELECT hello supporta anche le espressioni scalari, costanti, espressioni aritmetiche, espressioni logiche, ecc. Ad esempio, ecco una semplice query "Hello World".

**Query**

    SELECT "Hello World"

**Risultati**

    [{
      "$1": "Hello World"
    }]


Di seguito è presentato un esempio più complesso che usa un'espressione scalare.

**Query**

    SELECT ((2 + 11 % 7)-2)/3    

**Risultati**

    [{
      "$1": 1.33333
    }]


Nell'esempio seguente di hello, il risultato di hello di espressione scalare hello è un valore booleano.

**Query**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**Risultati**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>Creazione di oggetti e matrici
Un'altra funzione fondamentale dell'API SQL di DocumentDB è la creazione di matrici/oggetti. Nell'esempio precedente hello, si noti che è stato creato un nuovo oggetto JSON. Analogamente, uno inoltre possibile creare matrici come illustrato nell'hello seguono esempi:

**Query**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**Risultati**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>Parola chiave VALUE
Hello **valore** (parola chiave) fornisce un valore JSON tooreturn modo. Ad esempio, le query hello illustrata di seguito restituisce hello scalare `"Hello World"` anziché `{$1: "Hello World"}`.

**Query**

    SELECT VALUE "Hello World"

**Risultati**

    [
      "Hello World"
    ]


la query seguente Hello restituisce il valore JSON hello senza hello `"address"` etichetta nei risultati di hello.

**Query**

    SELECT VALUE f.address
    FROM Families f    

**Risultati**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

Hello esempio estende questo tooshow come valori primitivi tooreturn JSON (livello hello foglia dell'albero di hello JSON). 

**Query**

    SELECT VALUE f.address.state
    FROM Families f    

**Risultati**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>Operatore *
operatore speciale (*) Hello è supportato tooproject hello documento come-è. Se utilizzato, deve essere hello proiettati solo campo. Benché una query come `SELECT * FROM Families f` sia valida, `SELECT VALUE * FROM Families f ` e `SELECT *, f.id FROM Families f ` non lo sono.

**Query**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Risultati**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>Operatore TOP
parola chiave TOP Hello può essere utilizzato toolimit hello numero di valori da una query. Se TOP viene utilizzato in combinazione con una clausola ORDER BY hello, set di risultati di hello è limitato toohello primo numero N di valori ordinati. in caso contrario, restituisce hello primo numero N di risultati in un ordine non definito. Come procedura consigliata, in un'istruzione SELECT, utilizzare sempre una clausola ORDER BY con la clausola TOP hello. Si tratta pertanto hello toopredictably indicano quali righe sono interessate dalla clausola TOP. 

**Query**

    SELECT TOP 1 * 
    FROM Families f 

**Risultati**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

È possibile usare TOP con un valore costante (come illustrato in precedenza) o con un valore della variabile usando le query con parametri. Per altre informazioni dettagliate, vedere le query con parametri seguenti.

### <a id="Aggregates"></a>Funzioni di aggregazione
È inoltre possibile eseguire le aggregazioni in hello `SELECT` clausola. Le funzioni di aggregazione eseguono un calcolo su un set di valori e restituiscono un singolo valore. Ad esempio, hello query seguente restituisce il conteggio di hello dei documenti della famiglia insieme hello.

**Query**

    SELECT COUNT(1) 
    FROM Families f 

**Risultati**

    [{
        "$1": 2
    }]

È inoltre possibile restituire valore scalare di hello di hello aggregazione utilizzando hello `VALUE` (parola chiave). Ad esempio, hello query seguente restituisce il conteggio di hello dei valori come un singolo numero:

**Query**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**Risultati**

    [ 2 ]

È anche possibile eseguire aggregazioni combinate a filtri. Ad esempio, hello query seguente restituisce il conteggio di hello dei documenti con indirizzo hello in stato di Washington hello.

**Query**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**Risultati**

    [ 1 ]

Hello nella tabella seguente mostra hello elenco di funzioni di aggregazione supportate nell'API di DocumentDB. `SUM`e `AVG` vengono eseguite su valori numerici, mentre `COUNT`, `MIN` e `MAX` possono essere eseguite su numeri, stringhe, valori booleani e valori null. 

| Utilizzo | Descrizione |
|-------|-------------|
| COUNT | Restituisce hello numero di elementi in espressione hello. |
| SUM   | Restituisce hello somma di tutti i valori hello hello espressione. |
| MIN   | Restituisce hello valore minimo nell'espressione hello. |
| MAX   | Restituisce hello valore massimo nell'espressione hello. |
| MEDIA   | Restituisce hello Media dei valori hello in espressione hello. |

Le aggregazioni possono essere eseguite anche sui risultati di hello di un'iterazione della matrice. Per altre informazioni, vedere [Array Iteration in Queries](#Iteration) (Iterazione della matrice nelle query).

> [!NOTE]
> Quando tramite hello Esplora Query del portale di Azure, si noti che le query di aggregazione possono restituire hello risultati aggregati parzialmente su una pagina di query. Hello SDK produce un singolo valore cumulativo in tutte le pagine. 
> 
> Ordine in query di aggregazione tooperform tramite codice, è necessario .NET SDK 1.12.0, .NET Core SDK 1.1.0 o SDK per Java 1.9.5 o versione successiva.    
>

## <a id="OrderByClause"></a>Clausola ORDER BY
Come in SQL ANSI, è possibile includere una clausola Order By facoltativa durante l'esecuzione di query. clausola di Hello può includere un parametro facoltativo ASC/DESC toospecify hello ordine degli argomenti in cui devono essere recuperati i risultati.

Ad esempio, ecco una query che recupera i gruppi in ordine di hello residenti il nome di città.

**Query**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**Risultati**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

Di seguito è una query che recupera i gruppi nell'ordine della data di creazione, che viene archiviata come un numero che rappresenta di hello valore epoch, ovvero il tempo trascorso dall'1 gennaio 1970, in secondi.

**Query**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**Risultati**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>Concetti avanzati relativi ai database e alle query SQL

### <a id="Iteration"></a>Iterazione
È stato aggiunto un nuovo costrutto di tramite hello **IN** parola chiave DocumentDB API tooprovide supporto tecnico di SQL per scorrere le matrici JSON. origine FROM Hello fornisce supporto per l'iterazione. Iniziamo con hello di esempio seguente:

**Query**

    SELECT * 
    FROM Families.children

**Risultati**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

Ora diamo un'occhiata a un'altra query che esegue l'iterazione figlio nella raccolta di hello. Si noti la differenza hello nella matrice di output di hello. Questo esempio suddivide `children` e appiattisce risultati hello in una matrice.  

**Query**

    SELECT * 
    FROM c IN Families.children

**Risultati**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

Può essere ulteriormente utilizzati toofilter in ogni singola voce della matrice di hello, come illustrato nell'esempio seguente hello:

**Query**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**Risultati**  

    [{
      "givenName": "Lisa"
    }]

È anche possibile eseguire l'aggregazione per il risultato di hello di iterazione di matrice. Ad esempio, hello nella query seguente conta hello figli tra tutti i gruppi.

**Query**

    SELECT COUNT(child) 
    FROM child IN Families.children

**Risultati**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>Join
In un database relazionale, è importante hello necessità toojoin tra le tabelle. Di hello logico toodesigning corollario normalizzato schemi. Toothis contrarie, l'API DocumentDB riguarda il modello di dati denormalizzati hello di documenti privi di schema. Si tratta hello equivalente logico di un "self-join".

sintassi di Hello che supporta la lingua di hello è JOIN JOIN < from_source2 > di < from_source1 >... JOIN <from_sourceN>. In generale, restituisce un set di tuple **N** (tupla con valori **N**). Ogni tupla ha valori prodotti dall'iterazione di tutti gli alias della raccolta sui rispettivi set. In altre parole, questo è un prodotto incrociato completo dei set di hello che fanno parte di join hello.

Hello esempi seguenti viene illustrato il funzionamento clausola JOIN hello. Nell'esempio seguente di hello, hello risulta vuota poiché hello prodotto incrociato di ogni documento di origine e un set vuoto è vuoto.

**Query**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**Risultati**  

    [{
    }]


Nell'esempio seguente di hello, join hello è compreso tra la radice del documento hello e hello `children` subroot. È un prodotto incrociato tra due oggetti JSON. fatti Hello che gli elementi figlio è una matrice non sono efficaci per hello JOIN poiché ci stiamo gestiscono un solo nodo radice è una matrice di figli hello. Pertanto il risultato di hello contiene solo due risultati, poiché il prodotto incrociato di tutti i documenti con matrice hello hello produce esattamente un solo documento.

**Query**

    SELECT f.id
    FROM Families f
    JOIN f.children

**Risultati**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


Hello di esempio seguente viene illustrato un join di più tradizionale:

**Query**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**Risultati**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



Hello in primo luogo toonote è tale hello `from_source` di hello **JOIN** clausola è un iteratore. In tal caso, il flusso di hello in questo caso è come segue:  

* Espandere ogni elemento figlio **c** nella matrice hello.
* Applicare un prodotto incrociato con la radice del documento hello hello **f** con ogni elemento figlio **c** che è stata semplificata nel primo passaggio hello.
* Infine, progetto oggetto radice hello **f** solo proprietà name. 

primo documento Hello (`AndersenFamily`) contiene un solo elemento figlio, in modo hello set di risultati contiene solo un documento di toothis corrispondente dell'oggetto singolo. secondo documento Hello (`WakefieldFamily`) contiene due elementi figlio. In tal caso, hello prodotto incrociato produce un oggetto separato per ogni elemento figlio, determinando in tal modo due oggetti, uno per ogni documento di toothis figlio corrispondente. radice Hello campi in entrambi questi documenti sono hello stesso, come previsto in un prodotto incrociato.

Hello reale utilità hello JOIN è tooform tuple dal prodotto incrociato hello in una forma che altrimenti tooproject difficile. Inoltre, come si può vedere nel seguente esempio hello, è possibile filtrare in combinazione hello di una tupla hello degli che consente l'utente ha scelto una condizione soddisfatta da tuple hello complessiva.

**Query**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**Risultati**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



In questo esempio è un'estensione naturale della hello sopra riportato, esegue un join double. In tal caso, hello prodotto incrociato possono essere visualizzato come hello pseudo-codice seguente:

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily` ha un figlio che ha un animale domestico. In tal caso, hello prodotto incrociato restituisce una riga (1\*1\*1) da questa famiglia. Tuttavia, la famiglia WakefieldFamily ha due figli, ma un solo figlio, "Jesse", ha animali domestici. Jesse ha però due animali domestici. Di conseguenza hello prodotto incrociato restituisce 1\*1\*2 = 2 righe da questa famiglia.

Nell'esempio riportato di seguito hello, è un ulteriore filtro su `pet`. Consente di escludere tutte le tuple hello in cui non è "Shadow" hello pet nome. Si noti che è in grado di toobuild tuple da matrici, filtro in uno qualsiasi degli elementi di hello di tupla hello e qualsiasi combinazione di elementi di hello del progetto. 

**Query**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**Risultati**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>Integrazione JavaScript
DB Cosmos Azure fornisce un modello di programmazione per l'esecuzione di logica dell'applicazione basata su JavaScript direttamente nelle raccolte di hello in termini di stored procedure e trigger. Ciò consente quanto segue:

* Operazioni CRUD transazionale di possibilità toodo ad alte prestazioni e le query su documenti in una raccolta in virtù di integrazione hello del runtime JavaScript direttamente nel motore di database hello. 
* Modellazione naturale del flusso di controllo, definizione dell'ambito delle variabili e assegnazione e integrazione di primitivi di gestione delle eccezioni con transazioni di database. Per ulteriori informazioni sul supporto di Azure Cosmos DB per l'integrazione con JavaScript, consultare la documentazione di toohello JavaScript sul lato server programmabilità.

### <a id="UserDefinedFunctions"></a>Funzioni definite dall'utente (UDF)
Oltre ai tipi di hello già definiti in questo articolo, SQL API DocumentDB fornisce il supporto per utente definite funzioni (funzione definita dall'utente). In particolare, funzioni definite dall'utente scalari sono supportate in cui gli sviluppatori di hello possono passare zero o più argomenti e restituire un risultato singolo argomento. Verrà quindi eseguito un controllo per verificare che ciascuno di questi argomenti sia un valore JSON legale.  

la sintassi SQL API DocumentDB Hello viene estesa toosupport logica dell'applicazione personalizzata utilizzando le funzioni definite dall'utente. Le UDF possono essere registrate con l'API di DocumentDB ed è quindi possibile fare loro riferimento come parte di una query SQL. In effetti, funzioni definite dall'utente sono exquisitely hello progettato toobe richiamata da una query. Come scelta toothis corollario, funzioni definite dall'utente non dispongono di accesso toohello contesto oggetto cui hello altre JavaScript dispongono di tipi (stored procedure e trigger). Poiché le query vengono eseguite in sola lettura, è possibile eseguirle sulle repliche primarie o secondarie. Pertanto, funzioni definite dall'utente sono progettati toorun nelle repliche secondarie, a differenza di altri tipi di JavaScript.

Di seguito è riportato un esempio di come una funzione definita dall'utente possono essere registrati nel database DB Cosmos hello, in particolare in una raccolta documenti.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

esempio Hello crea una funzione definita dall'utente il cui nome è `REGEX_MATCH`. Accetta due valori stringa JSON `input` e `pattern` e controlla se le corrispondenze prima hello hello criterio specificato in hello secondo funzione JavaScript string.match().

È ora possibile usare questa UDF in una query in una proiezione. Funzioni definite dall'utente deve essere qualificato con prefisso distinzione maiuscole/minuscole hello "definita dall'utente." quando chiamate dall'interno delle query. 

> [!NOTE]
> Precedente too3/17/2015 Cosmos DB supportato chiamate di funzione definita dall'utente senza hello "definita dall'utente." come SELECT REGEX_MATCH(). Questo modello di chiamata è stato deprecato.  
> 
> 

**Query**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**Risultati**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

funzione definita dall'utente Hello consente anche all'interno di un filtro come illustrato nell'esempio hello riportato di seguito, anche qualificato con hello "definita dall'utente." prefisso:

**Query**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**Risultati**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


In sostanza, le UDF sono espressioni scalari valide che è possibile usare sia nelle proiezioni sia nei filtri. 

tooexpand alimentato hello di funzioni definite dall'utente, si esaminerà un altro esempio con la logica condizionale:

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


Di seguito è riportato un esempio che esercizi hello funzione definita dall'utente.

**Query**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**Risultati**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


Come hello showcase esempi precedenti, funzioni definite dall'utente integrarlo power hello del linguaggio JavaScript hello SQL API DocumentDB tooprovide una ricca interfaccia programmabile toodo procedurale, condizionale logica complessa con l'aiuto di hello del runtime JavaScript incorporato funzionalità.

SQL API DocumentDB fornisce argomenti di hello toohello funzioni definite dall'utente per ogni documento nell'origine hello fase hello corrente (clausola WHERE o clausola SELECT) di elaborazione hello funzione definita dall'utente. Hello risultato viene incorporato hello generale della pipeline di esecuzione senza problemi. Se le proprietà di hello parametri di funzione definita dall'utente hello tooby cui viene fatto riferimento non sono disponibili in hello valore JSON, hello parametro viene considerato come non definito e pertanto hello viene ignorata completamente la chiamata di funzione definita dall'utente. Allo stesso modo se il risultato di hello della funzione definita dall'utente hello è definito, non è incluso nel risultato hello. 

In sintesi, funzioni definite dall'utente sono logica di business complessa toodo validi strumenti come parte di query hello.

### <a name="operator-evaluation"></a>Valutazione degli operatori
In virtù di hello di essere un database, JSON COSMOS DB, disegna parallels con operatori JavaScript e la semantica di valutazione. Mentre DB Cosmos tenta la semantica JavaScript toopreserve in termini di supporto JSON, valutazione operazione hello devia in alcuni casi.

In SQL API DocumentDB, a differenza di SQL tradizionale, hello tipi di valori, spesso non noti fino a quando i valori hello vengono recuperati dal database. In ordine tooefficiently eseguire query, la maggior parte degli operatori hello hanno requisiti di tipo strict. 

L'API SQL di DocumentDB non esegue conversioni implicite, a differenza di JavaScript. Ad esempio, una query come `SELECT * FROM Person p WHERE p.Age = 21` corrisponde a documenti che contengono una proprietà Age il cui valore è 21. Qualsiasi altro documento la cui proprietà Age corrisponde alla stringa "21", o ad altre possibili variazioni come "021", "21.0", "0021", "00021" e così via, non verrà trovato. Si tratta invece toohello JavaScript in cui i valori stringa hello sono toonumbers eseguito in modo implicito il cast (basato su operatore, ad esempio: = =). Questa scelta è fondamentale per la ricerca di indici corrispondenti nell'API SQL di DocumentDB. 

## <a name="parameterized-sql-queries"></a>Query SQL con parametri
COSMOS DB supporta le query con parametri espressi con hello familiare notazione @. SQL con parametri fornisce solide capacità di gestione ed escape dell'input utente, evitando l'esposizione accidentale di dati mediante attacchi SQL injection. 

Ad esempio, è possibile scrivere una query che accetta come parametri il cognome e lo stato di residenza e quindi eseguirla per diversi valori di cognome e stato di residenza in base all'input dell'utente.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

Questa richiesta può quindi essere inviata tooCosmos DB come una query con parametri di JSON, come illustrato di seguito.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

Hello argomento tooTOP può essere impostato utilizzando le query con parametri, come illustrato di seguito.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

I valori dei parametri possono essere qualsiasi valore JSON valido (stringhe, numeri, valori booleani, valori null, persino matrici o valori JSON annidati). Inoltre, dato che Cosmos DB è senza schema, i parametri non vengono convalidati rispetto a qualsiasi tipo.

## <a id="BuiltinFunctions"></a>Funzioni predefinite
Cosmos DB supporta anche una serie di funzioni predefinite per le operazioni comuni, che possono essere usate all'interno di query come le funzioni definite dall'utente (UDF).

| Gruppo di funzioni          | Operazioni                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Funzioni matematiche  | ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, gradi, PI, radianti, SIN e TAN |
| Funzioni di controllo del tipo | IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE                                                           |
| Funzioni stringa        | CONCAT, CONTAINS, ENDSWITH, INDEX_OF, sinistra, lunghezza, inferiore, LTRIM, REPLACE, replica, inversa, destra, RTRIM, STARTSWITH, SUBSTRING e superiore       |
| Funzioni di matrice         | ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH e ARRAY_SLICE                                                                                         |
| Funzioni spaziali       | ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID e ST_ISVALIDDETAILED                                                                           | 

Se attualmente si utilizza una funzione definita dall'utente (UDF) per il quale è ora disponibile una funzione predefinita, è necessario usare la funzione incorporata corrispondente di hello come saranno toobe toorun di più veloce e più efficiente. 

### <a name="mathematical-functions"></a>Funzioni matematiche
Hello funzioni matematiche eseguono un calcolo, in base ai valori di input forniti come argomenti e restituiscono un valore numerico. Di seguito è riportata una tabella delle funzioni matematiche predefinite supportate.


| Uso | Descrizione |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS (num_expr)](#bk_abs) | Restituisce hello assoluto (positivo) il valore di hello specificato espressione numerica. |
| [CEILING (num_expr)](#bk_ceiling) | Restituisce hello più piccolo valore integer maggiore di o uguale a, hello espressione numerica specificata. |
| [FLOOR (num_expr)](#bk_floor) | Restituisce l'intero più grande hello minore o uguale toohello specificato espressione numerica. |
| [EXP (num_expr)](#bk_exp) | Esponente hello restituisce di hello specificato espressione numerica. |
| [LOG (num_expr [,base])](#bk_log) | Logaritmo naturale di hello restituisce di hello specificato espressione numerica o logaritmo hello utilizzando hello specificato base |
| [LOG10 (num_expr)](#bk_log10) | Restituisce valori logaritmico hello in base 10 di hello specificato espressione numerica. |
| [ROUND (num_expr)](#bk_round) | Restituisce un valore numerico, il valore intero più vicino di toohello arrotondato. |
| [TRUNC (num_expr)](#bk_trunc) | Restituisce un valore numerico, il valore intero più vicino di toohello troncato. |
| [SQRT (num_expr)](#bk_sqrt) | Radice quadrata di hello restituisce di hello specificato espressione numerica. |
| [SQUARE (num_expr)](#bk_square) | Hello restituisce quadrato di hello specificato espressione numerica. |
| [POWER (num_expr, num_expr)](#bk_power) | Restituisce hello potenza hello specificato valore toohello espressione numerica specificata. |
| [SIGN (num_expr)](#bk_sign) | Espressione numerica restituisce hello sign valore (-1, 0, 1) di hello. |
| [ACOS (num_expr)](#bk_acos) | Angolo di hello restituisce, in radianti, il cui coseno è hello espressione numerica specificata; denominato anche arcocoseno. |
| [ASIN (num_expr)](#bk_asin) | Angolo di hello restituisce, in radianti, il cui seno è hello specificato espressione numerica. Detta anche arcoseno. |
| [ATAN (num_expr)](#bk_atan) | Angolo di hello restituisce, in radianti, la cui tangente è hello specificato espressione numerica. Detta anche arcotangente. |
| [ATN2 (num_expr)](#bk_atn2) | Restituisce hello angolo, espresso in radianti, tra l'asse x positivo hello e raggio hello dal punto di toohello origine hello (y, x), dove x e y sono valori hello di hello due espressioni float specificate. |
| [COS (num_expr)](#bk_cos) | Restituisce hello coseno trigonometrico hello specificato angolo, espresso in radianti, in hello espressione specificata. |
| [COT (num_expr)](#bk_cot) | Restituisce hello cotangente trigonometrica hello specificato angolo, espresso in radianti, in hello specificato espressione numerica. |
| [DEGREES (num_expr)](#bk_degrees) | Restituisce hello angolo corrispondente in gradi di un angolo specificato espresso in radianti. |
| [PI ()](#bk_pi) | Restituisce hello valore costante di pi greco. |
| [RADIANS (num_expr)](#bk_radians) | Restituisce radianti quando viene immessa un'espressione numerica, espresso in gradi. |
| [SIN (num_expr)](#bk_sin) | Restituisce hello seno trigonometrico hello specificato angolo, espresso in radianti, in hello espressione specificata. |
| [TAN (num_expr)](#bk_tan) | Tangente di hello restituisce dell'espressione di input hello, in hello espressione specificata. |

Ad esempio, è ora possibile eseguire query hello seguente:

**Query**

    SELECT VALUE ABS(-4)

**Risultati**

    [4]

Hello differenza principale tooANSI funzioni rispetto Cosmos DB SQL è che si trovano toowork progettato correttamente con i dati dello schema senza schema e misto. Ad esempio, se si dispone di un documento in cui la proprietà di dimensione hello mancante, o con un valore non numerico come "sconosciuto", quindi il documento hello viene ignorato, anziché restituire un errore.

### <a name="type-checking-functions"></a>Funzioni di controllo del tipo
funzioni di controllo di tipo Hello consentono di tipo hello toocheck di un'espressione all'interno di query SQL. Tipo di funzioni di controllo possono essere utilizzato tipo hello toodetermine delle proprietà all'interno di documenti in tempo reale di hello quando è sconosciuto o variabile. Di seguito è riportata una tabella di funzioni predefinite di controllo del tipo supportate.

<table>
<tr>
  <td><strong>Utilizzo</strong></td>
  <td><strong>Descrizione</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></td>
  <td>Restituisce un valore booleano che indica se il tipo di hello del valore di hello è una matrice.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></td>
  <td>Restituisce un valore booleano che indica se il tipo di hello del valore di hello è un valore booleano.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></td>
  <td>Restituisce un valore booleano che indica se il tipo di hello del valore di hello è null.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></td>
  <td>Restituisce un valore booleano che indica se il tipo di hello del valore di hello è un numero.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></td>
  <td>Restituisce un valore booleano che indica se il tipo di hello del valore di hello è un oggetto JSON.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></td>
  <td>Restituisce un valore booleano che indica se il tipo di hello del valore di hello è una stringa.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></td>
  <td>Restituisce un valore booleano che indica se la proprietà hello è stata assegnata un valore.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></td>
  <td>Restituisce un valore booleano che indica se il tipo di hello del valore di hello è una stringa, numero, booleano o null.</td>
</tr>

</table>

Utilizzo di queste funzioni, è possibile eseguire query hello seguente:

**Query**

    SELECT VALUE IS_NUMBER(-4)

**Risultati**

    [true]

### <a name="string-functions"></a>Funzioni stringa
Hello funzioni scalari seguenti eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, numerico o booleano. Ecco una tabella di funzioni per stringhe:

| Uso | Description |
| --- | --- |
| [LENGTH (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |Espressione di stringa specificata di hello restituisce il numero di caratteri di hello |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |Restituisce una stringa che rappresenta il risultato di hello del concatenamento di due o più valori di stringa. |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |Restituisce parte di un'espressione stringa. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |Restituisce un valore booleano che indica se prima espressione di stringa hello termina con hello secondo |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |Restituisce un valore booleano che indica se prima espressione di stringa hello termina con hello secondo |
| [CONTAINS (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |Restituisce un valore booleano che indica se prima espressione di stringa hello contiene hello secondo. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Restituisce hello a partire dalla posizione della prima occorrenza di hello della seconda espressione stringa hello all'hello prima espressione stringa specificata oppure -1 se la stringa hello non viene trovata. |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |Restituisce la parte sinistra di una stringa di hello con hello specificato numero di caratteri. |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Hello restituisce parte destra di una stringa con hello numero specificato di caratteri. |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |Restituisce un'espressione stringa dopo aver rimosso gli spazi vuoti iniziali. |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |Restituisce un'espressione stringa dopo la rimozione di tutti gli spazi vuoti finali. |
| [LOWER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |Restituisce un'espressione stringa dopo aver convertito i caratteri maiuscoli in caratteri toolowercase di dati. |
| [UPPER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |Restituisce un'espressione stringa dopo la conversione toouppercase di dati carattere minuscolo. |
| [REPLACE (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |Sostituisce tutte le occorrenze di un valore stringa specificato con un altro valore stringa. |
| [REPLICATE (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |Ripete un valore stringa in un numero di volte specificato. |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Restituisce l'inverso di hello di un valore stringa. |

Utilizzo di queste funzioni, è possibile eseguire query hello seguente. Ad esempio, si può restituire il nome della famiglia di hello in lettere maiuscole come indicato di seguito:

**Query**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**Risultati**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

In alternativa, è possibile concatenare stringhe come in questo esempio:

**Query**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**Risultati**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


Funzioni di stringa possono essere utilizzate anche in hello in risultati toofilter clausola, come nel seguente esempio hello:

**Query**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**Risultati**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>Funzioni di matrice
Hello funzioni scalari seguenti esegue un'operazione su un valore di input di matrice e restituito numerico, valore booleano o di matrice. La tabella seguente include funzioni di matrice predefinite:

| Uso | Description |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |Restituisce il numero di elementi di hello hello specificata espressione di matrice. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |Restituisce una matrice che rappresenta il risultato di hello della concatenazione di due o più valori della matrice. |
| [ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |Restituisce un valore booleano che indica se la matrice hello contiene hello valore specificato. Può specificare se la corrispondenza hello è completo o parziale. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |Restituisce parte di un'espressione di matrice. |

Funzioni di matrice possono essere matrici toomanipulate utilizzati all'interno di JSON. Ad esempio, ecco una query che restituisce tutti i documenti in cui uno degli elementi padre hello è "Robin Wakefield". 

**Query**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**Risultati**

    [{
      "id": "WakefieldFamily"
    }]

È possibile specificare un frammento parziale per gli elementi corrispondenti all'interno della matrice hello. Hello nella query seguente consente di trovare tutti gli elementi padre con hello `givenName` di `Robin`.

**Query**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**Risultati**

    [{
      "id": "WakefieldFamily"
    }]


Di seguito è riportato un altro che usa ARRAY_LENGTH tooget hello numero di elementi figlio per ogni famiglia.

**Query**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**Risultati**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>Funzioni spaziali
COSMOS DB supporta hello seguendo le funzioni predefinite di Open Geospatial Consortium (OGC) per l'esecuzione di query geospaziale. 

<table>
<tr>
  <td><strong>Utilizzo</strong></td>
  <td><strong>Descrizione</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr, point_expr)</td>
  <td>Restituisce la distanza hello tra espressioni di hello due LineString, Polygon o punto GeoJSON.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Restituisce un'espressione booleana che indica se hello prima GeoJSON oggetto (punto, poligono o LineString) all'interno di hello secondo GeoJSON oggetto (punto, poligono o LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Restituisce un'espressione booleana che indica se si intersecano hello due GeoJSON oggetti specificati (punto, poligono o LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Restituisce un valore booleano che indica se hello LineString, Polygon o punto GeoJSON espressione è valida.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Restituisce un valore JSON che contiene un valore booleano se hello specificato LineString, Polygon o punto GeoJSON espressione sia valido e se non è valido, è inoltre hello motivo come valore stringa.</td>
</tr>
</table>

Le funzioni spaziali possono essere utilizzati tooperform prossimità query sui dati spaziali. Ad esempio, ecco una query che restituisce che tutti i prodotti della famiglia di documenti che è all'interno di 30 km di hello posizione specificata usando hello ST_DISTANCE funzione predefinita. 

**Query**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Risultati**

    [{
      "id": "WakefieldFamily"
    }]

Per informazioni dettagliate sul supporto geospaziale in Cosmos DB, vedere [Uso dei dati geospaziali in Azure Cosmos DB](geospatial.md). Che esegue il wrapping di funzioni spaziali e hello sintassi SQL per Cosmos DB. Ora esaminata in modo LINQ query funzioni e le relative modalità di interazione con la sintassi di hello abbiamo visto finora.

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
LINQ è un modello di programmazione .NET che esprime il calcolo come query su flussi di oggetti. COSMOS DB fornisce un toointerface libreria lato client con LINQ facilitando la conversione tra JSON e gli oggetti .NET e un mapping da un subset di LINQ query query tooCosmos DB. 

immagine Hello seguente mostra l'architettura hello di supportare le query LINQ tramite DB Cosmos.  Client DB Cosmos di hello gli sviluppatori possono creare un **IQueryable** che direttamente le query hello Cosmos DB provider di query, che quindi converte query LINQ hello in una query Cosmos DB dell'oggetto. query Hello viene quindi passato toohello tooretrieve server DB Cosmos un set di risultati in formato JSON. Hello ha restituito i risultati vengono deserializzati in un flusso di oggetti .NET sul lato client hello.

![Architettura di supporto delle query LINQ usando API DocumentDB - Sintassi SQL, linguaggio di query JSON, concetti relativi ai database e query SQL][1]

### <a name="net-and-json-mapping"></a>Mapping .NET e JSON
mapping di Hello tra gli oggetti .NET e documenti JSON è naturale, viene eseguito il mapping di ogni campo del membro dati oggetto JSON tooa, dove il nome di campo hello è stato eseguito il mapping di parte di "chiave" toohello dell'oggetto hello e parte "value" hello è parte del valore toohello in modo ricorsivo il mapping dell'oggetto hello. Prendere in considerazione hello di esempio seguente: hello famiglia l'oggetto creato è documento JSON toohello mappato come illustrato di seguito. E viceversa, documento JSON hello oggetto .NET tooa indietro mappato.

**Classe C#**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>Conversione tooSQL LINQ
provider di query Cosmos DB Hello esegue il mapping di un lavoro richiesto più di una query LINQ in una query SQL del database Cosmos. In hello seguente descrizione, si presuppone il lettore di hello ha una conoscenza di base di LINQ.

In primo luogo, per il sistema di tipi di hello, sostegno tutti JSON i tipi primitivi, tipi numerici, boolean, string e null. Sono supportati solo questi tipi JSON. Hello seguenti espressioni scalari è supportata.

* Valori costanti – tra valori costanti di tipi di dati primitivi hello in fase di hello hello query viene valutata.
* Espressioni di indice di matrice delle proprietà-queste espressioni fanno riferimento toohello proprietà di un oggetto o un elemento di matrice.
  
     family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n è una variabile di tipo int
* Espressioni aritmetiche: includono espressioni aritmetiche comuni su valori numerici e booleani. Per l'elenco completo di hello, consultare toohello specifica di SQL.
  
     2 * family.children[0].grade;    x + y;
* Espressione di confronto stringa - tra cui il confronto di un valore di stringa costante toosome valore stringa.  
  
     mother.familyName == "Smith";    child.givenName == s; //s è una variabile di stringa
* Espressione di creazione oggetto/matrice: restituisce un oggetto di tipo valore composito o tipo anonimo o ancora un matrice di tali oggetti. Questi valori non possono essere annidati.
  
     new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //un tipo anonimo con due campi              
     new int[] { 3, child.grade, 5 };

### <a id="SupportedLinqOperators"></a>Elenco di operatori LINQ supportati
Di seguito è riportato un elenco di operatori LINQ supportati nel provider LINQ hello incluso hello DocumentDB .NET SDK.

* **Selezionare**: proiezioni traducono toohello SQL SELECT, incluse la costruzione di oggetti
* **Dove**: traslazione toohello SQL in cui i filtri e supporta la conversione tra & &, | | e! operatori SQL toohello
* **SelectMany**: consente la rimozione della clausola JOIN SQL toohello di matrici. Può essere utilizzato toochain/nidificare le espressioni toofilter sugli elementi di matrice
* **OrderBy e OrderByDescending**: converte tooORDER BY crescente/decrescente
* Operatori di aggregazione **Count**, **Sum**, **Min**, **Max** e **Average** e relativi equivalenti asincroni **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** e **AverageAsync**.
* **CompareTo**: converte toorange confronti. In genere usato per le stringhe in quanto non sono confrontabili in .NET
* **Richiedere**: converte toohello SQL TOP per limitare i risultati da una query
* **Funzioni matematiche**: supporta la conversione da. Abs, Acos, Asin di rete, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, troncare toohello equivalente SQL le funzioni predefinite.
* **Funzioni stringa**: supporta la conversione da. Concat, Contains, EndsWith del NET, IndexOf, Count, ToLower, TrimStart, Replace, inversa, TrimEnd, StartsWith, SubString, ToUpper toohello equivalente SQL funzioni predefinite.
* **Funzioni di matrice**: supporta la conversione da. Concat, Contains e conteggio toohello equivalente SQL funzioni predefinite del NET.
* **Le funzioni di estensione Geospatial**: supporta la conversione da metodi stub distanza, entro, IsValid e IsValidDetailed toohello equivalente SQL le funzioni predefinite.
* **Funzione di estensione della funzione definita dall'utente**: conversione supporta da hello stub metodo UserDefinedFunctionProvider.Invoke toohello corrispondente-funzione definita dall'utente.
* **Varie**: supporta la conversione di hello coalesce e agli operatori condizionali. Può essere convertita Contains tooString CONTAINS, ARRAY_CONTAINS o hello IN SQL, a seconda del contesto.

### <a name="sql-query-operators"></a>Operatori di query SQL
Di seguito sono riportati alcuni esempi che illustrano la modalità di conversione alcuni degli operatori di query LINQ standard hello tooCosmos DB le query.

#### <a name="select-operator"></a>Operatore Select
sintassi di Hello è `input.Select(x => f(x))`, dove `f` è un'espressione scalare.

**Espressione lambda LINQ**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**Espressione lambda LINQ**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**Espressione lambda LINQ**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>Operatore SelectMany
sintassi di Hello è `input.SelectMany(x => f(x))`, dove `f` è un'espressione scalare che restituisce un tipo di raccolta.

**Espressione lambda LINQ**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Operatore Where
sintassi di Hello è `input.Where(x => f(x))`, dove `f` è un'espressione scalare, che restituisce un valore booleano.

**Espressione lambda LINQ**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**Espressione lambda LINQ**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>Query SQL composte
Hello sopra gli operatori possono essere composti tooform query più efficace. Poiché DB Cosmos supporta raccolte annidate, composizione hello può essere concatenato o nidificati.

#### <a name="concatenation"></a>Concatenazione
sintassi di Hello è `input(.|.SelectMany())(.Select()|.Where())*`. Una query concatenata può iniziare con una query `SelectMany` facoltativa, seguita da più operatori `Select` o `Where`.

**Espressione lambda LINQ**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**Espressione lambda LINQ**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**Espressione lambda LINQ**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**Espressione lambda LINQ**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>Annidamento
sintassi di Hello è `input.SelectMany(x=>x.Q())` dove Q è un `Select`, `SelectMany`, o `Where` operatore.

In una query annidata, la query interna hello è tooeach applicato elemento della raccolta esterna hello. Una caratteristica importante è che la query interna hello può fare riferimento a toohello campi di elementi di hello nella raccolta di outer hello come self-join.

**Espressione lambda LINQ**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**Espressione lambda LINQ**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**Espressione lambda LINQ**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>Esecuzione di query SQL
Cosmos DB espone risorse tramite un'API REST che può essere chiamata da qualsiasi linguaggio in grado di effettuare richieste HTTP/HTTPS. In Cosmos DB sono anche disponibili librerie di programmazione per diversi linguaggi comuni, come NET, Node.js, JavaScript e Python. Hello API REST e hello diverse librerie tutti supportano l'esecuzione di query tramite SQL. Hello .NET SDK supporta inoltre query tooSQL LINQ.

Hello seguenti esempi viene illustrato come toocreate una query e li inviano rispetto a un account di database DB Cosmos.

### <a id="RestAPI"></a>API REST
Cosmos DB offre un modello di programmazione aperto RESTful su HTTP. È possibile effettuare il provisioning degli account di database usando una sottoscrizione di Azure. modello di risorsa Cosmos DB Hello è costituito da un set di risorse con un account di database, ognuno dei quali è indirizzabile utilizzando un URI logico e stabile. Un set di risorse è tooas di cui si fa riferimento un feed in questo documento. Un account di database è costituito da un set di database, ognuno dei quali include più raccolte, che possono contenere documenti, UDF e altri tipi di risorse.

modello di interazione di base Hello con queste risorse è tramite verbi hello HTTP GET, PUT, POST e DELETE con la relativa interpretazione standard. verbo POST Hello viene utilizzato per la creazione di una nuova risorsa, per l'esecuzione di una stored procedure o per l'esecuzione di una query DB Cosmos. Le query sono sempre operazioni di sola lettura senza nessun effetto collaterale.

Hello esempi seguenti viene illustrato un POST per una query di DocumentDB API effettuata una raccolta che contiene due documenti di esempio hello che abbiamo esaminato finora. query Hello dispone di un filtro semplice nella proprietà di nome hello JSON. Si noti utilizzo hello di hello `x-ms-documentdb-isquery` e Content-Type: `application/query+json` toodenote intestazioni che hello operazione è una query.

**Richiesta**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**Risultati**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


Hello secondo esempio viene illustrata una query più complessa che restituisce più risultati da join hello.

**Richiesta**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**Risultati**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


Se i risultati di una query non possono essere contenuta all'interno di una singola pagina dei risultati, quindi hello API REST restituisce un token di continuazione mediante hello `x-ms-continuation-token` intestazione della risposta. I client possono impaginare risultati includendo l'intestazione hello in risultati successivi. è anche possibile controllare il numero di Hello di risultati per pagina tramite hello `x-ms-max-item-count` intestazione dei numeri. Se la query specificata hello dispone di una funzione di aggregazione come `COUNT`, quindi pagina query hello può restituire un valore aggregato parzialmente sulla pagina hello dei risultati. i client Hello deve eseguire un'aggregazione di secondo livello su questi risultati tooproduce hello finale risultati, ad esempio, somma conteggi hello restituiti nel numero totale di hello singole pagine tooreturn hello.

criteri di verifica coerenza di dati toomanage hello per le query, utilizzare hello `x-ms-consistency-level` intestazione come tutte le richieste API REST. Per coerenza di sessione, è più recente hello di tooalso obbligatorio eco `x-ms-session-token` intestazione Cookie nella richiesta di query hello. Hello criteri di indicizzazione della raccolta di query possono inoltre influire sulla coerenza hello dei risultati della query. Con le impostazioni dei criteri di indicizzazione predefiniti di hello, per le raccolte hello indice è sempre aggiornati con il contenuto del documento hello e risultati corrispondano a coerenza hello scelta per i dati di query. Se Criteri di indicizzazione hello tooLazy flessibile, le query possono restituire risultati non aggiornati. Per altre informazioni, vedere [Livelli di coerenza di Azure Cosmos DB][consistency-levels].

Se hello configurato i criteri di indicizzazione nella raccolta di hello non supportano la query specificata hello, server di database di Azure Cosmos hello restituisce 400 "richiesta non valida". Questo codice viene restituito per le query di intervallo per ricerche hash (uguaglianza) e per i percorsi esplicitamente esclusi dall'indicizzazione. Hello `x-ms-documentdb-query-enable-scan` intestazione può essere specificato tooallow hello query tooperform una scansione quando un indice non è disponibile.

È possibile ottenere le metriche dettagliate sull'esecuzione di query mediante l'impostazione `x-ms-documentdb-populatequerymetrics` intestazione troppo`True`. Per altre informazioni, vedere [metriche di query SQL per l'API Azure Cosmos DB DocumentDB](documentdb-sql-query-metrics.md).

### <a id="DotNetSdk"></a>C# (.NET) SDK
Hello .NET SDK supporta LINQ sia SQL l'esecuzione di query. Hello riportato di seguito come query di filtro semplice hello tooperform introdotta in precedenza in questo documento.

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


In questo esempio vengono confrontate due proprietà per l'uguaglianza all'interno di ciascun documento, usando le proiezioni anonime. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Hello successiva illustra i join, espliciti tramite LINQ SelectMany.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



client .NET Hello scorre automaticamente da tutte le pagine hello dei risultati della query in blocchi di foreach hello come illustrato in precedenza. Opzioni introdotte in hello sezione API REST sono disponibili anche in query di Hello hello .NET SDK utilizzando hello `FeedOptions` e `FeedResponse` classi hello CreateDocumentQuery metodo. numero di Hello di pagine può essere controllata utilizzando hello `MaxItemCount` impostazione. 

È possibile controllare in modo esplicito il paging creando `IDocumentQueryable` utilizzando hello `IQueryable` oggetto, quindi leggendo il` ResponseContinuationToken` valori e passarli nuovamente come `RequestContinuationToken` in `FeedOptions`. `EnableScanInQuery`può essere set tooenable analisi quando query hello non possono essere supportati da criteri di indicizzazione hello configurato. Per le raccolte partizionate, è possibile utilizzare `PartitionKey` query di hello toorun su una singola partizione (sebbene DB Cosmos può estrarre automaticamente questo dal testo della query hello), e `EnableCrossPartitionQuery` query toorun che potrebbe essere necessario toobe eseguite in più partizioni. 

Fare riferimento troppo[esempi di Azure Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net) per altri esempi che includono query. 

### <a id="JavaScriptServerSideApi"></a>API lato server JavaScript
COSMOS DB fornisce un modello di programmazione per l'esecuzione di logica dell'applicazione basata su JavaScript direttamente nelle raccolte di hello utilizzando stored procedure e trigger. logica di JavaScript Hello registrata a livello di raccolta può quindi eseguire operazioni di database su hello operazioni sui documenti hello hello fornito insieme. Viene quindi eseguito il wrapping di queste operazioni nelle transazioni ACID Ambient.

Hello esempio seguente viene illustrato come una query da toouse hello queryDocuments in toomake hello API server JavaScript all'interno di stored procedure e trigger.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>Riferimenti
1. [Introduzione tooAzure Cosmos DB][introduction]
2. [Specifica SQL di Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Esempi relativi a Azure Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net)
4. [Livelli di coerenza di Azure Cosmos DB][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. Specifiche Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. Tecniche di valutazione delle query per database di grandi dimensioni [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994
11. Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.
12. Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: un linguaggio non così estraneo per l'elaborazione dati, SIGMOD 2008.
13. G. Graefe. framework di catena Hello per l'ottimizzazione delle query. IEEE Data Eng. Bull., 18(3): 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md