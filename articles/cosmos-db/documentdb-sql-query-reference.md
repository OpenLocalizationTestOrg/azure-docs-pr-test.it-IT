---
titolo: aaa "API di Azure Cosmos DB DocumentDB: la sintassi SQL | Descrizione di Microsoft Docs": fare riferimento alla documentazione per il linguaggio di query SQL di Azure Cosmos DB DocumentDB API hello.
servizi: cosmos db autore: manager mimig1: jhubbard editor: mimig documentationcenter: '

ms. AssetID: ms. Service: cosmos db Workload: ms. tgt_pltfrm servizi dati: ms. DevLang na: ms. topic na: fare riferimento a MS. date: 13/06/2017 Author: mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>API di DocumentDB per Azure Cosmos DB: riferimento per la sintassi SQL

Hello Azure Cosmos DB l'API DocumentDB supporta documenti l'esecuzione di query mediante una familiare SQL (Structured Query Language) grammatica simile su documenti JSON gerarchici senza richiedere uno schema esplicito o la creazione di indici secondari. In questo argomento fornisce la documentazione di riferimento per il linguaggio di query SQL API DocumentDB hello.

Per una procedura dettagliata di hello linguaggio di query SQL API DocumentDB, vedere [query SQL per l'API Azure Cosmos DB DocumentDB](documentdb-sql-query.md).  
  
Anche Microsoft invita è hello toovisit [Query Playground](http://www.documentdb.com/sql/demo) in cui è possibile provare Azure Cosmos DB ed eseguire query SQL nel set di dati.  
  
## <a name="select-query"></a>Query SELECT  
Recupera documenti JSON dal database di hello. Supporta la valutazione delle espressioni, le proiezioni, il filtraggio e i join.  convenzioni di Hello usate per descrivere le istruzioni SELECT hello vengano inserite nella sezione convenzioni della sintassi hello.  
  
**Sintassi**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **Osservazioni**  
  
 Per i dettagli su ogni clausola, vedere le sezioni seguenti:  
  
-   [Clausola SELECT](#bk_select_query)  
  
-   [Clausola FROM](#bk_from_clause)  
  
-   [Clausola WHERE](#bk_where_clause)  
  
-   [Clausola ORDER BY](#bk_orderby_clause)  
  
clausole Hello nell'istruzione SELECT hello devono essere ordinate come illustrato in precedenza. Una delle clausole facoltative hello può essere omessa. Tuttavia, quando si utilizzano clausole facoltative, è necessario specificarle nell'ordine corretto hello.  
  
**Ordine di elaborazione logica dell'istruzione SELECT hello**  
  
l'ordine in cui vengono elaborate clausole Hello è:  

1.  [Clausola FROM](#bk_from_clause)  
2.  [Clausola WHERE](#bk_where_clause)  
3.  [Clausola ORDER BY](#bk_orderby_clause)  
4.  [Clausola SELECT](#bk_select_query)  

Si noti che questo è diverso dall'ordine hello in cui appaiono nella sintassi hello. ordinamento Hello è tale che tutti i nuovi simboli introdotti da una clausola elaborata sono visibili e possono essere utilizzati nelle clausole elaborate successivamente. Ad esempio, gli alias dichiarati in una clausola FROM sono accessibili nelle clausole WHERE e SELECT.  

**Spazi vuoti e commenti**  

Tutti i caratteri di spazio vuoto che non fanno parte di una stringa tra virgolette o identificatore tra virgolette non fanno parte della grammatica del linguaggio hello e vengono ignorati durante l'analisi.  

il linguaggio di query di Hello supporta commenti in stile T-SQL come  

-   istruzione SQL `-- comment text [newline]`  

Mentre i commenti e gli spazi vuoti non presentano alcun significato nella grammatica hello, devono essere utilizzati tooseparate token. Ad esempio: `-1e5` è un token numero singolo, mentre `: – 1 e5` è un token meno seguito dal numero 1 e dall'identificatore e5.  

##  <a name="bk_select_query"></a> Clausola SELECT  
clausole Hello nell'istruzione SELECT hello devono essere ordinate come illustrato in precedenza. Una delle clausole facoltative hello può essere omessa. Tuttavia, quando si utilizzano clausole facoltative, è necessario specificarle nell'ordine corretto hello.  

**Sintassi**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **Argomenti**  
  
 `<select_specification>`  
  
 Imposta proprietà o il valore toobe selezionati per il risultato di hello.  
  
 `'*'`  
  
Specifica che il valore di hello deve essere recuperato senza apportare alcuna modifica. In particolare, se il valore di hello elaborato è un oggetto, tutte le proprietà verranno recuperate.  
  
 `<object_property_list>`  
  
Specifica l'elenco di hello di toobe proprietà recuperata. Ogni valore restituito sarà un oggetto con proprietà hello specificate.  
  
`VALUE`  
  
Specifica che deve essere recuperato il valore JSON hello anziché l'intero oggetto JSON di hello. Questo, a differenza `<property_list>` non va a capo valore hello proiettato in un oggetto.  
  
`<scalar_expression>`  
  
Espressione che rappresenta hello valore toobe calcolato. Vedere la sezione [Espressioni scalari](#bk_scalar_expressions) per informazioni dettagliate.  
  
**Osservazioni**  
  
Hello `SELECT *` sintassi è valida solo se clausola FROM ha dichiarato esattamente un alias. `SELECT *` offre una proiezione dell'identità, che può essere utile se non è necessaria alcuna proiezione. SELECT * è valida solo se viene specificata la clausola FROM e se viene introdotta solo una singola origine di input.  
  
Si noti che `SELECT <select_list>` e `SELECT *` sono "zucchero sintattico" e può essere espressi in alternativa usando semplici istruzioni SELECT, come illustrato di seguito.  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     Equivale a:  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     Equivale a:  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**Vedere anche**  
  
[Espressioni scalari](#bk_scalar_expressions)  
[Clausola SELECT](#bk_select_query)  
  
##  <a name="bk_from_clause"></a> Clausola FROM  
Specifica l'origine hello o origini unite in join. clausola FROM Hello è facoltativo. Se non viene specificata, le altre clausole verranno comunque eseguite come se la clausola FROM specificasse un singolo documento.  
  
**Sintassi**  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
**Argomenti**  
  
`<from_source>`  
  
Specifica un'origine dati, con o senza un alias. Se non viene specificato alcun alias, tale elemento verrà inferito da hello `<collection_expression>` utilizzando le seguenti regole:  
  
-   Se l'espressione hello è collection_name, come alias verrà usato collection_name.  
  
-   Se l'espressione hello è `<collection_expression>`, verrà usato property_name, property_name come alias. Se l'espressione hello è collection_name, come alias verrà usato collection_name.  
  
AS `input_alias`  
  
Specifica che hello `input_alias` è un set di valori restituiti da hello espressione di raccolta sottostante.  
 
`input_alias` IN  
  
Specifica che hello `input_alias` deve rappresentare il set di hello di valori ottenuti eseguendo l'iterazione su tutti gli elementi di matrice di ogni matrice restituita dall'espressione di raccolta sottostante hello. Tutti i valori restituiti dall'espressione di raccolta sottostante che non sono matrici vengono ignorati.  
  
`<collection_expression>`  
  
Specifica hello raccolta espressione toobe documenti hello tooretrieve.  
  
`ROOT`  
  
Specifica che il documento deve essere recuperato da predefinito hello, raccolta attualmente connesso.  
  
`collection_name`  
  
Specifica che il documento deve essere recuperato dalla raccolta hello fornito. nome Hello dell'insieme di hello deve corrispondere il nome di hello dell'insieme di hello attualmente connessi.  
  
`input_alias`  
  
Specifica che il documento deve essere recuperato da hello altra origine definita dall'alias di hello fornito.  
  
`<collection_expression> '.' property_`  
  
Specifica che il documento deve essere recuperato accedendo hello `property_name` elemento di matrice array_index o di proprietà per tutti i documenti recuperati dall'espressione di raccolta specificata.  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
Specifica che il documento deve essere recuperato accedendo hello `property_name` elemento di matrice array_index o di proprietà per tutti i documenti recuperati dall'espressione di raccolta specificata.  
  
**Osservazioni**  
  
Tutti gli alias fornito o dedotto in hello `<from_source>(`s) deve essere univoco. Sintassi di Hello `<collection_expression>.`property_name è hello identico `<collection_expression>' ['"property_name"']'`. Tuttavia, quest ' ultima hello utilizzabile se un nome di proprietà contiene un carattere non identificatore.  
  
**Proprietà mancanti, elementi di matrice mancanti, gestione dei valori non definita**  
  
Se un'espressione di raccolta accede alle proprietà o agli elementi di matrice e il valore non esiste, tale valore verrà ignorato e non elaborato ulteriormente.  
  
**Definizione dell'ambito per il contesto dell'espressione di raccolta**  
  
Un'espressione di raccolta può avere come ambito una raccolta o un documento:  
  
-   È un'espressione con ambito raccolta, se hello origine sottostante dell'espressione di raccolta hello è ROOT o `collection_name`. Un'espressione di questo tipo rappresenta un set di documenti recuperati direttamente dalla raccolta hello e non è dipendente dall'elaborazione hello di altre espressioni di raccolta.  
  
-   Un'espressione è un ambito documento, se hello origine sottostante dell'espressione di raccolta hello è `input_alias` introdotta in precedenza nella query hello. Un'espressione di questo tipo rappresenta un set di documenti ottenuti dalla valutazione di espressione di raccolta hello nell'ambito di hello di ogni documento appartenente toohello set associato hello alias insieme.  set di Hello risultante sarà un'unione di set ottenuti valutando l'espressione di raccolta hello per ognuno dei documenti hello in hello sottostante set.  
  
**Join**  
  
Nella versione corrente di hello, Azure Cosmos DB supporta gli inner join. Altre funzionalità di join saranno presto disponibili.

Set di risultati di inner join in un prodotto incrociato completo di hello che fanno parte di join hello. il risultato di Hello di un join a N vie è un set di tuple a N elementi, in cui ogni valore di tupla hello associata hello alias set che fanno parte di join hello che è possibile accedere facendo riferimento a tale alias in altre clausole.  
  
valutazione Hello di join hello dipende dall'ambito del contesto hello di hello che fanno parte di set di:  
  
-  Un join tra il set di raccolta A e il set di raccolta con ambito B genera un prodotto incrociato di tutti gli elementi presenti nei set A e B.
  
-   Un join tra il set A e il set con ambito documento B genera un'unione di tutti i set ottenuti dalla valutazione di un set con ambito documento B per ogni documento del set A.  
  
 Nella versione corrente di hello, da query processor di hello è supportato un massimo di un'espressione con ambito raccolta.  
  
**Esempi di join:**  
  
Diamo un'occhiata hello seguente clausola FROM:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 Consentire a ogni origine di definire `input_alias1, input_alias2, …, input_aliasN`. Questa clausola FROM restituisce un set di N tuple (tuple con N valori). Ogni tupla ha valori prodotti dall'iterazione di tutti gli alias della raccolta sui rispettivi set.  
  
*Esempio di JOIN 1, con 2 origini:*  
  
- Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.  
  
- Consentire a `<from_source2>` di avere un ambito documento che fa riferimento a input_alias1 e di rappresentare i set:  
  
    {1, 2} per `input_alias1 = A,`  
  
    {3} per `input_alias1 = B,`  
  
    {4, 5} per `input_alias1 = C,`  
  
- Hello dalla clausola `<from_source1> JOIN <from_source2>` comporterà hello tuple seguente:  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*Esempio di JOIN 2, con 3 origini:*  
  
- Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.  
  
- Consentire a `<from_source2>` di avere un ambito documento che fa riferimento `input_alias1` e di rappresentare i set:  
  
    {1, 2} per `input_alias1 = A,`  
  
    {3} per `input_alias1 = B,`  
  
    {4, 5} per `input_alias1 = C,`  
  
- Consentire a `<from_source3>` di avere un ambito documento che fa riferimento `input_alias2` e di rappresentare i set:  
  
    {100, 200} per `input_alias2 = 1,`  
  
    {300} per `input_alias2 = 3,`  
  
- Hello dalla clausola `<from_source1> JOIN <from_source2> JOIN <from_source3>` comporterà hello tuple seguente:  
  
    (input_alias1, input_alias2, input_alias3):  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> Mancanza di tuple per altri valori di `input_alias1`, `input_alias2`, per cui hello `<from_source3>` non ha restituito alcun valore.  
  
*Esempio di JOIN 3, con 3 origini:*  
  
- Consentire a <from_source1> di avere un ambito raccolta e di rappresentare il set {A, B, C}.  
  
- Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.  
  
- Consentire a <from_source2> di avere un ambito documento che fa riferimento a input_alias1 e di rappresentare i set:  
  
    {1, 2} per `input_alias1 = A,`  
  
    {3} per `input_alias1 = B,`  
  
    {4, 5} per `input_alias1 = C,`  
  
- Consentire `<from_source3>` ambito troppo`input_alias1` e rappresentare insiemi:  
  
    {100, 200} per `input_alias2 = A,`  
  
    {300} per `input_alias2 = C,`  
  
- Hello dalla clausola `<from_source1> JOIN <from_source2> JOIN <from_source3>` comporterà hello tuple seguente:  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)  
  
> [!NOTE]
> Questo ha comportato il prodotto incrociato tra `<from_source2>` e `<from_source3>` perché entrambi sono con ambito toohello stesso `<from_source1>`.  Sono state create 4 (2x2) tuple con valore A, 0 tuple con valore B (1 x 0) e 2 (2x1) tuple con valore C.  
  
**Vedere anche**  
  
 [Clausola SELECT](#bk_select_query)  
  
##  <a name="bk_where_clause"></a> Clausola WHERE  
 Specifica la condizione di ricerca hello per hello documenti restituiti dalla query hello.  
  
 **Sintassi**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **Argomenti**  
  
-   `<filter_condition>`  
  
     Specifica hello condizione toobe soddisfatti hello documenti toobe restituito.  
  
-   `<scalar_expression>`  
  
     Espressione che rappresenta hello valore toobe calcolato. Vedere hello [espressioni scalari](#bk_scalar_expressions) sezione per informazioni dettagliate.  
  
 **Osservazioni**  
  
 Affinché hello toobe documento ha restituito un'espressione specificata come condizione di filtro deve restituire tootrue. Solo un valore booleano true soddisferà la condizione di hello, qualsiasi altro valore: undefined, null, false, numero, matrice o oggetto non soddisferà la condizione hello.  
  
##  <a name="bk_orderby_clause"></a> Clausola ORDER BY  
 Specifica l'ordinamento dei risultati restituiti dalla query hello hello.  
  
 **Sintassi**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **Argomenti**  
  
-   `<sort_specification>`  
  
     Specifica una proprietà o l'espressione in cui set di risultati di query hello toosort. Una colonna di ordinamento può essere specificata come alias di nome o di colonna.  
  
     È possibile specificare più colonne di ordinamento. I nomi delle colonne devono essere univoci. sequenza di Hello di colonne di ordinamento hello nella clausola ORDER BY hello definisce organizzazione hello del set di risultati ordinato hello. Vale a dire hello set di risultati vengono ordinati prima proprietà hello e quindi tale elenco ordinato viene ordinato in base hello secondo e così via.  
  
     i nomi di colonna Hello a cui fa riferimento nella clausola ORDER BY hello devono corrispondere tooeither una colonna in hello selezionare elenco o tooa colonna definita in una tabella specificata nella clausola FROM hello senza ambiguità.  
  
-   `<sort_expression>`  
  
     Specifica una singola proprietà o un'espressione per il set di risultati query toosort hello.  
  
-   `<scalar_expression>`  
  
     Vedere hello [espressioni scalari](#bk_scalar_expressions) sezione per informazioni dettagliate.  
  
-   `ASC | DESC`  
  
     Specifica che i valori nella colonna specificata hello hello devono essere ordinati in ordine crescente o decrescente. ASC Ordina dal più basso valore toohighest valore hello. DESC Ordina dal più alto valore toolowest valore. ASC è l'ordinamento predefinito hello. Valori null vengono considerati come possibili valori hello più bassi.  
  
 **Osservazioni**  
  
 Durante la grammatica di query hello supporta più ordine dalle proprietà, hello Azure Cosmos DB query runtime supporta l'ordinamento solo in una singola proprietà e solo con i nomi di proprietà, ad esempio, non in base a proprietà calcolate. L'ordinamento richiede inoltre che hello criteri di indicizzazione include un indice di intervallo per la proprietà hello e hello specificato tipo, con la massima precisione hello. Toohello l'indicizzazione di documentazione per i criteri per ulteriori informazioni, vedere.  
  
##  <a name="bk_scalar_expressions"></a> Espressioni scalari  
 Un'espressione scalare è una combinazione di simboli e operatori che possono essere valutati tooobtain un singolo valore. Le espressioni semplici possono essere costanti, riferimenti a proprietà, riferimenti a elementi di matrice, riferimenti ad alias o chiamate di funzioni. Le espressioni semplici possono essere combinate in espressioni complesse usando gli operatori.  
  
 Per informazioni dettagliate sui valori che possono essere contenuti nelle espressioni scalari, vedere la sezione relativa alle [costanti](#bk_constants).  
  
 **Sintassi**  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 **Argomenti**  
  
-   `<constant>`  
  
     Rappresenta un valore costante. Per informazioni dettagliate, vedere la sezione [Costanti](#bk_constants).  
  
-   `input_alias`  
  
     Rappresenta un valore definito da hello `input_alias` introdotta in hello `FROM` clausola.  
    Questo valore è sicuramente toonot essere **definito** –**definito** i valori nell'input hello verranno ignorati.  
  
-   `<scalar_expression>.property_name`  
  
     Rappresenta un valore della proprietà hello di un oggetto. Se la proprietà hello non esiste o proprietà fa riferimento a un valore che non è un oggetto, quindi hello espressione troppo**definito** valore.  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     Rappresenta un valore della proprietà hello con nome `property_name` o elemento di matrice con indice `array_index` di un'oggetto/la matrice. Se l'indice di matrice proprietà hello non esiste o l'indice di matrice proprietà hello fa riferimento a un valore che non è una matrice di oggetti o, quindi hello espressione valore tooundefined.  
  
-   `unary_operator <scalar_expression>`  
  
     Rappresenta un operatore applicato tooa singolo valore. Per informazioni dettagliate, vedere la sezione [Operatori](#bk_operators).  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     Rappresenta un operatore applicato tootwo valori. Per informazioni dettagliate, vedere la sezione [Operatori](#bk_operators).  
  
-   `<scalar_function_expression>`  
  
     Rappresenta un valore definito da un risultato di una chiamata di funzione.  
  
-   `udf_scalar_function`  
  
     Nome dell'utente hello funzione scalare definita.  
  
-   `builtin_scalar_function`  
  
     Nome della funzione scalare predefinita hello.  
  
-   `<create_object_expression>`  
  
     Rappresenta un valore ottenuto creando un nuovo oggetto con proprietà specificate e i relativi valori.  
  
-   `<create_array_expression>`  
  
     Rappresenta un valore ottenuto creando una nuova matrice con valori specificati come elementi  
  
-   `parameter_name`  
  
     Rappresenta un valore del nome di parametro specificato hello. I nomi di parametro deve essere un singolo @ come primo carattere hello.  
  
 **Osservazioni**  
  
 Quando si chiama una funzione scalare predefinita o definita dall'utente è necessario definire tutti gli argomenti. Se uno degli argomenti hello è definito, non verrà chiamata la funzione hello e hello risultato sarà indefinito.  
  
 Quando si crea un oggetto, verrà saltata e non presenti nell'oggetto creato hello qualsiasi proprietà che è assegnato il valore undefined.  
  
 Quando la creazione di una matrice, il valore di qualsiasi elemento che viene assegnata **definito** valore verrà ignorato e non inclusi nell'oggetto hello creato. In questo modo tootake elemento hello successivamente definita al suo posto in modo tale matrice hello creato verrà non vengano ignorati indici.  
  
##  <a name="bk_operators"></a> Operatori  
 Questa sezione descrive gli operatori di hello è supportato. Ogni operatore può essere assegnato tooexactly una categoria.  
  
 Vedere la tabella delle **categorie di operatori** riportata di seguito per informazioni dettagliate sulla gestione dei valori **non definiti**, sui requisiti di tipi per valori di input e sulla gestione dei valori con tipi non corrispondenti.  
  
 **Categorie di operatori:**  
  
|**Categoria**|**Dettagli**|  
|-|-|  
|**aritmetico**|L'operatore prevede uno o più input toobe numeri. Anche l'output è un numero. Se uno degli input hello è **definito** o è di tipo diverso dal risultato numero quindi hello **definito**.|  
|**bit per bit**|L'operatore prevede uno o più input numeri interi con segno a 32 bit toobe. Anche l'output è un numero intero con segno a 32 bit.<br /><br /> Gli eventuali valori non interi vengono arrotondati. I valori positivi verranno arrotondati per difetto, i valori negativi per eccesso.<br /><br /> Qualsiasi valore è compreso nell'intervallo integer a 32 bit hello verrà convertiti prendendo ultimi 32 bit della relativi due notazione di complemento.<br /><br /> Se uno degli input hello è **definito** o un tipo diverso da un numero, il risultato di hello è **definito**.<br /><br /> **Nota:** hello sopra il comportamento è compatibile con il comportamento di un operatore bit per bit di JavaScript.|  
|**logico**|L'operatore prevede uno o più input toobe valori booleani. Anche l'output è un valore booleano.<br />Se uno degli input hello è **definito** o un tipo diverso da un valore booleano, verrà utilizzato come risultato di hello **definito**.|  
|**confronto**|L'operatore prevede uno o più input toohave hello stesso tipo e non essere indefinito. L'output è un valore booleano.<br /><br /> Se uno degli input hello è **definito** o hello input hanno tipi diversi, quindi il risultato di hello è **definito**.<br /><br /> Vedere la tabella dell'**ordinamento dei valori per il confronto** per informazioni dettagliate sull'ordinamento dei valori.|  
|**string**|L'operatore prevede uno o più input toobe stringhe. Anche l'output è una stringa.<br />Se uno degli input hello è **definito** o è di tipo diverso dal risultato di stringa quindi hello **definito**.|  
  
 **Operatori unari:**  
  
|**Nome**|**Operatore**|**Dettagli**|  
|-|-|-|  
|**aritmetico**|+<br /><br /> -|Restituisce il valore numerico hello.<br /><br /> Negazione bit per bit. Restituisce il valore numerico negato.|  
|**bit per bit**|~|Complemento a uno. Restituisce un complemento di un valore numerico.|  
|**Logico**|**NOT**|Negazione. Restituisce un valore booleano negato.|  
  
 **Operatori binari:**  
  
|**Nome**|**Operatore**|**Dettagli**|  
|-|-|-|  
|**aritmetico**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|Addizione.<br /><br /> Sottrazione.<br /><br /> Moltiplicazione.<br /><br /> Divisione.<br /><br /> Modulazione.|  
|**bit per bit**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|OR bit per bit.<br /><br /> AND bit per bit.<br /><br /> XOR bit per bit.<br /><br /> Spostamento a sinistra.<br /><br /> Spostamento a destra.<br /><br /> Spostamento a destra riempimento zero.|  
|**logico**|**AND**<br /><br /> **OR**|Congiunzione logica. Restituisce **true** se entrambi gli argomenti sono **true**, altrimenti restituisce **false**.<br /><br /> Congiunzione logica. Restituisce **true** se entrambi gli argomenti sono **true**, altrimenti restituisce **false**.|  
|**confronto**|**=**<br /><br /> **!=, &lt;&gt;**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|Uguale a. Restituisce **true** se gli argomenti sono uguali, altrimenti restituisce **false**.<br /><br /> Diverso da. Restituisce **true** se gli argomenti non sono uguali, altrimenti restituisce **false**.<br /><br /> Maggiore di. Restituisce **true** se il primo argomento è maggiore del secondo hello, restituire **false** in caso contrario.<br /><br /> Maggiore o uguale a. Restituisce **true** se il primo argomento è maggiore o uguale a toohello secondo, restituire **false** in caso contrario.<br /><br /> Minore di. Restituisce **true** se il primo argomento è minore della seconda hello, restituire **false** in caso contrario.<br /><br /> Minore o uguale a. Restituisce **true** se il primo argomento è minore o uguale toohello secondo uno, restituito **false** in caso contrario.<br /><br /> Unione. Restituisce hello secondo argomento se hello primo argomento è un **definito** valore.|  
|**String**|**&amp;#124;&amp;#124;**|Concatenazione. Restituisce una concatenazione di entrambi gli argomenti.|  
  
 **Operatori ternari:**  
  
|Operatore ternario|?|Restituisce hello secondo argomento se il primo argomento hello valuta troppo**true**; in caso contrario restituito terzo argomento hello.|  
|-|-|-|  
  
 **Ordinamento dei valori per il confronto**  
  
|**Tipo**|**Ordine dei valori**|  
|-|-|  
|**Undefined**|Non confrontabile.|  
|**Null**|Singolo valore: **null**|  
|**Number**|Numero reale naturale.<br /><br /> Il valore infinito negativo è minore di qualsiasi altro valore numerico.<br /><br /> Il valore infinito positivo è maggiore di qualsiasi altro valore numerico. il valore **NaN** non è confrontabile. Il confronto con **NaN** restituisce un valore **non definito**.|  
|**String**|Ordine lessicografico.|  
|**Array**|Nessun ordinamento, ma equo.|  
|**Object**|Nessun ordinamento, ma equo.|  
  
 **Osservazioni**  
  
 In Azure Cosmos DB tipi hello di valori sono spesso sconosciuti finché vengono effettivamente recuperati dal database hello. In ordine toosupport un'esecuzione efficiente delle query, la maggior parte degli operatori hello hanno requisiti di tipo strict. Inoltre, gli operatori di per sé non eseguono conversioni implicite.  
  
 Ciò significa che una query come: seleziona * FROM ROOT r WHERE Age = 21 restituisce solo documenti con proprietà Age uguale toohello number 21. Documenti con proprietà Age uguale toohello stringa "21" o la stringa hello "0021" non corrispondono, come espressione hello "21" = 21 restituisce tooundefined. In questo modo per migliorare l'utilizzo di indici, in quanto ricerca hello di un valore specifico (ovvero il numero 21) è più veloce rispetto alla ricerca di un numero indefinito di possibili corrispondenze (numero 21 o le stringhe "21", "021", "21.0"...). Ciò si differenzia dal modo in cui JavaScript valuta gli operatori per valori di tipi diversi.  
  
 **Confronto e uguaglianza di oggetti e matrici**  
  
 Il confronto dei valori di oggetto o matrice con gli operatori di intervallo (>, >=, <, <=) produce un risultato indefinito poiché non è definito un ordine per i valori di oggetto o matrice. Tuttavia l'uso degli operatori di uguaglianza/disuguaglianza (=,! =, <>) è supportato e i valori vengono confrontati strutturalmente.  
  
 Le matrici sono uguali se entrambe le matrici hanno stesso numero di elementi e sono uguali anche gli elementi nelle posizioni corrispondenti. Se il confronto tra qualsiasi coppia di elementi risultante nel risultato hello definito, di confronto di matrice è definito.  
  
 Gli oggetti sono uguali se entrambi gli oggetti hanno le stesse proprietà definite e se anche i valori delle proprietà corrispondenti sono uguali. Se il confronto tra qualsiasi coppia di valori di proprietà comporta risultati hello definito, di confronto di oggetti è definito.  
  
##  <a name="bk_constants"></a> Costanti  
 Una costante, nota anche come valore letterale o scalare, è un simbolo che rappresenta un valore di dati specifico. formato di Hello di una costante dipende dal tipo di dati hello del valore di hello che rappresenta.  
  
 **Tipi di dati scalari supportati:**  
  
|**Tipo**|**Ordine dei valori**|  
|-|-|  
|**Undefined**|Singolo valore: **non definito**|  
|**Null**|Singolo valore: **null**|  
|**Boolean**|Valori: **false**, **true**.|  
|**Number**|Un numero a virgola mobile e precisione doppia, standard IEEE 754.|  
|**String**|Una sequenza di zero o più caratteri Unicode. Le stringhe devono essere racchiuse tra virgolette singole o doppie.|  
|**Array**|Una sequenza di zero o più elementi. Ogni elemento può essere un valore di qualsiasi tipo di dati scalare, tranne Undefined.|  
|**Object**|Un set non ordinato di zero o più coppie nome/valore. Il nome è una stringa Unicode, il valore può essere di qualsiasi tipo di dati scalare, tranne **Undefined**.|  
  
 **Sintassi**  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 **Argomenti**  
  
1.  `<undefined_constant>; undefined`  
  
     Rappresenta un valore non definito di tipo Undefined.  
  
2.  `<null_constant>; null`  
  
     Rappresenta un valore **null** di tipo **Null**.  
  
3.  `<boolean_constant>`  
  
     Rappresenta una costante di tipo Boolean.  
  
4.  `false`  
  
     Rappresenta un valore **false** di tipo booleano.  
  
5.  `true`  
  
     Rappresenta un valore **true** di tipo booleano.  
  
6.  `<number_constant>`  
  
     Rappresenta una costante.  
  
7.  `decimal_literal`  
  
     I valori letterali decimali sono numeri rappresentati usando la notazione decimale o la notazione scientifica.  
  
8.  `hexadecimal_literal`  
  
     I valori letterali esadecimali sono numeri rappresentati usando il prefisso "0x" seguito da una o più cifre esadecimali.  
  
9. `<string_constant>`  
  
     Rappresenta una costante di tipo String.  
  
10. `string _literal`  
  
     I valori letterali stringa sono stringhe Unicode rappresentate da una sequenza di zero o più caratteri Unicode o sequenze di escape. I valori letterali stringa sono racchiusi tra virgolette singole (apostrofo: ') o virgolette doppie (virgolette inglesi: ").  
  
 Sono consentite le sequenze di escape seguenti:  
  
|**Sequenza di escape**|**Descrizione**|**Carattere Unicode**|  
|-|-|-|  
|\\'|apostrofo (')|U + 0027|  
|\\"|virgolette doppie (")|U + 0022|  
|\\\|barra rovesciata (\\)|U + 005C|  
|\\/|barra (/)|U + 002F|  
|\b|BACKSPACE|U + 0008|  
|\f|avanzamento carta|U + 000C|  
|\n|avanzamento riga|U + 000A|  
|\r|ritorno a capo|U + 000D|  
|\t|TAB|U + 0009|  
|\uXXXX|Carattere Unicode definito da 4 cifre esadecimali.|U + XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a> Linee guida sulle prestazioni delle query  
 Affinché un toobe query eseguita in modo efficiente per una raccolta di grandi dimensioni, è opportuno usare filtri gestibili tramite uno o più indici.  
  
 Hello seguendo i filtri verrà considerato per la ricerca nell'indice:  
  
-   Usare l'operatore di uguaglianza (=) con un'espressione percorso documenti e una costante.  
  
-   Usare gli operatori di intervallo (<, \<=, >, >=) con un'espressione percorso documenti e costanti numeriche.  
  
-   Espressione di percorso del documento è l'acronimo di un'espressione che identifica un percorso di costante nei documenti di hello dalla raccolta di database a cui fa riferimento hello.  
  
 **Espressione percorso documenti**  
  
 Le espressioni percorso documenti sono espressioni usate in un percorso di funzioni di valutazione dell'indicizzatore proprietà o matrice per un documento proveniente da documenti di una raccolta di database. Questo può essere utilizzato tooidentify hello percorso di valori a cui fa riferimento in un filtro direttamente all'interno dei documenti hello nella raccolta di database hello.  
  
 Per un'espressione toobe considerata un'espressione di percorso del documento, è necessario:  
  
1.  Riferimento hello raccolta radice direttamente.  
  
2.  Faccia riferimento all'indicizzatore di proprietà o matrici costanti di un'espressione percorso documenti  
  
3.  Faccia riferimento a un alias che rappresenta un'espressione percorso documenti.  
  
     **Convenzioni della sintassi**  
  
     Hello nella tabella seguente descrive la sintassi di toodescribe hello convenzioni utilizzate in riferimenti al linguaggio di Query API DocumentDB hello.  
  
    |**Convenzione**|**Usata per**|  
    |-|-|    
    |LETTERE MAIUSCOLE|Parole chiave che non fanno distinzione tra maiuscole e minuscole.|  
    |lettere minuscole|Parole chiave che fanno distinzione tra maiuscole e minuscole.|  
    |\<non terminale>|Non terminale, definito separatamente.|  
    |\<non terminale> ::=|Definizione della sintassi di non terminale hello.|  
    |altro_terminale|Terminale (token), descritto dettagliatamente con parole.|  
    |identificatore|Identificatore. Consente solo i seguenti caratteri: a-z A-Z 0-9 _Il primo carattere non può essere una cifra.|  
    |"stringa"|Stringa tra virgolette. Consente qualsiasi stringa valida. Vedere la descrizione di string_literal.|  
    |'simbolo'|Simbolo letterale che fa parte della sintassi hello.|  
    |&#124; (barra verticale)|Alternative per gli elementi di sintassi. È possibile utilizzare solo uno degli elementi di hello specificati.|  
    |[ ] /(parentesi quadre)|Le parentesi quadre racchiudono uno o più elementi facoltativi.|  
    |[ ,...n ]|Indica hello precedente elemento può essere ripetuto n volte. Hello occorrenze sono separate da virgole.|  
    |[ ...n ]|Indica hello precedente elemento può essere ripetuto n volte. Hello occorrenze sono separate da spazi.|  
  
##  <a name="bk_built_in_functions"></a> Funzioni predefinite  
 In Azure Cosmos DB sono disponibili molte funzioni SQL predefinite. categorie di Hello delle funzioni predefinite sono elencate di seguito.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Funzioni matematiche](#bk_mathematical_functions)|Hello funzioni matematiche eseguono un calcolo basato in genere su valori di input forniti come argomenti e restituiscono un valore numerico.|  
|[Funzioni di controllo del tipo](#bk_type_checking_functions)|funzioni di controllo di tipo Hello consentono di tipo hello toocheck di un'espressione all'interno di query SQL.|  
|[Funzioni stringa](#bk_string_functions)|funzioni stringa Hello eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, numerico o booleano.|  
|[Funzioni di matrice](#bk_array_functions)|funzioni di matrice Hello eseguono un'operazione su un valore di input di matrice e restituito numerico, un valore booleano o di matrice.|  
|[Funzioni spaziali](#bk_spatial_functions)|le funzioni spaziali Hello eseguono un'operazione su un valore di oggetto spaziale input e restituiscono un valore numerico o booleano.|  
  
###  <a name="bk_mathematical_functions"></a> Funzioni matematiche  
 Hello ognuna delle funzioni seguenti esegue un calcolo basato in genere su valori di input forniti come argomenti e restituiscono un valore numerico.  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[ACOS](#bk_acos)|[ASIN](#bk_asin)|  
|[ATAN](#bk_atan)|[ATN2](#bk_atn2)|[CEILING](#bk_ceiling)|  
|[COS](#bk_cos)|[COT](#bk_cot)|[DEGREES](#bk_degrees)|  
|[EXP](#bk_exp)|[FLOOR](#bk_floor)|[LOG](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[POWER](#bk_power)|  
|[RADIANS](#bk_radians)|[ROUND](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[SQUARE](#bk_square)|[SIGN](#bk_sign)|  
|[TAN](#bk_tan)|[TRUNC](#bk_trunc)||  
  
####  <a name="bk_abs"></a> ABS  
 Restituisce hello assoluto (positivo) il valore di hello specificato espressione numerica.  
  
 **Sintassi**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello riportato di seguito risultati hello dell'utilizzo della funzione hello ABS su tre numeri diversi.  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a> ACOS  
 Angolo di hello restituisce, in radianti, il cui coseno è hello espressione numerica specificata; denominato anche arcocoseno.  
  
 **Sintassi**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente restituisce hello Arcocoseno di -1.  
  
```  
SELECT ACOS(-1)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a> ASIN  
 Angolo di hello restituisce, in radianti, il cui seno è hello specificato espressione numerica. Detta anche arcoseno.  
  
 **Sintassi**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente restituisce hello ARCOSENO di -1.  
  
```  
SELECT ASIN(-1)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a> ATAN  
 Angolo di hello restituisce, in radianti, la cui tangente è hello specificato espressione numerica. Detta anche arcotangente.  
  
 **Sintassi**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio restituisce hello ATAN di hello seguente valore specificato.  
  
```  
SELECT ATAN(-45.01)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a> ATN2  
 Restituisce hello valore principale di hello arcotangente di y / x, espresso in radianti.  
  
 **Sintassi**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 esempio Hello calcola hello ATN2 per hello specificato x e y componenti.  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a> CEILING  
 Restituisce hello più piccolo valore integer maggiore di o uguale a, hello espressione numerica specificata.  
  
 **Sintassi**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello di esempio seguente mostra i numeri positivi, negativi e valori zero con hello funzione CEILING.  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a> COS  
 Restituisce hello coseno trigonometrico hello specificato angolo, espresso in radianti, in hello espressione specificata.  
  
 **Sintassi**  
  
```  
COS(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello di esempio seguente calcola hello CO di hello specificato angolo.  
  
```  
SELECT COS(14.78)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a> COT  
 Restituisce hello cotangente trigonometrica hello specificato angolo, espresso in radianti, in hello specificato espressione numerica.  
  
 **Sintassi**  
  
```  
COT(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello di esempio seguente calcola hello COTANGENTE dell'angolo specificato hello.  
  
```  
SELECT COT(124.1332)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a> DEGREES  
 Restituisce hello angolo corrispondente in gradi di un angolo specificato espresso in radianti.  
  
 **Sintassi**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente restituisce hello numero di gradi di un angolo di PI/2 radianti.  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a> FLOOR  
 Restituisce l'intero più grande hello minore o uguale toohello specificato espressione numerica.  
  
 **Sintassi**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello di esempio seguente mostra i numeri positivi, negativi e valori zero con hello FLOOR (funzione).  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a> EXP  
 Hello restituisce il valore esponenziale di hello specificato espressione numerica.  
  
 **Sintassi**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **Osservazioni**  
  
 costante Hello **e** (2.718281 …) è hello base dei logaritmi naturali.  
  
 esponente di un numero Hello è hello costante **e** generato toohello potenza del numero di hello. Ad esempio, EXP(1.0) = e^1.0 = 2,71828182845905 e EXP(10) = e^10 = 22026,4657948067.  
  
 Hello esponenziale del logaritmo naturale di hello di un numero è il numero hello stesso: EXP (LOG (n)) = n. E hello del logaritmo naturale di hello esponenziale di un numero è il numero hello stesso: LOG (EXP (n)) = n.  
  
 **esempi**  
  
 Hello esempio seguente dichiara una variabile e restituisce hello valore esponenziale della variabile specificata hello (10).  
  
```  
SELECT EXP(10)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 Hello esempio seguente restituisce hello valore esponenziale del logaritmo naturale di hello 20 e il logaritmo naturale hello di hello esponenziale di 20. Poiché queste funzioni sono inverse una da altra, il valore restituito di hello con arrotondamento matematico in entrambi i casi è 20 virgola mobile.  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a> LOG  
 Logaritmo naturale di hello restituisce di hello specificato espressione numerica.  
  
 **Sintassi**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
-   `base`  
  
     Argomento numerico facoltativo che imposta la base logaritmo hello hello.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **Osservazioni**  
  
 Per impostazione predefinita, log () restituisce logaritmo naturale di hello. È possibile modificare base hello hello logaritmo tooanother valore con parametri di base facoltativo hello.  
  
 Logaritmo naturale di Hello è hello logaritmo toohello base **e**, dove **e** è un too2.718281828 approssimativamente costante non razionale.  
  
 Logaritmo naturale di Hello di hello esponenziale di un numero è numero hello stesso: LOG (EXP (n)) = n. E hello esponenziale del logaritmo naturale di hello di un numero è il numero hello stesso: EXP (LOG (n)) = n.  
  
 **esempi**  
  
 Hello esempio seguente viene dichiarata una variabile e restituisce hello logaritmo valore della variabile specificata hello (10).  
  
```  
SELECT LOG(10)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 Hello esempio seguente calcola hello LOG per l'esponente hello di un numero.  
  
```  
SELECT EXP(LOG(10))  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a> LOG10  
 Logaritmo in base 10 di hello restituisce hello specificato espressione numerica.  
  
 **Sintassi**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **Osservazioni**  
  
 Hello LOG10 e funzioni POWER sono inversamente correlate tooone un altro. Ad esempio, 10 ^ LOG10(n) = n.  
  
 **esempi**  
  
 Hello esempio seguente viene dichiarata una variabile e restituisce il valore LOG10 hello della variabile specificata hello (100).  
  
```  
SELECT LOG10(100)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a> PI  
 Restituisce hello valore costante di pi greco.  
  
 **Sintassi**  
  
```  
PI ()  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente restituisce il valore di hello di pi greco.  
  
```  
SELECT PI()  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a> POWER  
 Valore di hello specificato di hello restituisce espressione toohello potenza specificata.  
  
 **Sintassi**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
-   `y`  
  
     È hello power toowhich tooraise `numeric_expression`.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello di esempio seguente viene illustrata la generazione di un numero toohello potenza 3 (cubo hello del numero di hello).  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a> RADIANS  
 Restituisce radianti quando viene immessa un'espressione numerica, espresso in gradi.  
  
 **Sintassi**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente accetta alcuni angoli come input e restituisce i relativi valori in radianti.  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a> ROUND  
 Restituisce un valore numerico, il valore intero più vicino di toohello arrotondato.  
  
 **Sintassi**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello seguente Arrotonda hello dopo i numeri positivi e negativi toohello numero intero più vicino.  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a> SIGN  
 Restituisce hello positivo (+ 1), zero (0) o negativo (-1) segno di hello specificato espressione numerica.  
  
 **Sintassi**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente restituisce valori di hello SIGN dei numeri da-2 too2.  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a> SIN  
 Restituisce hello seno trigonometrico hello specificato angolo, espresso in radianti, in hello espressione specificata.  
  
 **Sintassi**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello di esempio seguente calcola hello seno dell'angolo specificato hello.  
  
```  
SELECT SIN(45.175643)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a> SQRT  
 Radice quadrata di hello restituisce di hello specificato valore numerico.  
  
 **Sintassi**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente restituisce hello di radici quadrate dei numeri da 1 a 3.  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a> SQUARE  
 Hello restituisce quadrato di hello specificato valore numerico.  
  
 **Sintassi**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente restituisce i quadrati hello di numeri da 1 a 3.  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a> TAN  
 Tangente di hello restituisce di hello specificato angolo, espresso in radianti, in hello espressione specificata.  
  
 **Sintassi**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 esempio Hello calcola hello tangente di PI () / 2.  
  
```  
SELECT TAN(PI()/2);  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a> TRUNC  
 Restituisce un valore numerico, il valore intero più vicino di toohello troncato.  
  
 **Sintassi**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **Argomenti**  
  
-   `numeric_expression`  
  
     È un'espressione numerica.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello di esempio seguente tronca hello seguente toohello numeri positivi e negativi più vicino valore integer.  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a> Funzioni di controllo del tipo  
 funzioni seguenti Hello supportano controllo in base a valori di input del tipo, ogni funzione restituisce un valore booleano.  
  
||||  
|-|-|-|  
|[IS_ARRAY](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a> IS_ARRAY  
 Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è una matrice.  
  
 **Sintassi**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **Argomenti**  
  
-   `expression`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando la funzione IS_ARRAY hello.  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a> IS_BOOL  
 Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un valore booleano.  
  
 **Sintassi**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **Argomenti**  
  
-   `expression`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando hello funzione IS_BOOL.  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a> IS_DEFINED  
 Restituisce un valore booleano che indica se la proprietà hello è stata assegnata un valore.  
  
 **Sintassi**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **Argomenti**  
  
-   `expression`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello seguente esempio viene controllato per la presenza di hello di una proprietà all'interno di hello specificato documento JSON. Hello primo risultato è true perché "a" è presente, ma hello secondo restituisce false perché "b" è assente.  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a> IS_NULL  
 Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è null.  
  
 **Sintassi**  
  
```  
IS_NULL(<expression>)  
```  
  
 **Argomenti**  
  
-   `expression`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando la funzione IS_NULL hello.  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a> IS_NUMBER  
 Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un numero.  
  
 **Sintassi**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **Argomenti**  
  
-   `expression`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando la funzione IS_NULL hello.  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a> IS_OBJECT  
 Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un oggetto JSON.  
  
 **Sintassi**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **Argomenti**  
  
-   `expression`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando la funzione IS_OBJECT hello.  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a> IS_PRIMITIVE  
 Restituisce un valore booleano che indica se il tipo di hello di hello specificato espressione è una primitiva (stringa, booleano, numerico o null).  
  
 **Sintassi**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **Argomenti**  
  
-   `expression`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando hello funzione IS_PRIMITIVE.  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a> IS_STRING  
 Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è una stringa.  
  
 **Sintassi**  
  
```  
IS_STRING(<expression>)  
```  
  
 **Argomenti**  
  
-   `expression`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando hello funzione IS_STRING.  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a> Funzioni stringa  
 Hello funzioni scalari seguenti eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, numerico o booleano.  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[CONTAINS](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[LEFT](#bk_left)|[LENGTH](#bk_length)|  
|[LOWER](#bk_lower)|[LTRIM](#bk_ltrim)|[REPLACE](#bk_replace)|  
|[REPLICATE](#bk_replicate)|[REVERSE](#bk_reverse)|[RIGHT](#bk_right)|  
|[RTRIM](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[SUBSTRING](#bk_substring)|  
|[UPPER](#bk_upper)|||  
  
####  <a name="bk_concat"></a> CONCAT  
 Restituisce una stringa che rappresenta il risultato di hello del concatenamento di due o più valori di stringa.  
  
 **Sintassi**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello seguente esempio restituisce la stringa hello concatenato di hello valori specificati.  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a> CONTAINS  
 Restituisce un valore booleano che indica se prima espressione di stringa hello contiene hello secondo.  
  
 **Sintassi**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente viene controllato se "abc" contiene "ab" e che contiene "d".  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a> ENDSWITH  
 Restituisce un valore booleano che indica se prima espressione di stringa hello termina con hello secondo.  
  
 **Sintassi**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello esempio seguente restituisce hello "abc" termina con "b" e "bc".  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a> INDEX_OF  
 Restituisce hello a partire dalla posizione della prima occorrenza di hello della seconda espressione stringa hello all'hello prima espressione stringa specificata oppure -1 se la stringa hello non viene trovata.  
  
 **Sintassi**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello esempio seguente viene restituito indice hello di diverse sottostringhe all'interno di "abc".  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a> LEFT  
 Restituisce la parte sinistra di una stringa di hello con hello specificato numero di caratteri.  
  
 **Sintassi**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
-   `num_expr`  
  
     È qualsiasi espressione numerica valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello esempio seguente restituisce hello parte di "abc" per diversi valori di lunghezza a sinistra.  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a> LENGTH  
 Restituisce il numero di caratteri di hello hello specificato espressione stringa.  
  
 **Sintassi**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello esempio seguente restituisce una stringa di lunghezza hello.  
  
```  
SELECT LENGTH("abc")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a> LOWER  
 Restituisce un'espressione stringa dopo aver convertito i caratteri maiuscoli in caratteri toolowercase di dati.  
  
 **Sintassi**  
  
```  
LOWER(<str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello seguente esempio viene illustrato come toouse inferiore in una query.  
  
```  
SELECT LOWER("Abc")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a> LTRIM  
 Restituisce un'espressione stringa dopo aver rimosso gli spazi vuoti iniziali.  
  
 **Sintassi**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello seguente esempio viene illustrato come toouse LTRIM all'interno di una query.  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a> REPLACE  
 Sostituisce tutte le occorrenze di un valore stringa specificato con un altro valore stringa.  
  
 **Sintassi**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello di esempio seguente viene illustrato come toouse SOSTITUISCONO in una query.  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a> REPLICATE  
 Ripete un valore stringa in un numero di volte specificato.  
  
 **Sintassi**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
-   `num_expr`  
  
     È qualsiasi espressione numerica valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello di esempio seguente viene illustrato come eseguire la replica toouse in una query.  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a> REVERSE  
 Restituisce l'inverso di hello di un valore stringa.  
  
 **Sintassi**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello di esempio seguente viene illustrato come toouse inversa in una query.  
  
```  
SELECT REVERSE("Abc")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a> RIGHT  
 Hello restituisce parte destra di una stringa con hello numero specificato di caratteri.  
  
 **Sintassi**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
-   `num_expr`  
  
     È qualsiasi espressione numerica valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello esempio seguente restituisce hello parte destra di "abc" per diversi valori di lunghezza.  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a> RTRIM  
 Restituisce un'espressione di stringa dopo aver rimosso gli spazi vuoti finali.  
  
 **Sintassi**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello seguente esempio viene illustrato come toouse RTRIM all'interno di una query.  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a> STARTSWITH  
 Restituisce un valore booleano che indica se prima espressione di stringa hello inizia con hello secondo.  
  
 **Sintassi**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello seguente controlla se hello stringa "abc" inizia con "b" e "a".  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a> SUBSTRING  
 Restituisce parte di un'espressione stringa a partire da hello posizione in base zero del carattere specificata e continua toohello specificato, lunghezza o alla fine di toohello della stringa hello.  
  
 **Sintassi**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
-   `num_expr`  
  
     È qualsiasi espressione numerica valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello esempio seguente restituisce la sottostringa hello di "abc" a partire da 1 e una lunghezza di 1 carattere.  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a> UPPER  
 Restituisce un'espressione stringa dopo la conversione toouppercase di dati carattere minuscolo.  
  
 **Sintassi**  
  
```  
UPPER(<str_expr>)  
```  
  
 **Argomenti**  
  
-   `str_expr`  
  
     È qualsiasi espressione di stringa valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di stringa.  
  
 **esempi**  
  
 Hello seguente esempio viene illustrato come toouse superiore in una query  
  
```  
SELECT UPPER("Abc")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a> Funzioni di matrice  
 Hello funzioni scalari seguenti esegue un'operazione su un valore di input di matrice e restituito numerico, valore booleano o di matrice  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a> ARRAY_CONCAT  
 Restituisce una matrice che rappresenta il risultato di hello della concatenazione di due o più valori della matrice.  
  
 **Sintassi**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **Argomenti**  
  
-   `arr_expr`  
  
     È qualsiasi espressione di matrice valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione di matrice.  
  
 **esempi**  
  
 Hello seguente esempio come tooconcatenate due matrici.  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a> ARRAY_CONTAINS  
 Restituisce un valore booleano che indica se la matrice hello contiene hello valore specificato.  
  
 **Sintassi**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **Argomenti**  
  
-   `arr_expr`  
  
     È qualsiasi espressione di matrice valida.  
  
-   `expr`  
  
     È qualsiasi espressione valida.  
  
 **Tipi restituiti**  
  
 Restituisce un valore booleano.  
  
 **esempi**  
  
 Hello seguente come esempio toocheck per l'appartenenza a una matrice tramite ARRAY_CONTAINS.  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a> ARRAY_LENGTH  
 Restituisce il numero di elementi di hello hello specificata espressione di matrice.  
  
 **Sintassi**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **Argomenti**  
  
-   `arr_expr`  
  
     È qualsiasi espressione di matrice valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica.  
  
 **esempi**  
  
 Hello seguente esempio come tooget hello lunghezza di una matrice tramite ARRAY_LENGTH.  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a> ARRAY_SLICE  
 Restituisce parte di un'espressione di matrice.
  
 **Sintassi**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argomenti**  
  
-   `arr_expr`  
  
     È qualsiasi espressione di matrice valida.  
  
-   `num_expr`  
  
     È qualsiasi espressione numerica valida.  
  
 **Tipi restituiti**  
  
 Restituisce un valore booleano.  
  
 **esempi**  
  
 Hello seguente come esempio tooget una parte di una matrice tramite ARRAY_SLICE.  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a> Funzioni spaziali  
 Hello funzioni scalari seguenti eseguono un'operazione su un valore di oggetto spaziale input e restituiscono un valore numerico o booleano.  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a> ST_DISTANCE  
 Restituisce la distanza hello tra espressioni di hello due LineString, Polygon o punto GeoJSON.  
  
 **Sintassi**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argomenti**  
  
-   `spatial_expr`  
  
     È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione numerica che contiene la distanza hello. Questo è espresso in metri per il sistema di riferimento predefinito hello.  
  
 **esempi**  
  
 Hello seguente esempio viene illustrato come tooreturn tutti i documenti della famiglia entro 30 chilometri di hello specificato percorso funzione hello ST_DISTANCE incorporato. .  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a> ST_WITHIN  
 Restituisce un'espressione booleana che indica se hello GeoJSON l'oggetto (punto, poligono o LineString) specificato nel primo argomento hello è all'interno di hello GeoJSON (punto, poligono o LineString) nel secondo argomento hello.  
  
 **Sintassi**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argomenti**  
  
-   `spatial_expr`  
  
     È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.  
 
-   `spatial_expr`  
  
     È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.  
  
 **Tipi restituiti**  
  
 Restituisce un valore booleano.  
  
 **esempi**  
  
 Hello di esempio seguente viene illustrato come toofind famiglia tutti i documenti all'interno di un poligono utilizzando ST_WITHIN.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a> ST_INTERSECTS  
 Restituisce un'espressione booleana che indica se hello GeoJSON l'oggetto (punto, poligono o LineString) specificato nel primo argomento hello interseca hello GeoJSON (punto, poligono o LineString) nel secondo argomento hello.  
  
 **Sintassi**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argomenti**  
  
-   `spatial_expr`  
  
     È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.  
 
-   `spatial_expr`  
  
     È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.  
  
 **Tipi restituiti**  
  
 Restituisce un valore booleano.  
  
 **esempi**  
  
 Hello seguente esempio viene illustrato come toofind tutte le aree che si interseca con hello dato poligono.  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a> ST_ISVALID  
 Restituisce un valore booleano che indica se hello LineString, Polygon o punto GeoJSON espressione è valida.  
  
 **Sintassi**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argomenti**  
  
-   `spatial_expr`  
  
     È qualsiasi espressione di punto GeoJSON, poligono o LineString valida.  
  
 **Tipi restituiti**  
  
 Restituisce un'espressione booleana.  
  
 **esempi**  
  
 Hello seguente esempio viene illustrato come toocheck se un punto valido utilizzando ST_VALID.  
  
 Ad esempio, questo punto ha un valore di latitudine che non è compreso nell'intervallo valido di hello di valori [-90, 90], pertanto hello query restituisce false.  
  
 Per i poligoni, hello GeoJSON specifica richiede che hello ultima coppia di coordinate specificato deve essere hello stesso come hello innanzitutto toocreate una forma chiusa. I punti all'interno di un poligono devono essere specificati in senso antiorario. Un poligono specificato nell'ordine in senso orario rappresenta inverso hello dell'area di hello in esso contenuti.  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED  
 Restituisce un valore JSON che contiene un valore booleano se hello specificato LineString, Polygon o punto GeoJSON espressione sia valido e se non è valido, è inoltre hello motivo come valore stringa.  
  
 **Sintassi**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argomenti**  
  
-   `spatial_expr`  
  
     È qualsiasi espressione di punto GeoJSON o poligono valida.  
  
 **Tipi restituiti**  
  
 Restituisce un valore JSON che contiene un valore booleano se hello specificato punto GeoJSON o espressione poligono sia valido e se non è valido, è inoltre hello motivo come valore stringa.  
  
 **esempi**  
  
 Hello seguente come esempio validità toocheck (con i dettagli) utilizzando ST_ISVALIDDETAILED.  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 Di seguito è riportato il set di risultati hello.  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Query e sintassi SQL per Azure Cosmos DB](documentdb-sql-query.md)   
 [Documentazione di Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
