---
<span data-ttu-id="630d1-101">titolo: aaa "API di Azure Cosmos DB DocumentDB: la sintassi SQL | Descrizione di Microsoft Docs": fare riferimento alla documentazione per il linguaggio di query SQL di Azure Cosmos DB DocumentDB API hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="630d1-102">servizi: cosmos db autore: manager mimig1: jhubbard editor: mimig documentationcenter: '</span><span class="sxs-lookup"><span data-stu-id="630d1-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="630d1-103">ms. AssetID: ms. Service: cosmos db Workload: ms. tgt_pltfrm servizi dati: ms. DevLang na: ms. topic na: fare riferimento a MS. date: 13/06/2017 Author: mimig</span><span class="sxs-lookup"><span data-stu-id="630d1-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="630d1-104">API di DocumentDB per Azure Cosmos DB: riferimento per la sintassi SQL</span><span class="sxs-lookup"><span data-stu-id="630d1-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="630d1-105">Hello Azure Cosmos DB l'API DocumentDB supporta documenti l'esecuzione di query mediante una familiare SQL (Structured Query Language) grammatica simile su documenti JSON gerarchici senza richiedere uno schema esplicito o la creazione di indici secondari.</span><span class="sxs-lookup"><span data-stu-id="630d1-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="630d1-106">In questo argomento fornisce la documentazione di riferimento per il linguaggio di query SQL API DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="630d1-107">Per una procedura dettagliata di hello linguaggio di query SQL API DocumentDB, vedere [query SQL per l'API Azure Cosmos DB DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="630d1-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="630d1-108">Anche Microsoft invita è hello toovisit [Query Playground](http://www.documentdb.com/sql/demo) in cui è possibile provare Azure Cosmos DB ed eseguire query SQL nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="630d1-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="630d1-109">Query SELECT</span><span class="sxs-lookup"><span data-stu-id="630d1-109">SELECT query</span></span>  
<span data-ttu-id="630d1-110">Recupera documenti JSON dal database di hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="630d1-111">Supporta la valutazione delle espressioni, le proiezioni, il filtraggio e i join.</span><span class="sxs-lookup"><span data-stu-id="630d1-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="630d1-112">convenzioni di Hello usate per descrivere le istruzioni SELECT hello vengano inserite nella sezione convenzioni della sintassi hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="630d1-113">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="630d1-114">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-114">**Remarks**</span></span>  
  
 <span data-ttu-id="630d1-115">Per i dettagli su ogni clausola, vedere le sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="630d1-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="630d1-116">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="630d1-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="630d1-117">Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="630d1-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="630d1-118">Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="630d1-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="630d1-119">Clausola ORDER BY</span><span class="sxs-lookup"><span data-stu-id="630d1-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="630d1-120">clausole Hello nell'istruzione SELECT hello devono essere ordinate come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="630d1-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="630d1-121">Una delle clausole facoltative hello può essere omessa.</span><span class="sxs-lookup"><span data-stu-id="630d1-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="630d1-122">Tuttavia, quando si utilizzano clausole facoltative, è necessario specificarle nell'ordine corretto hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="630d1-123">**Ordine di elaborazione logica dell'istruzione SELECT hello**</span><span class="sxs-lookup"><span data-stu-id="630d1-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="630d1-124">l'ordine in cui vengono elaborate clausole Hello è:</span><span class="sxs-lookup"><span data-stu-id="630d1-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="630d1-125">Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="630d1-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="630d1-126">Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="630d1-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="630d1-127">Clausola ORDER BY</span><span class="sxs-lookup"><span data-stu-id="630d1-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="630d1-128">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="630d1-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="630d1-129">Si noti che questo è diverso dall'ordine hello in cui appaiono nella sintassi hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="630d1-130">ordinamento Hello è tale che tutti i nuovi simboli introdotti da una clausola elaborata sono visibili e possono essere utilizzati nelle clausole elaborate successivamente.</span><span class="sxs-lookup"><span data-stu-id="630d1-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="630d1-131">Ad esempio, gli alias dichiarati in una clausola FROM sono accessibili nelle clausole WHERE e SELECT.</span><span class="sxs-lookup"><span data-stu-id="630d1-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="630d1-132">**Spazi vuoti e commenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="630d1-133">Tutti i caratteri di spazio vuoto che non fanno parte di una stringa tra virgolette o identificatore tra virgolette non fanno parte della grammatica del linguaggio hello e vengono ignorati durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="630d1-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="630d1-134">il linguaggio di query di Hello supporta commenti in stile T-SQL come</span><span class="sxs-lookup"><span data-stu-id="630d1-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="630d1-135">istruzione SQL `-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="630d1-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="630d1-136">Mentre i commenti e gli spazi vuoti non presentano alcun significato nella grammatica hello, devono essere utilizzati tooseparate token.</span><span class="sxs-lookup"><span data-stu-id="630d1-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="630d1-137">Ad esempio: `-1e5` è un token numero singolo, mentre `: – 1 e5` è un token meno seguito dal numero 1 e dall'identificatore e5.</span><span class="sxs-lookup"><span data-stu-id="630d1-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="630d1-138"><a name="bk_select_query"></a> Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="630d1-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="630d1-139">clausole Hello nell'istruzione SELECT hello devono essere ordinate come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="630d1-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="630d1-140">Una delle clausole facoltative hello può essere omessa.</span><span class="sxs-lookup"><span data-stu-id="630d1-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="630d1-141">Tuttavia, quando si utilizzano clausole facoltative, è necessario specificarle nell'ordine corretto hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="630d1-142">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="630d1-143">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="630d1-144">Imposta proprietà o il valore toobe selezionati per il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="630d1-145">Specifica che il valore di hello deve essere recuperato senza apportare alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="630d1-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="630d1-146">In particolare, se il valore di hello elaborato è un oggetto, tutte le proprietà verranno recuperate.</span><span class="sxs-lookup"><span data-stu-id="630d1-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="630d1-147">Specifica l'elenco di hello di toobe proprietà recuperata.</span><span class="sxs-lookup"><span data-stu-id="630d1-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="630d1-148">Ogni valore restituito sarà un oggetto con proprietà hello specificate.</span><span class="sxs-lookup"><span data-stu-id="630d1-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="630d1-149">Specifica che deve essere recuperato il valore JSON hello anziché l'intero oggetto JSON di hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="630d1-150">Questo, a differenza `<property_list>` non va a capo valore hello proiettato in un oggetto.</span><span class="sxs-lookup"><span data-stu-id="630d1-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="630d1-151">Espressione che rappresenta hello valore toobe calcolato.</span><span class="sxs-lookup"><span data-stu-id="630d1-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="630d1-152">Vedere la sezione [Espressioni scalari](#bk_scalar_expressions) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="630d1-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="630d1-153">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-153">**Remarks**</span></span>  
  
<span data-ttu-id="630d1-154">Hello `SELECT *` sintassi è valida solo se clausola FROM ha dichiarato esattamente un alias.</span><span class="sxs-lookup"><span data-stu-id="630d1-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="630d1-155">`SELECT *` offre una proiezione dell'identità, che può essere utile se non è necessaria alcuna proiezione.</span><span class="sxs-lookup"><span data-stu-id="630d1-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="630d1-156">SELECT * è valida solo se viene specificata la clausola FROM e se viene introdotta solo una singola origine di input.</span><span class="sxs-lookup"><span data-stu-id="630d1-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="630d1-157">Si noti che `SELECT <select_list>` e `SELECT *` sono "zucchero sintattico" e può essere espressi in alternativa usando semplici istruzioni SELECT, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="630d1-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="630d1-158">Equivale a:</span><span class="sxs-lookup"><span data-stu-id="630d1-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="630d1-159">Equivale a:</span><span class="sxs-lookup"><span data-stu-id="630d1-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="630d1-160">**Vedere anche**</span><span class="sxs-lookup"><span data-stu-id="630d1-160">**See Also**</span></span>  
  
[<span data-ttu-id="630d1-161">Espressioni scalari</span><span class="sxs-lookup"><span data-stu-id="630d1-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="630d1-162">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="630d1-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="630d1-163"><a name="bk_from_clause"></a> Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="630d1-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="630d1-164">Specifica l'origine hello o origini unite in join.</span><span class="sxs-lookup"><span data-stu-id="630d1-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="630d1-165">clausola FROM Hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="630d1-165">hello FROM clause is optional.</span></span> <span data-ttu-id="630d1-166">Se non viene specificata, le altre clausole verranno comunque eseguite come se la clausola FROM specificasse un singolo documento.</span><span class="sxs-lookup"><span data-stu-id="630d1-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="630d1-167">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="630d1-168">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="630d1-169">Specifica un'origine dati, con o senza un alias.</span><span class="sxs-lookup"><span data-stu-id="630d1-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="630d1-170">Se non viene specificato alcun alias, tale elemento verrà inferito da hello `<collection_expression>` utilizzando le seguenti regole:</span><span class="sxs-lookup"><span data-stu-id="630d1-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="630d1-171">Se l'espressione hello è collection_name, come alias verrà usato collection_name.</span><span class="sxs-lookup"><span data-stu-id="630d1-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="630d1-172">Se l'espressione hello è `<collection_expression>`, verrà usato property_name, property_name come alias.</span><span class="sxs-lookup"><span data-stu-id="630d1-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="630d1-173">Se l'espressione hello è collection_name, come alias verrà usato collection_name.</span><span class="sxs-lookup"><span data-stu-id="630d1-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="630d1-174">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="630d1-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="630d1-175">Specifica che hello `input_alias` è un set di valori restituiti da hello espressione di raccolta sottostante.</span><span class="sxs-lookup"><span data-stu-id="630d1-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="630d1-176">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="630d1-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="630d1-177">Specifica che hello `input_alias` deve rappresentare il set di hello di valori ottenuti eseguendo l'iterazione su tutti gli elementi di matrice di ogni matrice restituita dall'espressione di raccolta sottostante hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="630d1-178">Tutti i valori restituiti dall'espressione di raccolta sottostante che non sono matrici vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="630d1-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="630d1-179">Specifica hello raccolta espressione toobe documenti hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="630d1-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="630d1-180">Specifica che il documento deve essere recuperato da predefinito hello, raccolta attualmente connesso.</span><span class="sxs-lookup"><span data-stu-id="630d1-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="630d1-181">Specifica che il documento deve essere recuperato dalla raccolta hello fornito.</span><span class="sxs-lookup"><span data-stu-id="630d1-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="630d1-182">nome Hello dell'insieme di hello deve corrispondere il nome di hello dell'insieme di hello attualmente connessi.</span><span class="sxs-lookup"><span data-stu-id="630d1-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="630d1-183">Specifica che il documento deve essere recuperato da hello altra origine definita dall'alias di hello fornito.</span><span class="sxs-lookup"><span data-stu-id="630d1-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="630d1-184">Specifica che il documento deve essere recuperato accedendo hello `property_name` elemento di matrice array_index o di proprietà per tutti i documenti recuperati dall'espressione di raccolta specificata.</span><span class="sxs-lookup"><span data-stu-id="630d1-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="630d1-185">Specifica che il documento deve essere recuperato accedendo hello `property_name` elemento di matrice array_index o di proprietà per tutti i documenti recuperati dall'espressione di raccolta specificata.</span><span class="sxs-lookup"><span data-stu-id="630d1-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="630d1-186">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-186">**Remarks**</span></span>  
  
<span data-ttu-id="630d1-187">Tutti gli alias fornito o dedotto in hello `<from_source>(`s) deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="630d1-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="630d1-188">Sintassi di Hello `<collection_expression>.`property_name è hello identico `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="630d1-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="630d1-189">Tuttavia, quest ' ultima hello utilizzabile se un nome di proprietà contiene un carattere non identificatore.</span><span class="sxs-lookup"><span data-stu-id="630d1-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="630d1-190">**Proprietà mancanti, elementi di matrice mancanti, gestione dei valori non definita**</span><span class="sxs-lookup"><span data-stu-id="630d1-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="630d1-191">Se un'espressione di raccolta accede alle proprietà o agli elementi di matrice e il valore non esiste, tale valore verrà ignorato e non elaborato ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="630d1-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="630d1-192">**Definizione dell'ambito per il contesto dell'espressione di raccolta**</span><span class="sxs-lookup"><span data-stu-id="630d1-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="630d1-193">Un'espressione di raccolta può avere come ambito una raccolta o un documento:</span><span class="sxs-lookup"><span data-stu-id="630d1-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="630d1-194">È un'espressione con ambito raccolta, se hello origine sottostante dell'espressione di raccolta hello è ROOT o `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="630d1-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="630d1-195">Un'espressione di questo tipo rappresenta un set di documenti recuperati direttamente dalla raccolta hello e non è dipendente dall'elaborazione hello di altre espressioni di raccolta.</span><span class="sxs-lookup"><span data-stu-id="630d1-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="630d1-196">Un'espressione è un ambito documento, se hello origine sottostante dell'espressione di raccolta hello è `input_alias` introdotta in precedenza nella query hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="630d1-197">Un'espressione di questo tipo rappresenta un set di documenti ottenuti dalla valutazione di espressione di raccolta hello nell'ambito di hello di ogni documento appartenente toohello set associato hello alias insieme.</span><span class="sxs-lookup"><span data-stu-id="630d1-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="630d1-198">set di Hello risultante sarà un'unione di set ottenuti valutando l'espressione di raccolta hello per ognuno dei documenti hello in hello sottostante set.</span><span class="sxs-lookup"><span data-stu-id="630d1-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="630d1-199">**Join**</span><span class="sxs-lookup"><span data-stu-id="630d1-199">**Joins**</span></span>  
  
<span data-ttu-id="630d1-200">Nella versione corrente di hello, Azure Cosmos DB supporta gli inner join.</span><span class="sxs-lookup"><span data-stu-id="630d1-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="630d1-201">Altre funzionalità di join saranno presto disponibili.</span><span class="sxs-lookup"><span data-stu-id="630d1-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="630d1-202">Set di risultati di inner join in un prodotto incrociato completo di hello che fanno parte di join hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="630d1-203">il risultato di Hello di un join a N vie è un set di tuple a N elementi, in cui ogni valore di tupla hello associata hello alias set che fanno parte di join hello che è possibile accedere facendo riferimento a tale alias in altre clausole.</span><span class="sxs-lookup"><span data-stu-id="630d1-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="630d1-204">valutazione Hello di join hello dipende dall'ambito del contesto hello di hello che fanno parte di set di:</span><span class="sxs-lookup"><span data-stu-id="630d1-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="630d1-205">Un join tra il set di raccolta A e il set di raccolta con ambito B genera un prodotto incrociato di tutti gli elementi presenti nei set A e B.</span><span class="sxs-lookup"><span data-stu-id="630d1-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="630d1-206">Un join tra il set A e il set con ambito documento B genera un'unione di tutti i set ottenuti dalla valutazione di un set con ambito documento B per ogni documento del set A.</span><span class="sxs-lookup"><span data-stu-id="630d1-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="630d1-207">Nella versione corrente di hello, da query processor di hello è supportato un massimo di un'espressione con ambito raccolta.</span><span class="sxs-lookup"><span data-stu-id="630d1-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="630d1-208">**Esempi di join:**</span><span class="sxs-lookup"><span data-stu-id="630d1-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="630d1-209">Diamo un'occhiata hello seguente clausola FROM:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="630d1-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="630d1-210">Consentire a ogni origine di definire `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="630d1-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="630d1-211">Questa clausola FROM restituisce un set di N tuple (tuple con N valori).</span><span class="sxs-lookup"><span data-stu-id="630d1-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="630d1-212">Ogni tupla ha valori prodotti dall'iterazione di tutti gli alias della raccolta sui rispettivi set.</span><span class="sxs-lookup"><span data-stu-id="630d1-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="630d1-213">*Esempio di JOIN 1, con 2 origini:*</span><span class="sxs-lookup"><span data-stu-id="630d1-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="630d1-214">Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="630d1-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="630d1-215">Consentire a `<from_source2>` di avere un ambito documento che fa riferimento a input_alias1 e di rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="630d1-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="630d1-216">{1, 2} per `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="630d1-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="630d1-217">{3} per `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="630d1-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="630d1-218">{4, 5} per `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="630d1-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="630d1-219">Hello dalla clausola `<from_source1> JOIN <from_source2>` comporterà hello tuple seguente:</span><span class="sxs-lookup"><span data-stu-id="630d1-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="630d1-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="630d1-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="630d1-221">*Esempio di JOIN 2, con 3 origini:*</span><span class="sxs-lookup"><span data-stu-id="630d1-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="630d1-222">Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="630d1-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="630d1-223">Consentire a `<from_source2>` di avere un ambito documento che fa riferimento `input_alias1` e di rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="630d1-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="630d1-224">{1, 2} per `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="630d1-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="630d1-225">{3} per `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="630d1-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="630d1-226">{4, 5} per `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="630d1-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="630d1-227">Consentire a `<from_source3>` di avere un ambito documento che fa riferimento `input_alias2` e di rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="630d1-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="630d1-228">{100, 200} per `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="630d1-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="630d1-229">{300} per `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="630d1-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="630d1-230">Hello dalla clausola `<from_source1> JOIN <from_source2> JOIN <from_source3>` comporterà hello tuple seguente:</span><span class="sxs-lookup"><span data-stu-id="630d1-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="630d1-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="630d1-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="630d1-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="630d1-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="630d1-233">Mancanza di tuple per altri valori di `input_alias1`, `input_alias2`, per cui hello `<from_source3>` non ha restituito alcun valore.</span><span class="sxs-lookup"><span data-stu-id="630d1-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="630d1-234">*Esempio di JOIN 3, con 3 origini:*</span><span class="sxs-lookup"><span data-stu-id="630d1-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="630d1-235">Consentire a <from_source1> di avere un ambito raccolta e di rappresentare il set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="630d1-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="630d1-236">Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="630d1-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="630d1-237">Consentire a <from_source2> di avere un ambito documento che fa riferimento a input_alias1 e di rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="630d1-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="630d1-238">{1, 2} per `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="630d1-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="630d1-239">{3} per `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="630d1-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="630d1-240">{4, 5} per `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="630d1-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="630d1-241">Consentire `<from_source3>` ambito troppo`input_alias1` e rappresentare insiemi:</span><span class="sxs-lookup"><span data-stu-id="630d1-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="630d1-242">{100, 200} per `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="630d1-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="630d1-243">{300} per `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="630d1-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="630d1-244">Hello dalla clausola `<from_source1> JOIN <from_source2> JOIN <from_source3>` comporterà hello tuple seguente:</span><span class="sxs-lookup"><span data-stu-id="630d1-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="630d1-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="630d1-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="630d1-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="630d1-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="630d1-247">Questo ha comportato il prodotto incrociato tra `<from_source2>` e `<from_source3>` perché entrambi sono con ambito toohello stesso `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="630d1-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="630d1-248">Sono state create 4 (2x2) tuple con valore A, 0 tuple con valore B (1 x 0) e 2 (2x1) tuple con valore C.</span><span class="sxs-lookup"><span data-stu-id="630d1-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="630d1-249">**Vedere anche**</span><span class="sxs-lookup"><span data-stu-id="630d1-249">**See also**</span></span>  
  
 [<span data-ttu-id="630d1-250">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="630d1-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="630d1-251"><a name="bk_where_clause"></a> Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="630d1-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="630d1-252">Specifica la condizione di ricerca hello per hello documenti restituiti dalla query hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="630d1-253">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="630d1-254">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="630d1-255">Specifica hello condizione toobe soddisfatti hello documenti toobe restituito.</span><span class="sxs-lookup"><span data-stu-id="630d1-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="630d1-256">Espressione che rappresenta hello valore toobe calcolato.</span><span class="sxs-lookup"><span data-stu-id="630d1-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="630d1-257">Vedere hello [espressioni scalari](#bk_scalar_expressions) sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="630d1-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="630d1-258">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-258">**Remarks**</span></span>  
  
 <span data-ttu-id="630d1-259">Affinché hello toobe documento ha restituito un'espressione specificata come condizione di filtro deve restituire tootrue.</span><span class="sxs-lookup"><span data-stu-id="630d1-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="630d1-260">Solo un valore booleano true soddisferà la condizione di hello, qualsiasi altro valore: undefined, null, false, numero, matrice o oggetto non soddisferà la condizione hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="630d1-261"><a name="bk_orderby_clause"></a> Clausola ORDER BY</span><span class="sxs-lookup"><span data-stu-id="630d1-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="630d1-262">Specifica l'ordinamento dei risultati restituiti dalla query hello hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="630d1-263">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="630d1-264">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="630d1-265">Specifica una proprietà o l'espressione in cui set di risultati di query hello toosort.</span><span class="sxs-lookup"><span data-stu-id="630d1-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="630d1-266">Una colonna di ordinamento può essere specificata come alias di nome o di colonna.</span><span class="sxs-lookup"><span data-stu-id="630d1-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="630d1-267">È possibile specificare più colonne di ordinamento.</span><span class="sxs-lookup"><span data-stu-id="630d1-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="630d1-268">I nomi delle colonne devono essere univoci.</span><span class="sxs-lookup"><span data-stu-id="630d1-268">Column names must be unique.</span></span> <span data-ttu-id="630d1-269">sequenza di Hello di colonne di ordinamento hello nella clausola ORDER BY hello definisce organizzazione hello del set di risultati ordinato hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="630d1-270">Vale a dire hello set di risultati vengono ordinati prima proprietà hello e quindi tale elenco ordinato viene ordinato in base hello secondo e così via.</span><span class="sxs-lookup"><span data-stu-id="630d1-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="630d1-271">i nomi di colonna Hello a cui fa riferimento nella clausola ORDER BY hello devono corrispondere tooeither una colonna in hello selezionare elenco o tooa colonna definita in una tabella specificata nella clausola FROM hello senza ambiguità.</span><span class="sxs-lookup"><span data-stu-id="630d1-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="630d1-272">Specifica una singola proprietà o un'espressione per il set di risultati query toosort hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="630d1-273">Vedere hello [espressioni scalari](#bk_scalar_expressions) sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="630d1-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="630d1-274">Specifica che i valori nella colonna specificata hello hello devono essere ordinati in ordine crescente o decrescente.</span><span class="sxs-lookup"><span data-stu-id="630d1-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="630d1-275">ASC Ordina dal più basso valore toohighest valore hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="630d1-276">DESC Ordina dal più alto valore toolowest valore.</span><span class="sxs-lookup"><span data-stu-id="630d1-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="630d1-277">ASC è l'ordinamento predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-277">ASC is hello default sort order.</span></span> <span data-ttu-id="630d1-278">Valori null vengono considerati come possibili valori hello più bassi.</span><span class="sxs-lookup"><span data-stu-id="630d1-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="630d1-279">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-279">**Remarks**</span></span>  
  
 <span data-ttu-id="630d1-280">Durante la grammatica di query hello supporta più ordine dalle proprietà, hello Azure Cosmos DB query runtime supporta l'ordinamento solo in una singola proprietà e solo con i nomi di proprietà, ad esempio, non in base a proprietà calcolate.</span><span class="sxs-lookup"><span data-stu-id="630d1-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="630d1-281">L'ordinamento richiede inoltre che hello criteri di indicizzazione include un indice di intervallo per la proprietà hello e hello specificato tipo, con la massima precisione hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="630d1-282">Toohello l'indicizzazione di documentazione per i criteri per ulteriori informazioni, vedere.</span><span class="sxs-lookup"><span data-stu-id="630d1-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="630d1-283"><a name="bk_scalar_expressions"></a> Espressioni scalari</span><span class="sxs-lookup"><span data-stu-id="630d1-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="630d1-284">Un'espressione scalare è una combinazione di simboli e operatori che possono essere valutati tooobtain un singolo valore.</span><span class="sxs-lookup"><span data-stu-id="630d1-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="630d1-285">Le espressioni semplici possono essere costanti, riferimenti a proprietà, riferimenti a elementi di matrice, riferimenti ad alias o chiamate di funzioni.</span><span class="sxs-lookup"><span data-stu-id="630d1-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="630d1-286">Le espressioni semplici possono essere combinate in espressioni complesse usando gli operatori.</span><span class="sxs-lookup"><span data-stu-id="630d1-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="630d1-287">Per informazioni dettagliate sui valori che possono essere contenuti nelle espressioni scalari, vedere la sezione relativa alle [costanti](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="630d1-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="630d1-288">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="630d1-289">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="630d1-290">Rappresenta un valore costante.</span><span class="sxs-lookup"><span data-stu-id="630d1-290">Represents a constant value.</span></span> <span data-ttu-id="630d1-291">Per informazioni dettagliate, vedere la sezione [Costanti](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="630d1-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="630d1-292">Rappresenta un valore definito da hello `input_alias` introdotta in hello `FROM` clausola.</span><span class="sxs-lookup"><span data-stu-id="630d1-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="630d1-293">Questo valore è sicuramente toonot essere **definito** –**definito** i valori nell'input hello verranno ignorati.</span><span class="sxs-lookup"><span data-stu-id="630d1-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="630d1-294">Rappresenta un valore della proprietà hello di un oggetto.</span><span class="sxs-lookup"><span data-stu-id="630d1-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="630d1-295">Se la proprietà hello non esiste o proprietà fa riferimento a un valore che non è un oggetto, quindi hello espressione troppo**definito** valore.</span><span class="sxs-lookup"><span data-stu-id="630d1-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="630d1-296">Rappresenta un valore della proprietà hello con nome `property_name` o elemento di matrice con indice `array_index` di un'oggetto/la matrice.</span><span class="sxs-lookup"><span data-stu-id="630d1-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="630d1-297">Se l'indice di matrice proprietà hello non esiste o l'indice di matrice proprietà hello fa riferimento a un valore che non è una matrice di oggetti o, quindi hello espressione valore tooundefined.</span><span class="sxs-lookup"><span data-stu-id="630d1-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="630d1-298">Rappresenta un operatore applicato tooa singolo valore.</span><span class="sxs-lookup"><span data-stu-id="630d1-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="630d1-299">Per informazioni dettagliate, vedere la sezione [Operatori](#bk_operators).</span><span class="sxs-lookup"><span data-stu-id="630d1-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="630d1-300">Rappresenta un operatore applicato tootwo valori.</span><span class="sxs-lookup"><span data-stu-id="630d1-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="630d1-301">Per informazioni dettagliate, vedere la sezione [Operatori](#bk_operators).</span><span class="sxs-lookup"><span data-stu-id="630d1-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="630d1-302">Rappresenta un valore definito da un risultato di una chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="630d1-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="630d1-303">Nome dell'utente hello funzione scalare definita.</span><span class="sxs-lookup"><span data-stu-id="630d1-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="630d1-304">Nome della funzione scalare predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="630d1-305">Rappresenta un valore ottenuto creando un nuovo oggetto con proprietà specificate e i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="630d1-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="630d1-306">Rappresenta un valore ottenuto creando una nuova matrice con valori specificati come elementi</span><span class="sxs-lookup"><span data-stu-id="630d1-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="630d1-307">Rappresenta un valore del nome di parametro specificato hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="630d1-308">I nomi di parametro deve essere un singolo @ come primo carattere hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="630d1-309">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-309">**Remarks**</span></span>  
  
 <span data-ttu-id="630d1-310">Quando si chiama una funzione scalare predefinita o definita dall'utente è necessario definire tutti gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="630d1-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="630d1-311">Se uno degli argomenti hello è definito, non verrà chiamata la funzione hello e hello risultato sarà indefinito.</span><span class="sxs-lookup"><span data-stu-id="630d1-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="630d1-312">Quando si crea un oggetto, verrà saltata e non presenti nell'oggetto creato hello qualsiasi proprietà che è assegnato il valore undefined.</span><span class="sxs-lookup"><span data-stu-id="630d1-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="630d1-313">Quando la creazione di una matrice, il valore di qualsiasi elemento che viene assegnata **definito** valore verrà ignorato e non inclusi nell'oggetto hello creato.</span><span class="sxs-lookup"><span data-stu-id="630d1-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="630d1-314">In questo modo tootake elemento hello successivamente definita al suo posto in modo tale matrice hello creato verrà non vengano ignorati indici.</span><span class="sxs-lookup"><span data-stu-id="630d1-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="630d1-315"><a name="bk_operators"></a> Operatori</span><span class="sxs-lookup"><span data-stu-id="630d1-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="630d1-316">Questa sezione descrive gli operatori di hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="630d1-316">This section describes hello supported operators.</span></span> <span data-ttu-id="630d1-317">Ogni operatore può essere assegnato tooexactly una categoria.</span><span class="sxs-lookup"><span data-stu-id="630d1-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="630d1-318">Vedere la tabella delle **categorie di operatori** riportata di seguito per informazioni dettagliate sulla gestione dei valori **non definiti**, sui requisiti di tipi per valori di input e sulla gestione dei valori con tipi non corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="630d1-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="630d1-319">**Categorie di operatori:**</span><span class="sxs-lookup"><span data-stu-id="630d1-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="630d1-320">**Categoria**</span><span class="sxs-lookup"><span data-stu-id="630d1-320">**Category**</span></span>|<span data-ttu-id="630d1-321">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="630d1-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="630d1-322">**aritmetico**</span><span class="sxs-lookup"><span data-stu-id="630d1-322">**arithmetic**</span></span>|<span data-ttu-id="630d1-323">L'operatore prevede uno o più input toobe numeri.</span><span class="sxs-lookup"><span data-stu-id="630d1-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="630d1-324">Anche l'output è un numero.</span><span class="sxs-lookup"><span data-stu-id="630d1-324">Output is also a Number.</span></span> <span data-ttu-id="630d1-325">Se uno degli input hello è **definito** o è di tipo diverso dal risultato numero quindi hello **definito**.</span><span class="sxs-lookup"><span data-stu-id="630d1-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="630d1-326">**bit per bit**</span><span class="sxs-lookup"><span data-stu-id="630d1-326">**bitwise**</span></span>|<span data-ttu-id="630d1-327">L'operatore prevede uno o più input numeri interi con segno a 32 bit toobe.</span><span class="sxs-lookup"><span data-stu-id="630d1-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="630d1-328">Anche l'output è un numero intero con segno a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="630d1-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="630d1-329">Gli eventuali valori non interi vengono arrotondati.</span><span class="sxs-lookup"><span data-stu-id="630d1-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="630d1-330">I valori positivi verranno arrotondati per difetto, i valori negativi per eccesso.</span><span class="sxs-lookup"><span data-stu-id="630d1-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="630d1-331">Qualsiasi valore è compreso nell'intervallo integer a 32 bit hello verrà convertiti prendendo ultimi 32 bit della relativi due notazione di complemento.</span><span class="sxs-lookup"><span data-stu-id="630d1-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="630d1-332">Se uno degli input hello è **definito** o un tipo diverso da un numero, il risultato di hello è **definito**.</span><span class="sxs-lookup"><span data-stu-id="630d1-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="630d1-333">**Nota:** hello sopra il comportamento è compatibile con il comportamento di un operatore bit per bit di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="630d1-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="630d1-334">**logico**</span><span class="sxs-lookup"><span data-stu-id="630d1-334">**logical**</span></span>|<span data-ttu-id="630d1-335">L'operatore prevede uno o più input toobe valori booleani.</span><span class="sxs-lookup"><span data-stu-id="630d1-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="630d1-336">Anche l'output è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="630d1-337">Se uno degli input hello è **definito** o un tipo diverso da un valore booleano, verrà utilizzato come risultato di hello **definito**.</span><span class="sxs-lookup"><span data-stu-id="630d1-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="630d1-338">**confronto**</span><span class="sxs-lookup"><span data-stu-id="630d1-338">**comparison**</span></span>|<span data-ttu-id="630d1-339">L'operatore prevede uno o più input toohave hello stesso tipo e non essere indefinito.</span><span class="sxs-lookup"><span data-stu-id="630d1-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="630d1-340">L'output è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="630d1-341">Se uno degli input hello è **definito** o hello input hanno tipi diversi, quindi il risultato di hello è **definito**.</span><span class="sxs-lookup"><span data-stu-id="630d1-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="630d1-342">Vedere la tabella dell'**ordinamento dei valori per il confronto** per informazioni dettagliate sull'ordinamento dei valori.</span><span class="sxs-lookup"><span data-stu-id="630d1-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="630d1-343">**string**</span><span class="sxs-lookup"><span data-stu-id="630d1-343">**string**</span></span>|<span data-ttu-id="630d1-344">L'operatore prevede uno o più input toobe stringhe.</span><span class="sxs-lookup"><span data-stu-id="630d1-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="630d1-345">Anche l'output è una stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-345">Output is also a String.</span></span><br /><span data-ttu-id="630d1-346">Se uno degli input hello è **definito** o è di tipo diverso dal risultato di stringa quindi hello **definito**.</span><span class="sxs-lookup"><span data-stu-id="630d1-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="630d1-347">**Operatori unari:**</span><span class="sxs-lookup"><span data-stu-id="630d1-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="630d1-348">**Nome**</span><span class="sxs-lookup"><span data-stu-id="630d1-348">**Name**</span></span>|<span data-ttu-id="630d1-349">**Operatore**</span><span class="sxs-lookup"><span data-stu-id="630d1-349">**Operator**</span></span>|<span data-ttu-id="630d1-350">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="630d1-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="630d1-351">**aritmetico**</span><span class="sxs-lookup"><span data-stu-id="630d1-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="630d1-352">Restituisce il valore numerico hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="630d1-353">Negazione bit per bit.</span><span class="sxs-lookup"><span data-stu-id="630d1-353">Bitwise negation.</span></span> <span data-ttu-id="630d1-354">Restituisce il valore numerico negato.</span><span class="sxs-lookup"><span data-stu-id="630d1-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="630d1-355">**bit per bit**</span><span class="sxs-lookup"><span data-stu-id="630d1-355">**bitwise**</span></span>|~|<span data-ttu-id="630d1-356">Complemento a uno.</span><span class="sxs-lookup"><span data-stu-id="630d1-356">Ones' complement.</span></span> <span data-ttu-id="630d1-357">Restituisce un complemento di un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="630d1-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="630d1-358">**Logico**</span><span class="sxs-lookup"><span data-stu-id="630d1-358">**Logical**</span></span>|<span data-ttu-id="630d1-359">**NOT**</span><span class="sxs-lookup"><span data-stu-id="630d1-359">**NOT**</span></span>|<span data-ttu-id="630d1-360">Negazione.</span><span class="sxs-lookup"><span data-stu-id="630d1-360">Negation.</span></span> <span data-ttu-id="630d1-361">Restituisce un valore booleano negato.</span><span class="sxs-lookup"><span data-stu-id="630d1-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="630d1-362">**Operatori binari:**</span><span class="sxs-lookup"><span data-stu-id="630d1-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="630d1-363">**Nome**</span><span class="sxs-lookup"><span data-stu-id="630d1-363">**Name**</span></span>|<span data-ttu-id="630d1-364">**Operatore**</span><span class="sxs-lookup"><span data-stu-id="630d1-364">**Operator**</span></span>|<span data-ttu-id="630d1-365">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="630d1-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="630d1-366">**aritmetico**</span><span class="sxs-lookup"><span data-stu-id="630d1-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="630d1-367">Addizione.</span><span class="sxs-lookup"><span data-stu-id="630d1-367">Addition.</span></span><br /><br /> <span data-ttu-id="630d1-368">Sottrazione.</span><span class="sxs-lookup"><span data-stu-id="630d1-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="630d1-369">Moltiplicazione.</span><span class="sxs-lookup"><span data-stu-id="630d1-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="630d1-370">Divisione.</span><span class="sxs-lookup"><span data-stu-id="630d1-370">Division.</span></span><br /><br /> <span data-ttu-id="630d1-371">Modulazione.</span><span class="sxs-lookup"><span data-stu-id="630d1-371">Modulation.</span></span>|  
|<span data-ttu-id="630d1-372">**bit per bit**</span><span class="sxs-lookup"><span data-stu-id="630d1-372">**bitwise**</span></span>|<span data-ttu-id="630d1-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="630d1-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="630d1-374">OR bit per bit.</span><span class="sxs-lookup"><span data-stu-id="630d1-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="630d1-375">AND bit per bit.</span><span class="sxs-lookup"><span data-stu-id="630d1-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="630d1-376">XOR bit per bit.</span><span class="sxs-lookup"><span data-stu-id="630d1-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="630d1-377">Spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="630d1-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="630d1-378">Spostamento a destra.</span><span class="sxs-lookup"><span data-stu-id="630d1-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="630d1-379">Spostamento a destra riempimento zero.</span><span class="sxs-lookup"><span data-stu-id="630d1-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="630d1-380">**logico**</span><span class="sxs-lookup"><span data-stu-id="630d1-380">**logical**</span></span>|<span data-ttu-id="630d1-381">**AND**</span><span class="sxs-lookup"><span data-stu-id="630d1-381">**AND**</span></span><br /><br /> <span data-ttu-id="630d1-382">**OR**</span><span class="sxs-lookup"><span data-stu-id="630d1-382">**OR**</span></span>|<span data-ttu-id="630d1-383">Congiunzione logica.</span><span class="sxs-lookup"><span data-stu-id="630d1-383">Logical conjunction.</span></span> <span data-ttu-id="630d1-384">Restituisce **true** se entrambi gli argomenti sono **true**, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="630d1-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="630d1-385">Congiunzione logica.</span><span class="sxs-lookup"><span data-stu-id="630d1-385">Logical conjunction.</span></span> <span data-ttu-id="630d1-386">Restituisce **true** se entrambi gli argomenti sono **true**, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="630d1-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="630d1-387">**confronto**</span><span class="sxs-lookup"><span data-stu-id="630d1-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="630d1-388">**!=, &lt;&gt;**</span><span class="sxs-lookup"><span data-stu-id="630d1-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="630d1-389">**??**</span><span class="sxs-lookup"><span data-stu-id="630d1-389">**??**</span></span>|<span data-ttu-id="630d1-390">Uguale a.</span><span class="sxs-lookup"><span data-stu-id="630d1-390">Equals.</span></span> <span data-ttu-id="630d1-391">Restituisce **true** se gli argomenti sono uguali, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="630d1-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="630d1-392">Diverso da.</span><span class="sxs-lookup"><span data-stu-id="630d1-392">Not equal to.</span></span> <span data-ttu-id="630d1-393">Restituisce **true** se gli argomenti non sono uguali, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="630d1-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="630d1-394">Maggiore di.</span><span class="sxs-lookup"><span data-stu-id="630d1-394">Greater Than.</span></span> <span data-ttu-id="630d1-395">Restituisce **true** se il primo argomento è maggiore del secondo hello, restituire **false** in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="630d1-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="630d1-396">Maggiore o uguale a.</span><span class="sxs-lookup"><span data-stu-id="630d1-396">Greater Than or Equal To.</span></span> <span data-ttu-id="630d1-397">Restituisce **true** se il primo argomento è maggiore o uguale a toohello secondo, restituire **false** in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="630d1-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="630d1-398">Minore di.</span><span class="sxs-lookup"><span data-stu-id="630d1-398">Less Than.</span></span> <span data-ttu-id="630d1-399">Restituisce **true** se il primo argomento è minore della seconda hello, restituire **false** in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="630d1-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="630d1-400">Minore o uguale a.</span><span class="sxs-lookup"><span data-stu-id="630d1-400">Less Than or Equal To.</span></span> <span data-ttu-id="630d1-401">Restituisce **true** se il primo argomento è minore o uguale toohello secondo uno, restituito **false** in caso contrario.</span><span class="sxs-lookup"><span data-stu-id="630d1-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="630d1-402">Unione.</span><span class="sxs-lookup"><span data-stu-id="630d1-402">Coalesce.</span></span> <span data-ttu-id="630d1-403">Restituisce hello secondo argomento se hello primo argomento è un **definito** valore.</span><span class="sxs-lookup"><span data-stu-id="630d1-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="630d1-404">**String**</span><span class="sxs-lookup"><span data-stu-id="630d1-404">**String**</span></span>|<span data-ttu-id="630d1-405">**&amp;#124;&amp;#124;**</span><span class="sxs-lookup"><span data-stu-id="630d1-405">**&#124;&#124;**</span></span>|<span data-ttu-id="630d1-406">Concatenazione.</span><span class="sxs-lookup"><span data-stu-id="630d1-406">Concatenation.</span></span> <span data-ttu-id="630d1-407">Restituisce una concatenazione di entrambi gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="630d1-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="630d1-408">**Operatori ternari:**</span><span class="sxs-lookup"><span data-stu-id="630d1-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="630d1-409">Operatore ternario</span><span class="sxs-lookup"><span data-stu-id="630d1-409">Ternary operator</span></span>|<span data-ttu-id="630d1-410">?</span><span class="sxs-lookup"><span data-stu-id="630d1-410">?</span></span>|<span data-ttu-id="630d1-411">Restituisce hello secondo argomento se il primo argomento hello valuta troppo**true**; in caso contrario restituito terzo argomento hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="630d1-412">**Ordinamento dei valori per il confronto**</span><span class="sxs-lookup"><span data-stu-id="630d1-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="630d1-413">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="630d1-413">**Type**</span></span>|<span data-ttu-id="630d1-414">**Ordine dei valori**</span><span class="sxs-lookup"><span data-stu-id="630d1-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="630d1-415">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="630d1-415">**Undefined**</span></span>|<span data-ttu-id="630d1-416">Non confrontabile.</span><span class="sxs-lookup"><span data-stu-id="630d1-416">Not comparable.</span></span>|  
|<span data-ttu-id="630d1-417">**Null**</span><span class="sxs-lookup"><span data-stu-id="630d1-417">**Null**</span></span>|<span data-ttu-id="630d1-418">Singolo valore: **null**</span><span class="sxs-lookup"><span data-stu-id="630d1-418">Single value: **null**</span></span>|  
|<span data-ttu-id="630d1-419">**Number**</span><span class="sxs-lookup"><span data-stu-id="630d1-419">**Number**</span></span>|<span data-ttu-id="630d1-420">Numero reale naturale.</span><span class="sxs-lookup"><span data-stu-id="630d1-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="630d1-421">Il valore infinito negativo è minore di qualsiasi altro valore numerico.</span><span class="sxs-lookup"><span data-stu-id="630d1-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="630d1-422">Il valore infinito positivo è maggiore di qualsiasi altro valore numerico. il valore **NaN** non è confrontabile.</span><span class="sxs-lookup"><span data-stu-id="630d1-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="630d1-423">Il confronto con **NaN** restituisce un valore **non definito**.</span><span class="sxs-lookup"><span data-stu-id="630d1-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="630d1-424">**String**</span><span class="sxs-lookup"><span data-stu-id="630d1-424">**String**</span></span>|<span data-ttu-id="630d1-425">Ordine lessicografico.</span><span class="sxs-lookup"><span data-stu-id="630d1-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="630d1-426">**Array**</span><span class="sxs-lookup"><span data-stu-id="630d1-426">**Array**</span></span>|<span data-ttu-id="630d1-427">Nessun ordinamento, ma equo.</span><span class="sxs-lookup"><span data-stu-id="630d1-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="630d1-428">**Object**</span><span class="sxs-lookup"><span data-stu-id="630d1-428">**Object**</span></span>|<span data-ttu-id="630d1-429">Nessun ordinamento, ma equo.</span><span class="sxs-lookup"><span data-stu-id="630d1-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="630d1-430">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-430">**Remarks**</span></span>  
  
 <span data-ttu-id="630d1-431">In Azure Cosmos DB tipi hello di valori sono spesso sconosciuti finché vengono effettivamente recuperati dal database hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="630d1-432">In ordine toosupport un'esecuzione efficiente delle query, la maggior parte degli operatori hello hanno requisiti di tipo strict.</span><span class="sxs-lookup"><span data-stu-id="630d1-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="630d1-433">Inoltre, gli operatori di per sé non eseguono conversioni implicite.</span><span class="sxs-lookup"><span data-stu-id="630d1-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="630d1-434">Ciò significa che una query come: seleziona * FROM ROOT r WHERE Age = 21 restituisce solo documenti con proprietà Age uguale toohello number 21.</span><span class="sxs-lookup"><span data-stu-id="630d1-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="630d1-435">Documenti con proprietà Age uguale toohello stringa "21" o la stringa hello "0021" non corrispondono, come espressione hello "21" = 21 restituisce tooundefined.</span><span class="sxs-lookup"><span data-stu-id="630d1-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="630d1-436">In questo modo per migliorare l'utilizzo di indici, in quanto ricerca hello di un valore specifico (ovvero il numero 21) è più veloce rispetto alla ricerca di un numero indefinito di possibili corrispondenze (numero 21 o le stringhe "21", "021", "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="630d1-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="630d1-437">Ciò si differenzia dal modo in cui JavaScript valuta gli operatori per valori di tipi diversi.</span><span class="sxs-lookup"><span data-stu-id="630d1-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="630d1-438">**Confronto e uguaglianza di oggetti e matrici**</span><span class="sxs-lookup"><span data-stu-id="630d1-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="630d1-439">Il confronto dei valori di oggetto o matrice con gli operatori di intervallo (>, >=, <, <=) produce un risultato indefinito poiché non è definito un ordine per i valori di oggetto o matrice.</span><span class="sxs-lookup"><span data-stu-id="630d1-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="630d1-440">Tuttavia l'uso degli operatori di uguaglianza/disuguaglianza (=,! =, <>) è supportato e i valori vengono confrontati strutturalmente.</span><span class="sxs-lookup"><span data-stu-id="630d1-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="630d1-441">Le matrici sono uguali se entrambe le matrici hanno stesso numero di elementi e sono uguali anche gli elementi nelle posizioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="630d1-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="630d1-442">Se il confronto tra qualsiasi coppia di elementi risultante nel risultato hello definito, di confronto di matrice è definito.</span><span class="sxs-lookup"><span data-stu-id="630d1-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="630d1-443">Gli oggetti sono uguali se entrambi gli oggetti hanno le stesse proprietà definite e se anche i valori delle proprietà corrispondenti sono uguali.</span><span class="sxs-lookup"><span data-stu-id="630d1-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="630d1-444">Se il confronto tra qualsiasi coppia di valori di proprietà comporta risultati hello definito, di confronto di oggetti è definito.</span><span class="sxs-lookup"><span data-stu-id="630d1-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="630d1-445"><a name="bk_constants"></a> Costanti</span><span class="sxs-lookup"><span data-stu-id="630d1-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="630d1-446">Una costante, nota anche come valore letterale o scalare, è un simbolo che rappresenta un valore di dati specifico.</span><span class="sxs-lookup"><span data-stu-id="630d1-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="630d1-447">formato di Hello di una costante dipende dal tipo di dati hello del valore di hello che rappresenta.</span><span class="sxs-lookup"><span data-stu-id="630d1-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="630d1-448">**Tipi di dati scalari supportati:**</span><span class="sxs-lookup"><span data-stu-id="630d1-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="630d1-449">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="630d1-449">**Type**</span></span>|<span data-ttu-id="630d1-450">**Ordine dei valori**</span><span class="sxs-lookup"><span data-stu-id="630d1-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="630d1-451">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="630d1-451">**Undefined**</span></span>|<span data-ttu-id="630d1-452">Singolo valore: **non definito**</span><span class="sxs-lookup"><span data-stu-id="630d1-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="630d1-453">**Null**</span><span class="sxs-lookup"><span data-stu-id="630d1-453">**Null**</span></span>|<span data-ttu-id="630d1-454">Singolo valore: **null**</span><span class="sxs-lookup"><span data-stu-id="630d1-454">Single value: **null**</span></span>|  
|<span data-ttu-id="630d1-455">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="630d1-455">**Boolean**</span></span>|<span data-ttu-id="630d1-456">Valori: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="630d1-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="630d1-457">**Number**</span><span class="sxs-lookup"><span data-stu-id="630d1-457">**Number**</span></span>|<span data-ttu-id="630d1-458">Un numero a virgola mobile e precisione doppia, standard IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="630d1-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="630d1-459">**String**</span><span class="sxs-lookup"><span data-stu-id="630d1-459">**String**</span></span>|<span data-ttu-id="630d1-460">Una sequenza di zero o più caratteri Unicode.</span><span class="sxs-lookup"><span data-stu-id="630d1-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="630d1-461">Le stringhe devono essere racchiuse tra virgolette singole o doppie.</span><span class="sxs-lookup"><span data-stu-id="630d1-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="630d1-462">**Array**</span><span class="sxs-lookup"><span data-stu-id="630d1-462">**Array**</span></span>|<span data-ttu-id="630d1-463">Una sequenza di zero o più elementi.</span><span class="sxs-lookup"><span data-stu-id="630d1-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="630d1-464">Ogni elemento può essere un valore di qualsiasi tipo di dati scalare, tranne Undefined.</span><span class="sxs-lookup"><span data-stu-id="630d1-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="630d1-465">**Object**</span><span class="sxs-lookup"><span data-stu-id="630d1-465">**Object**</span></span>|<span data-ttu-id="630d1-466">Un set non ordinato di zero o più coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="630d1-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="630d1-467">Il nome è una stringa Unicode, il valore può essere di qualsiasi tipo di dati scalare, tranne **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="630d1-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="630d1-468">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="630d1-469">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="630d1-470">Rappresenta un valore non definito di tipo Undefined.</span><span class="sxs-lookup"><span data-stu-id="630d1-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="630d1-471">Rappresenta un valore **null** di tipo **Null**.</span><span class="sxs-lookup"><span data-stu-id="630d1-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="630d1-472">Rappresenta una costante di tipo Boolean.</span><span class="sxs-lookup"><span data-stu-id="630d1-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="630d1-473">Rappresenta un valore **false** di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="630d1-474">Rappresenta un valore **true** di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="630d1-475">Rappresenta una costante.</span><span class="sxs-lookup"><span data-stu-id="630d1-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="630d1-476">I valori letterali decimali sono numeri rappresentati usando la notazione decimale o la notazione scientifica.</span><span class="sxs-lookup"><span data-stu-id="630d1-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="630d1-477">I valori letterali esadecimali sono numeri rappresentati usando il prefisso "0x" seguito da una o più cifre esadecimali.</span><span class="sxs-lookup"><span data-stu-id="630d1-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="630d1-478">Rappresenta una costante di tipo String.</span><span class="sxs-lookup"><span data-stu-id="630d1-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="630d1-479">I valori letterali stringa sono stringhe Unicode rappresentate da una sequenza di zero o più caratteri Unicode o sequenze di escape.</span><span class="sxs-lookup"><span data-stu-id="630d1-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="630d1-480">I valori letterali stringa sono racchiusi tra virgolette singole (apostrofo: ') o virgolette doppie (virgolette inglesi: ").</span><span class="sxs-lookup"><span data-stu-id="630d1-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="630d1-481">Sono consentite le sequenze di escape seguenti:</span><span class="sxs-lookup"><span data-stu-id="630d1-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="630d1-482">**Sequenza di escape**</span><span class="sxs-lookup"><span data-stu-id="630d1-482">**Escape sequence**</span></span>|<span data-ttu-id="630d1-483">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="630d1-483">**Description**</span></span>|<span data-ttu-id="630d1-484">**Carattere Unicode**</span><span class="sxs-lookup"><span data-stu-id="630d1-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="630d1-485">\\'</span><span class="sxs-lookup"><span data-stu-id="630d1-485">\\'</span></span>|<span data-ttu-id="630d1-486">apostrofo (')</span><span class="sxs-lookup"><span data-stu-id="630d1-486">apostrophe (')</span></span>|<span data-ttu-id="630d1-487">U + 0027</span><span class="sxs-lookup"><span data-stu-id="630d1-487">U+0027</span></span>|  
|<span data-ttu-id="630d1-488">\\"</span><span class="sxs-lookup"><span data-stu-id="630d1-488">\\"</span></span>|<span data-ttu-id="630d1-489">virgolette doppie (")</span><span class="sxs-lookup"><span data-stu-id="630d1-489">quotation mark (")</span></span>|<span data-ttu-id="630d1-490">U + 0022</span><span class="sxs-lookup"><span data-stu-id="630d1-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="630d1-491">barra rovesciata (\\)</span><span class="sxs-lookup"><span data-stu-id="630d1-491">reverse solidus (\\)</span></span>|<span data-ttu-id="630d1-492">U + 005C</span><span class="sxs-lookup"><span data-stu-id="630d1-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="630d1-493">barra (/)</span><span class="sxs-lookup"><span data-stu-id="630d1-493">solidus (/)</span></span>|<span data-ttu-id="630d1-494">U + 002F</span><span class="sxs-lookup"><span data-stu-id="630d1-494">U+002F</span></span>|  
|<span data-ttu-id="630d1-495">\b</span><span class="sxs-lookup"><span data-stu-id="630d1-495">\b</span></span>|<span data-ttu-id="630d1-496">BACKSPACE</span><span class="sxs-lookup"><span data-stu-id="630d1-496">backspace</span></span>|<span data-ttu-id="630d1-497">U + 0008</span><span class="sxs-lookup"><span data-stu-id="630d1-497">U+0008</span></span>|  
|<span data-ttu-id="630d1-498">\f</span><span class="sxs-lookup"><span data-stu-id="630d1-498">\f</span></span>|<span data-ttu-id="630d1-499">avanzamento carta</span><span class="sxs-lookup"><span data-stu-id="630d1-499">form feed</span></span>|<span data-ttu-id="630d1-500">U + 000C</span><span class="sxs-lookup"><span data-stu-id="630d1-500">U+000C</span></span>|  
|\n|<span data-ttu-id="630d1-501">avanzamento riga</span><span class="sxs-lookup"><span data-stu-id="630d1-501">line feed</span></span>|<span data-ttu-id="630d1-502">U + 000A</span><span class="sxs-lookup"><span data-stu-id="630d1-502">U+000A</span></span>|  
|<span data-ttu-id="630d1-503">\r</span><span class="sxs-lookup"><span data-stu-id="630d1-503">\r</span></span>|<span data-ttu-id="630d1-504">ritorno a capo</span><span class="sxs-lookup"><span data-stu-id="630d1-504">carriage return</span></span>|<span data-ttu-id="630d1-505">U + 000D</span><span class="sxs-lookup"><span data-stu-id="630d1-505">U+000D</span></span>|  
|<span data-ttu-id="630d1-506">\t</span><span class="sxs-lookup"><span data-stu-id="630d1-506">\t</span></span>|<span data-ttu-id="630d1-507">TAB</span><span class="sxs-lookup"><span data-stu-id="630d1-507">tab</span></span>|<span data-ttu-id="630d1-508">U + 0009</span><span class="sxs-lookup"><span data-stu-id="630d1-508">U+0009</span></span>|  
|<span data-ttu-id="630d1-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="630d1-509">\uXXXX</span></span>|<span data-ttu-id="630d1-510">Carattere Unicode definito da 4 cifre esadecimali.</span><span class="sxs-lookup"><span data-stu-id="630d1-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="630d1-511">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="630d1-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="630d1-512"><a name="bk_query_perf_guidelines"></a> Linee guida sulle prestazioni delle query</span><span class="sxs-lookup"><span data-stu-id="630d1-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="630d1-513">Affinché un toobe query eseguita in modo efficiente per una raccolta di grandi dimensioni, è opportuno usare filtri gestibili tramite uno o più indici.</span><span class="sxs-lookup"><span data-stu-id="630d1-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="630d1-514">Hello seguendo i filtri verrà considerato per la ricerca nell'indice:</span><span class="sxs-lookup"><span data-stu-id="630d1-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="630d1-515">Usare l'operatore di uguaglianza (=) con un'espressione percorso documenti e una costante.</span><span class="sxs-lookup"><span data-stu-id="630d1-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="630d1-516">Usare gli operatori di intervallo (<, \<=, >, >=) con un'espressione percorso documenti e costanti numeriche.</span><span class="sxs-lookup"><span data-stu-id="630d1-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="630d1-517">Espressione di percorso del documento è l'acronimo di un'espressione che identifica un percorso di costante nei documenti di hello dalla raccolta di database a cui fa riferimento hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="630d1-518">**Espressione percorso documenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="630d1-519">Le espressioni percorso documenti sono espressioni usate in un percorso di funzioni di valutazione dell'indicizzatore proprietà o matrice per un documento proveniente da documenti di una raccolta di database.</span><span class="sxs-lookup"><span data-stu-id="630d1-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="630d1-520">Questo può essere utilizzato tooidentify hello percorso di valori a cui fa riferimento in un filtro direttamente all'interno dei documenti hello nella raccolta di database hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="630d1-521">Per un'espressione toobe considerata un'espressione di percorso del documento, è necessario:</span><span class="sxs-lookup"><span data-stu-id="630d1-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="630d1-522">Riferimento hello raccolta radice direttamente.</span><span class="sxs-lookup"><span data-stu-id="630d1-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="630d1-523">Faccia riferimento all'indicizzatore di proprietà o matrici costanti di un'espressione percorso documenti</span><span class="sxs-lookup"><span data-stu-id="630d1-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="630d1-524">Faccia riferimento a un alias che rappresenta un'espressione percorso documenti.</span><span class="sxs-lookup"><span data-stu-id="630d1-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="630d1-525">**Convenzioni della sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="630d1-526">Hello nella tabella seguente descrive la sintassi di toodescribe hello convenzioni utilizzate in riferimenti al linguaggio di Query API DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="630d1-527">**Convenzione**</span><span class="sxs-lookup"><span data-stu-id="630d1-527">**Convention**</span></span>|<span data-ttu-id="630d1-528">**Usata per**</span><span class="sxs-lookup"><span data-stu-id="630d1-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="630d1-529">LETTERE MAIUSCOLE</span><span class="sxs-lookup"><span data-stu-id="630d1-529">UPPERCASE</span></span>|<span data-ttu-id="630d1-530">Parole chiave che non fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="630d1-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="630d1-531">lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="630d1-531">lowercase</span></span>|<span data-ttu-id="630d1-532">Parole chiave che fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="630d1-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="630d1-533">\<non terminale></span><span class="sxs-lookup"><span data-stu-id="630d1-533">\<nonterminal></span></span>|<span data-ttu-id="630d1-534">Non terminale, definito separatamente.</span><span class="sxs-lookup"><span data-stu-id="630d1-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="630d1-535">\<non terminale> ::=</span><span class="sxs-lookup"><span data-stu-id="630d1-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="630d1-536">Definizione della sintassi di non terminale hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="630d1-537">altro_terminale</span><span class="sxs-lookup"><span data-stu-id="630d1-537">other_terminal</span></span>|<span data-ttu-id="630d1-538">Terminale (token), descritto dettagliatamente con parole.</span><span class="sxs-lookup"><span data-stu-id="630d1-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="630d1-539">identificatore</span><span class="sxs-lookup"><span data-stu-id="630d1-539">identifier</span></span>|<span data-ttu-id="630d1-540">Identificatore.</span><span class="sxs-lookup"><span data-stu-id="630d1-540">Identifier.</span></span> <span data-ttu-id="630d1-541">Consente solo i seguenti caratteri: a-z A-Z 0-9 _Il primo carattere non può essere una cifra.</span><span class="sxs-lookup"><span data-stu-id="630d1-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="630d1-542">"stringa"</span><span class="sxs-lookup"><span data-stu-id="630d1-542">"string"</span></span>|<span data-ttu-id="630d1-543">Stringa tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="630d1-543">Quoted string.</span></span> <span data-ttu-id="630d1-544">Consente qualsiasi stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-544">Allows any valid string.</span></span> <span data-ttu-id="630d1-545">Vedere la descrizione di string_literal.</span><span class="sxs-lookup"><span data-stu-id="630d1-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="630d1-546">'simbolo'</span><span class="sxs-lookup"><span data-stu-id="630d1-546">'symbol'</span></span>|<span data-ttu-id="630d1-547">Simbolo letterale che fa parte della sintassi hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="630d1-548">&#124; (barra verticale)</span><span class="sxs-lookup"><span data-stu-id="630d1-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="630d1-549">Alternative per gli elementi di sintassi.</span><span class="sxs-lookup"><span data-stu-id="630d1-549">Alternatives for syntax items.</span></span> <span data-ttu-id="630d1-550">È possibile utilizzare solo uno degli elementi di hello specificati.</span><span class="sxs-lookup"><span data-stu-id="630d1-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="630d1-551">[ ] /(parentesi quadre)</span><span class="sxs-lookup"><span data-stu-id="630d1-551">[ ] /(brackets)</span></span>|<span data-ttu-id="630d1-552">Le parentesi quadre racchiudono uno o più elementi facoltativi.</span><span class="sxs-lookup"><span data-stu-id="630d1-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="630d1-553">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="630d1-553">[ ,...n ]</span></span>|<span data-ttu-id="630d1-554">Indica hello precedente elemento può essere ripetuto n volte.</span><span class="sxs-lookup"><span data-stu-id="630d1-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="630d1-555">Hello occorrenze sono separate da virgole.</span><span class="sxs-lookup"><span data-stu-id="630d1-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="630d1-556">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="630d1-556">[ ...n ]</span></span>|<span data-ttu-id="630d1-557">Indica hello precedente elemento può essere ripetuto n volte.</span><span class="sxs-lookup"><span data-stu-id="630d1-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="630d1-558">Hello occorrenze sono separate da spazi.</span><span class="sxs-lookup"><span data-stu-id="630d1-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="630d1-559"><a name="bk_built_in_functions"></a> Funzioni predefinite</span><span class="sxs-lookup"><span data-stu-id="630d1-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="630d1-560">In Azure Cosmos DB sono disponibili molte funzioni SQL predefinite.</span><span class="sxs-lookup"><span data-stu-id="630d1-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="630d1-561">categorie di Hello delle funzioni predefinite sono elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="630d1-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="630d1-562">Funzione</span><span class="sxs-lookup"><span data-stu-id="630d1-562">Function</span></span>|<span data-ttu-id="630d1-563">Descrizione</span><span class="sxs-lookup"><span data-stu-id="630d1-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="630d1-564">Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="630d1-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="630d1-565">Hello funzioni matematiche eseguono un calcolo basato in genere su valori di input forniti come argomenti e restituiscono un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="630d1-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="630d1-566">Funzioni di controllo del tipo</span><span class="sxs-lookup"><span data-stu-id="630d1-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="630d1-567">funzioni di controllo di tipo Hello consentono di tipo hello toocheck di un'espressione all'interno di query SQL.</span><span class="sxs-lookup"><span data-stu-id="630d1-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="630d1-568">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="630d1-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="630d1-569">funzioni stringa Hello eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="630d1-570">Funzioni di matrice</span><span class="sxs-lookup"><span data-stu-id="630d1-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="630d1-571">funzioni di matrice Hello eseguono un'operazione su un valore di input di matrice e restituito numerico, un valore booleano o di matrice.</span><span class="sxs-lookup"><span data-stu-id="630d1-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="630d1-572">Funzioni spaziali</span><span class="sxs-lookup"><span data-stu-id="630d1-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="630d1-573">le funzioni spaziali Hello eseguono un'operazione su un valore di oggetto spaziale input e restituiscono un valore numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="630d1-574"><a name="bk_mathematical_functions"></a> Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="630d1-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="630d1-575">Hello ognuna delle funzioni seguenti esegue un calcolo basato in genere su valori di input forniti come argomenti e restituiscono un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="630d1-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="630d1-576">ABS</span><span class="sxs-lookup"><span data-stu-id="630d1-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="630d1-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="630d1-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="630d1-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="630d1-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="630d1-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="630d1-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="630d1-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="630d1-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="630d1-581">CEILING</span><span class="sxs-lookup"><span data-stu-id="630d1-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="630d1-582">COS</span><span class="sxs-lookup"><span data-stu-id="630d1-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="630d1-583">COT</span><span class="sxs-lookup"><span data-stu-id="630d1-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="630d1-584">DEGREES</span><span class="sxs-lookup"><span data-stu-id="630d1-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="630d1-585">EXP</span><span class="sxs-lookup"><span data-stu-id="630d1-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="630d1-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="630d1-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="630d1-587">LOG</span><span class="sxs-lookup"><span data-stu-id="630d1-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="630d1-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="630d1-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="630d1-589">PI</span><span class="sxs-lookup"><span data-stu-id="630d1-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="630d1-590">POWER</span><span class="sxs-lookup"><span data-stu-id="630d1-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="630d1-591">RADIANS</span><span class="sxs-lookup"><span data-stu-id="630d1-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="630d1-592">ROUND</span><span class="sxs-lookup"><span data-stu-id="630d1-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="630d1-593">SIN</span><span class="sxs-lookup"><span data-stu-id="630d1-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="630d1-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="630d1-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="630d1-595">SQUARE</span><span class="sxs-lookup"><span data-stu-id="630d1-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="630d1-596">SIGN</span><span class="sxs-lookup"><span data-stu-id="630d1-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="630d1-597">TAN</span><span class="sxs-lookup"><span data-stu-id="630d1-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="630d1-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="630d1-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="630d1-599"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="630d1-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="630d1-600">Restituisce hello assoluto (positivo) il valore di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-601">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-602">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-603">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-604">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-604">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-605">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-606">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-606">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-607">Hello riportato di seguito risultati hello dell'utilizzo della funzione hello ABS su tre numeri diversi.</span><span class="sxs-lookup"><span data-stu-id="630d1-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="630d1-608">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="630d1-609"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="630d1-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="630d1-610">Angolo di hello restituisce, in radianti, il cui coseno è hello espressione numerica specificata; denominato anche arcocoseno.</span><span class="sxs-lookup"><span data-stu-id="630d1-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="630d1-611">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-612">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-613">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-614">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-614">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-615">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-616">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-616">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-617">Hello esempio seguente restituisce hello Arcocoseno di -1.</span><span class="sxs-lookup"><span data-stu-id="630d1-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="630d1-618">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="630d1-619"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="630d1-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="630d1-620">Angolo di hello restituisce, in radianti, il cui seno è hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="630d1-621">Detta anche arcoseno.</span><span class="sxs-lookup"><span data-stu-id="630d1-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="630d1-622">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-623">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-624">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-625">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-625">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-626">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-627">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-627">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-628">Hello esempio seguente restituisce hello ARCOSENO di -1.</span><span class="sxs-lookup"><span data-stu-id="630d1-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="630d1-629">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="630d1-630"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="630d1-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="630d1-631">Angolo di hello restituisce, in radianti, la cui tangente è hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="630d1-632">Detta anche arcotangente.</span><span class="sxs-lookup"><span data-stu-id="630d1-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="630d1-633">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-634">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-635">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-636">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-636">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-637">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-638">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-638">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-639">Hello esempio restituisce hello ATAN di hello seguente valore specificato.</span><span class="sxs-lookup"><span data-stu-id="630d1-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="630d1-640">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="630d1-641"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="630d1-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="630d1-642">Restituisce hello valore principale di hello arcotangente di y / x, espresso in radianti.</span><span class="sxs-lookup"><span data-stu-id="630d1-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="630d1-643">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-644">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-645">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-646">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-646">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-647">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-648">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-648">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-649">esempio Hello calcola hello ATN2 per hello specificato x e y componenti.</span><span class="sxs-lookup"><span data-stu-id="630d1-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="630d1-650">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="630d1-651"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="630d1-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="630d1-652">Restituisce hello più piccolo valore integer maggiore di o uguale a, hello espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="630d1-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-653">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-654">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-655">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-656">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-656">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-657">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-658">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-658">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-659">Hello di esempio seguente mostra i numeri positivi, negativi e valori zero con hello funzione CEILING.</span><span class="sxs-lookup"><span data-stu-id="630d1-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="630d1-660">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="630d1-661"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="630d1-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="630d1-662">Restituisce hello coseno trigonometrico hello specificato angolo, espresso in radianti, in hello espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="630d1-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="630d1-663">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-664">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-665">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-666">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-666">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-667">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-668">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-668">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-669">Hello di esempio seguente calcola hello CO di hello specificato angolo.</span><span class="sxs-lookup"><span data-stu-id="630d1-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="630d1-670">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="630d1-671"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="630d1-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="630d1-672">Restituisce hello cotangente trigonometrica hello specificato angolo, espresso in radianti, in hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-673">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-674">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-675">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-676">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-676">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-677">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-678">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-678">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-679">Hello di esempio seguente calcola hello COTANGENTE dell'angolo specificato hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="630d1-680">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="630d1-681"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="630d1-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="630d1-682">Restituisce hello angolo corrispondente in gradi di un angolo specificato espresso in radianti.</span><span class="sxs-lookup"><span data-stu-id="630d1-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="630d1-683">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-684">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-685">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-686">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-686">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-687">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-688">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-688">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-689">Hello esempio seguente restituisce hello numero di gradi di un angolo di PI/2 radianti.</span><span class="sxs-lookup"><span data-stu-id="630d1-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="630d1-690">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="630d1-691"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="630d1-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="630d1-692">Restituisce l'intero più grande hello minore o uguale toohello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-693">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-694">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-695">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-696">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-696">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-697">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-698">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-698">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-699">Hello di esempio seguente mostra i numeri positivi, negativi e valori zero con hello FLOOR (funzione).</span><span class="sxs-lookup"><span data-stu-id="630d1-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="630d1-700">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="630d1-701"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="630d1-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="630d1-702">Hello restituisce il valore esponenziale di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-703">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-704">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-705">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-706">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-706">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-707">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-708">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-708">**Remarks**</span></span>  
  
 <span data-ttu-id="630d1-709">costante Hello **e** (2.718281 …) è hello base dei logaritmi naturali.</span><span class="sxs-lookup"><span data-stu-id="630d1-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="630d1-710">esponente di un numero Hello è hello costante **e** generato toohello potenza del numero di hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="630d1-711">Ad esempio, EXP(1.0) = e^1.0 = 2,71828182845905 e EXP(10) = e^10 = 22026,4657948067.</span><span class="sxs-lookup"><span data-stu-id="630d1-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="630d1-712">Hello esponenziale del logaritmo naturale di hello di un numero è il numero hello stesso: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="630d1-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="630d1-713">E hello del logaritmo naturale di hello esponenziale di un numero è il numero hello stesso: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="630d1-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="630d1-714">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-714">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-715">Hello esempio seguente dichiara una variabile e restituisce hello valore esponenziale della variabile specificata hello (10).</span><span class="sxs-lookup"><span data-stu-id="630d1-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="630d1-716">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="630d1-717">Hello esempio seguente restituisce hello valore esponenziale del logaritmo naturale di hello 20 e il logaritmo naturale hello di hello esponenziale di 20.</span><span class="sxs-lookup"><span data-stu-id="630d1-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="630d1-718">Poiché queste funzioni sono inverse una da altra, il valore restituito di hello con arrotondamento matematico in entrambi i casi è 20 virgola mobile.</span><span class="sxs-lookup"><span data-stu-id="630d1-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="630d1-719">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="630d1-720"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="630d1-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="630d1-721">Logaritmo naturale di hello restituisce di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-722">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="630d1-723">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-724">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="630d1-725">Argomento numerico facoltativo che imposta la base logaritmo hello hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="630d1-726">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-726">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-727">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-728">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-728">**Remarks**</span></span>  
  
 <span data-ttu-id="630d1-729">Per impostazione predefinita, log () restituisce logaritmo naturale di hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="630d1-730">È possibile modificare base hello hello logaritmo tooanother valore con parametri di base facoltativo hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="630d1-731">Logaritmo naturale di Hello è hello logaritmo toohello base **e**, dove **e** è un too2.718281828 approssimativamente costante non razionale.</span><span class="sxs-lookup"><span data-stu-id="630d1-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="630d1-732">Logaritmo naturale di Hello di hello esponenziale di un numero è numero hello stesso: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="630d1-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="630d1-733">E hello esponenziale del logaritmo naturale di hello di un numero è il numero hello stesso: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="630d1-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="630d1-734">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-734">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-735">Hello esempio seguente viene dichiarata una variabile e restituisce hello logaritmo valore della variabile specificata hello (10).</span><span class="sxs-lookup"><span data-stu-id="630d1-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="630d1-736">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="630d1-737">Hello esempio seguente calcola hello LOG per l'esponente hello di un numero.</span><span class="sxs-lookup"><span data-stu-id="630d1-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="630d1-738">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="630d1-739"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="630d1-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="630d1-740">Logaritmo in base 10 di hello restituisce hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-741">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-742">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-743">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-744">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-744">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-745">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-746">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="630d1-746">**Remarks**</span></span>  
  
 <span data-ttu-id="630d1-747">Hello LOG10 e funzioni POWER sono inversamente correlate tooone un altro.</span><span class="sxs-lookup"><span data-stu-id="630d1-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="630d1-748">Ad esempio, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="630d1-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="630d1-749">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-749">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-750">Hello esempio seguente viene dichiarata una variabile e restituisce il valore LOG10 hello della variabile specificata hello (100).</span><span class="sxs-lookup"><span data-stu-id="630d1-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="630d1-751">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="630d1-752"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="630d1-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="630d1-753">Restituisce hello valore costante di pi greco.</span><span class="sxs-lookup"><span data-stu-id="630d1-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="630d1-754">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="630d1-755">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-756">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-757">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-757">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-758">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-759">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-759">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-760">Hello esempio seguente restituisce il valore di hello di pi greco.</span><span class="sxs-lookup"><span data-stu-id="630d1-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="630d1-761">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="630d1-762"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="630d1-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="630d1-763">Valore di hello specificato di hello restituisce espressione toohello potenza specificata.</span><span class="sxs-lookup"><span data-stu-id="630d1-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="630d1-764">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="630d1-765">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-766">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="630d1-767">È hello power toowhich tooraise `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="630d1-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="630d1-768">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-768">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-769">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-770">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-770">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-771">Hello di esempio seguente viene illustrata la generazione di un numero toohello potenza 3 (cubo hello del numero di hello).</span><span class="sxs-lookup"><span data-stu-id="630d1-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="630d1-772">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="630d1-773"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="630d1-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="630d1-774">Restituisce radianti quando viene immessa un'espressione numerica, espresso in gradi.</span><span class="sxs-lookup"><span data-stu-id="630d1-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="630d1-775">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-776">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-777">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-778">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-778">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-779">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-780">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-780">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-781">Hello esempio seguente accetta alcuni angoli come input e restituisce i relativi valori in radianti.</span><span class="sxs-lookup"><span data-stu-id="630d1-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="630d1-782">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="630d1-783"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="630d1-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="630d1-784">Restituisce un valore numerico, il valore intero più vicino di toohello arrotondato.</span><span class="sxs-lookup"><span data-stu-id="630d1-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="630d1-785">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-786">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-787">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-788">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-788">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-789">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-790">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-790">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-791">Hello seguente Arrotonda hello dopo i numeri positivi e negativi toohello numero intero più vicino.</span><span class="sxs-lookup"><span data-stu-id="630d1-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="630d1-792">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="630d1-793"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="630d1-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="630d1-794">Restituisce hello positivo (+ 1), zero (0) o negativo (-1) segno di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-795">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-796">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-797">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-798">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-798">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-799">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-800">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-800">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-801">Hello esempio seguente restituisce valori di hello SIGN dei numeri da-2 too2.</span><span class="sxs-lookup"><span data-stu-id="630d1-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="630d1-802">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="630d1-803"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="630d1-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="630d1-804">Restituisce hello seno trigonometrico hello specificato angolo, espresso in radianti, in hello espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="630d1-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="630d1-805">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-806">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-807">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-808">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-808">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-809">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-810">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-810">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-811">Hello di esempio seguente calcola hello seno dell'angolo specificato hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="630d1-812">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="630d1-813"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="630d1-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="630d1-814">Radice quadrata di hello restituisce di hello specificato valore numerico.</span><span class="sxs-lookup"><span data-stu-id="630d1-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="630d1-815">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-816">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-817">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-818">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-818">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-819">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-820">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-820">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-821">Hello esempio seguente restituisce hello di radici quadrate dei numeri da 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="630d1-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="630d1-822">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="630d1-823"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="630d1-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="630d1-824">Hello restituisce quadrato di hello specificato valore numerico.</span><span class="sxs-lookup"><span data-stu-id="630d1-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="630d1-825">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-826">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-827">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-828">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-828">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-829">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-830">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-830">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-831">Hello esempio seguente restituisce i quadrati hello di numeri da 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="630d1-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="630d1-832">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="630d1-833"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="630d1-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="630d1-834">Tangente di hello restituisce di hello specificato angolo, espresso in radianti, in hello espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="630d1-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="630d1-835">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-836">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-837">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-838">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-838">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-839">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-840">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-840">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-841">esempio Hello calcola hello tangente di PI () / 2.</span><span class="sxs-lookup"><span data-stu-id="630d1-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="630d1-842">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="630d1-843"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="630d1-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="630d1-844">Restituisce un valore numerico, il valore intero più vicino di toohello troncato.</span><span class="sxs-lookup"><span data-stu-id="630d1-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="630d1-845">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="630d1-846">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="630d1-847">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-848">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-848">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-849">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-850">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-850">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-851">Hello di esempio seguente tronca hello seguente toohello numeri positivi e negativi più vicino valore integer.</span><span class="sxs-lookup"><span data-stu-id="630d1-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="630d1-852">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="630d1-853"><a name="bk_type_checking_functions"></a> Funzioni di controllo del tipo</span><span class="sxs-lookup"><span data-stu-id="630d1-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="630d1-854">funzioni seguenti Hello supportano controllo in base a valori di input del tipo, ogni funzione restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="630d1-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="630d1-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="630d1-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="630d1-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="630d1-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="630d1-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="630d1-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="630d1-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="630d1-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="630d1-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="630d1-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="630d1-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="630d1-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="630d1-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="630d1-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="630d1-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="630d1-863"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="630d1-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="630d1-864">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è una matrice.</span><span class="sxs-lookup"><span data-stu-id="630d1-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="630d1-865">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="630d1-866">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="630d1-867">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-868">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-868">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-869">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-870">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-870">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-871">Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando la funzione IS_ARRAY hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="630d1-872">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="630d1-873"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="630d1-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="630d1-874">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="630d1-875">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="630d1-876">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="630d1-877">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-878">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-878">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-879">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-880">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-880">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-881">Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando hello funzione IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="630d1-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="630d1-882">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="630d1-883"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="630d1-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="630d1-884">Restituisce un valore booleano che indica se la proprietà hello è stata assegnata un valore.</span><span class="sxs-lookup"><span data-stu-id="630d1-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="630d1-885">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="630d1-886">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="630d1-887">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-888">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-888">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-889">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-890">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-890">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-891">Hello seguente esempio viene controllato per la presenza di hello di una proprietà all'interno di hello specificato documento JSON.</span><span class="sxs-lookup"><span data-stu-id="630d1-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="630d1-892">Hello primo risultato è true perché "a" è presente, ma hello secondo restituisce false perché "b" è assente.</span><span class="sxs-lookup"><span data-stu-id="630d1-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="630d1-893">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="630d1-894"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="630d1-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="630d1-895">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è null.</span><span class="sxs-lookup"><span data-stu-id="630d1-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="630d1-896">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="630d1-897">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="630d1-898">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-899">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-899">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-900">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-901">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-901">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-902">Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando la funzione IS_NULL hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="630d1-903">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="630d1-904"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="630d1-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="630d1-905">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un numero.</span><span class="sxs-lookup"><span data-stu-id="630d1-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="630d1-906">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="630d1-907">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="630d1-908">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-909">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-909">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-910">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-911">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-911">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-912">Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando la funzione IS_NULL hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="630d1-913">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="630d1-914"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="630d1-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="630d1-915">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="630d1-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="630d1-916">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="630d1-917">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="630d1-918">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-919">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-919">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-920">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-921">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-921">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-922">Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando la funzione IS_OBJECT hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="630d1-923">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="630d1-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="630d1-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="630d1-925">Restituisce un valore booleano che indica se il tipo di hello di hello specificato espressione è una primitiva (stringa, booleano, numerico o null).</span><span class="sxs-lookup"><span data-stu-id="630d1-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="630d1-926">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="630d1-927">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="630d1-928">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-929">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-929">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-930">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-931">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-931">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-932">Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando hello funzione IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="630d1-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="630d1-933">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="630d1-934"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="630d1-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="630d1-935">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è una stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="630d1-936">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="630d1-937">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="630d1-938">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-939">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-939">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-940">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-941">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-941">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-942">Hello esempio seguente verifica oggetti di booleano JSON, numero, stringa, null, oggetto, matrice e tipi non definiti usando hello funzione IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="630d1-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="630d1-943">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="630d1-944"><a name="bk_string_functions"></a> Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="630d1-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="630d1-945">Hello funzioni scalari seguenti eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="630d1-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="630d1-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="630d1-947">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="630d1-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="630d1-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="630d1-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="630d1-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="630d1-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="630d1-950">LEFT</span><span class="sxs-lookup"><span data-stu-id="630d1-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="630d1-951">LENGTH</span><span class="sxs-lookup"><span data-stu-id="630d1-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="630d1-952">LOWER</span><span class="sxs-lookup"><span data-stu-id="630d1-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="630d1-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="630d1-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="630d1-954">REPLACE</span><span class="sxs-lookup"><span data-stu-id="630d1-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="630d1-955">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="630d1-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="630d1-956">REVERSE</span><span class="sxs-lookup"><span data-stu-id="630d1-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="630d1-957">RIGHT</span><span class="sxs-lookup"><span data-stu-id="630d1-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="630d1-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="630d1-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="630d1-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="630d1-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="630d1-960">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="630d1-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="630d1-961">UPPER</span><span class="sxs-lookup"><span data-stu-id="630d1-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="630d1-962"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="630d1-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="630d1-963">Restituisce una stringa che rappresenta il risultato di hello del concatenamento di due o più valori di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="630d1-964">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="630d1-965">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-966">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-967">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-967">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-968">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-969">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-969">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-970">Hello seguente esempio restituisce la stringa hello concatenato di hello valori specificati.</span><span class="sxs-lookup"><span data-stu-id="630d1-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="630d1-971">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="630d1-972"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="630d1-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="630d1-973">Restituisce un valore booleano che indica se prima espressione di stringa hello contiene hello secondo.</span><span class="sxs-lookup"><span data-stu-id="630d1-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="630d1-974">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="630d1-975">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-976">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-977">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-977">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-978">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-979">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-979">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-980">Hello esempio seguente viene controllato se "abc" contiene "ab" e che contiene "d".</span><span class="sxs-lookup"><span data-stu-id="630d1-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="630d1-981">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="630d1-982"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="630d1-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="630d1-983">Restituisce un valore booleano che indica se prima espressione di stringa hello termina con hello secondo.</span><span class="sxs-lookup"><span data-stu-id="630d1-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="630d1-984">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="630d1-985">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-986">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-987">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-987">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-988">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-989">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-989">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-990">Hello esempio seguente restituisce hello "abc" termina con "b" e "bc".</span><span class="sxs-lookup"><span data-stu-id="630d1-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="630d1-991">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="630d1-992"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="630d1-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="630d1-993">Restituisce hello a partire dalla posizione della prima occorrenza di hello della seconda espressione stringa hello all'hello prima espressione stringa specificata oppure -1 se la stringa hello non viene trovata.</span><span class="sxs-lookup"><span data-stu-id="630d1-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="630d1-994">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="630d1-995">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-996">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-997">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-997">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-998">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-999">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-999">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1000">Hello esempio seguente viene restituito indice hello di diverse sottostringhe all'interno di "abc".</span><span class="sxs-lookup"><span data-stu-id="630d1-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="630d1-1001">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="630d1-1002"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="630d1-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="630d1-1003">Restituisce la parte sinistra di una stringa di hello con hello specificato numero di caratteri.</span><span class="sxs-lookup"><span data-stu-id="630d1-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="630d1-1004">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="630d1-1005">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1006">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="630d1-1007">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-1008">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1009">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1010">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1010">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1011">Hello esempio seguente restituisce hello parte di "abc" per diversi valori di lunghezza a sinistra.</span><span class="sxs-lookup"><span data-stu-id="630d1-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="630d1-1012">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="630d1-1013"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="630d1-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="630d1-1014">Restituisce il numero di caratteri di hello hello specificato espressione stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="630d1-1015">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="630d1-1016">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1017">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-1018">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1019">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1020">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1020">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1021">Hello esempio seguente restituisce una stringa di lunghezza hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="630d1-1022">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="630d1-1023"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="630d1-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="630d1-1024">Restituisce un'espressione stringa dopo aver convertito i caratteri maiuscoli in caratteri toolowercase di dati.</span><span class="sxs-lookup"><span data-stu-id="630d1-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="630d1-1025">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="630d1-1026">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1027">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-1028">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1029">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1030">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1030">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1031">Hello seguente esempio viene illustrato come toouse inferiore in una query.</span><span class="sxs-lookup"><span data-stu-id="630d1-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="630d1-1032">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="630d1-1033"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="630d1-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="630d1-1034">Restituisce un'espressione stringa dopo aver rimosso gli spazi vuoti iniziali.</span><span class="sxs-lookup"><span data-stu-id="630d1-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="630d1-1035">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="630d1-1036">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1037">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-1038">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1039">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1040">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1040">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1041">Hello seguente esempio viene illustrato come toouse LTRIM all'interno di una query.</span><span class="sxs-lookup"><span data-stu-id="630d1-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="630d1-1042">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="630d1-1043"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="630d1-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="630d1-1044">Sostituisce tutte le occorrenze di un valore stringa specificato con un altro valore stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="630d1-1045">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="630d1-1046">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1047">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-1048">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1049">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1050">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1050">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1051">Hello di esempio seguente viene illustrato come toouse SOSTITUISCONO in una query.</span><span class="sxs-lookup"><span data-stu-id="630d1-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="630d1-1052">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="630d1-1053"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="630d1-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="630d1-1054">Ripete un valore stringa in un numero di volte specificato.</span><span class="sxs-lookup"><span data-stu-id="630d1-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="630d1-1055">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="630d1-1056">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1057">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="630d1-1058">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-1059">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1060">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1061">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1061">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1062">Hello di esempio seguente viene illustrato come eseguire la replica toouse in una query.</span><span class="sxs-lookup"><span data-stu-id="630d1-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="630d1-1063">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="630d1-1064"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="630d1-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="630d1-1065">Restituisce l'inverso di hello di un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="630d1-1066">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="630d1-1067">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1068">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-1069">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1070">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1071">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1071">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1072">Hello di esempio seguente viene illustrato come toouse inversa in una query.</span><span class="sxs-lookup"><span data-stu-id="630d1-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="630d1-1073">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="630d1-1074"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="630d1-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="630d1-1075">Hello restituisce parte destra di una stringa con hello numero specificato di caratteri.</span><span class="sxs-lookup"><span data-stu-id="630d1-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="630d1-1076">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="630d1-1077">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1078">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="630d1-1079">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-1080">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1081">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1082">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1082">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1083">Hello esempio seguente restituisce hello parte destra di "abc" per diversi valori di lunghezza.</span><span class="sxs-lookup"><span data-stu-id="630d1-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="630d1-1084">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="630d1-1085"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="630d1-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="630d1-1086">Restituisce un'espressione di stringa dopo aver rimosso gli spazi vuoti finali.</span><span class="sxs-lookup"><span data-stu-id="630d1-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="630d1-1087">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="630d1-1088">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1089">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-1090">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1091">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1092">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1092">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1093">Hello seguente esempio viene illustrato come toouse RTRIM all'interno di una query.</span><span class="sxs-lookup"><span data-stu-id="630d1-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="630d1-1094">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="630d1-1095"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="630d1-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="630d1-1096">Restituisce un valore booleano che indica se prima espressione di stringa hello inizia con hello secondo.</span><span class="sxs-lookup"><span data-stu-id="630d1-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="630d1-1097">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="630d1-1098">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1099">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-1100">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1101">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-1102">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1102">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1103">Hello seguente controlla se hello stringa "abc" inizia con "b" e "a".</span><span class="sxs-lookup"><span data-stu-id="630d1-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="630d1-1104">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="630d1-1105"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="630d1-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="630d1-1106">Restituisce parte di un'espressione stringa a partire da hello posizione in base zero del carattere specificata e continua toohello specificato, lunghezza o alla fine di toohello della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="630d1-1107">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="630d1-1108">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1109">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="630d1-1110">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-1111">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1112">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1113">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1113">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1114">Hello esempio seguente restituisce la sottostringa hello di "abc" a partire da 1 e una lunghezza di 1 carattere.</span><span class="sxs-lookup"><span data-stu-id="630d1-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="630d1-1115">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="630d1-1116"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="630d1-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="630d1-1117">Restituisce un'espressione stringa dopo la conversione toouppercase di dati carattere minuscolo.</span><span class="sxs-lookup"><span data-stu-id="630d1-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="630d1-1118">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="630d1-1119">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="630d1-1120">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="630d1-1121">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1122">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="630d1-1123">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1123">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1124">Hello seguente esempio viene illustrato come toouse superiore in una query</span><span class="sxs-lookup"><span data-stu-id="630d1-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="630d1-1125">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="630d1-1126"><a name="bk_array_functions"></a> Funzioni di matrice</span><span class="sxs-lookup"><span data-stu-id="630d1-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="630d1-1127">Hello funzioni scalari seguenti esegue un'operazione su un valore di input di matrice e restituito numerico, valore booleano o di matrice</span><span class="sxs-lookup"><span data-stu-id="630d1-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="630d1-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="630d1-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="630d1-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="630d1-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="630d1-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="630d1-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="630d1-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="630d1-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="630d1-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="630d1-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="630d1-1133">Restituisce una matrice che rappresenta il risultato di hello della concatenazione di due o più valori della matrice.</span><span class="sxs-lookup"><span data-stu-id="630d1-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="630d1-1134">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="630d1-1135">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="630d1-1136">È qualsiasi espressione di matrice valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="630d1-1137">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1138">Restituisce un'espressione di matrice.</span><span class="sxs-lookup"><span data-stu-id="630d1-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="630d1-1139">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1139">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1140">Hello seguente esempio come tooconcatenate due matrici.</span><span class="sxs-lookup"><span data-stu-id="630d1-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="630d1-1141">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="630d1-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="630d1-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="630d1-1143">Restituisce un valore booleano che indica se la matrice hello contiene hello valore specificato.</span><span class="sxs-lookup"><span data-stu-id="630d1-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="630d1-1144">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="630d1-1145">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="630d1-1146">È qualsiasi espressione di matrice valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="630d1-1147">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="630d1-1148">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1149">Restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="630d1-1150">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1150">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1151">Hello seguente come esempio toocheck per l'appartenenza a una matrice tramite ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="630d1-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="630d1-1152">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="630d1-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="630d1-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="630d1-1154">Restituisce il numero di elementi di hello hello specificata espressione di matrice.</span><span class="sxs-lookup"><span data-stu-id="630d1-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="630d1-1155">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="630d1-1156">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="630d1-1157">È qualsiasi espressione di matrice valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="630d1-1158">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1159">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="630d1-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-1160">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1160">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1161">Hello seguente esempio come tooget hello lunghezza di una matrice tramite ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="630d1-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="630d1-1162">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="630d1-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="630d1-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="630d1-1164">Restituisce parte di un'espressione di matrice.</span><span class="sxs-lookup"><span data-stu-id="630d1-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="630d1-1165">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="630d1-1166">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="630d1-1167">È qualsiasi espressione di matrice valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="630d1-1168">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="630d1-1169">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1170">Restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="630d1-1171">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1171">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1172">Hello seguente come esempio tooget una parte di una matrice tramite ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="630d1-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="630d1-1173">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="630d1-1174"><a name="bk_spatial_functions"></a> Funzioni spaziali</span><span class="sxs-lookup"><span data-stu-id="630d1-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="630d1-1175">Hello funzioni scalari seguenti eseguono un'operazione su un valore di oggetto spaziale input e restituiscono un valore numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="630d1-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="630d1-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="630d1-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="630d1-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="630d1-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="630d1-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="630d1-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="630d1-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="630d1-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="630d1-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="630d1-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="630d1-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="630d1-1182">Restituisce la distanza hello tra espressioni di hello due LineString, Polygon o punto GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="630d1-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="630d1-1183">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="630d1-1184">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="630d1-1185">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="630d1-1186">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1187">Restituisce un'espressione numerica che contiene la distanza hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="630d1-1188">Questo è espresso in metri per il sistema di riferimento predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="630d1-1189">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1189">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1190">Hello seguente esempio viene illustrato come tooreturn tutti i documenti della famiglia entro 30 chilometri di hello specificato percorso funzione hello ST_DISTANCE incorporato.</span><span class="sxs-lookup"><span data-stu-id="630d1-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="630d1-1191">.</span><span class="sxs-lookup"><span data-stu-id="630d1-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="630d1-1192">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="630d1-1193"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="630d1-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="630d1-1194">Restituisce un'espressione booleana che indica se hello GeoJSON l'oggetto (punto, poligono o LineString) specificato nel primo argomento hello è all'interno di hello GeoJSON (punto, poligono o LineString) nel secondo argomento hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="630d1-1195">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="630d1-1196">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="630d1-1197">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="630d1-1198">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="630d1-1199">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1200">Restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="630d1-1201">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1201">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1202">Hello di esempio seguente viene illustrato come toofind famiglia tutti i documenti all'interno di un poligono utilizzando ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="630d1-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="630d1-1203">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="630d1-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="630d1-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="630d1-1205">Restituisce un'espressione booleana che indica se hello GeoJSON l'oggetto (punto, poligono o LineString) specificato nel primo argomento hello interseca hello GeoJSON (punto, poligono o LineString) nel secondo argomento hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="630d1-1206">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="630d1-1207">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="630d1-1208">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="630d1-1209">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="630d1-1210">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1211">Restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="630d1-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="630d1-1212">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1212">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1213">Hello seguente esempio viene illustrato come toofind tutte le aree che si interseca con hello dato poligono.</span><span class="sxs-lookup"><span data-stu-id="630d1-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="630d1-1214">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="630d1-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="630d1-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="630d1-1216">Restituisce un valore booleano che indica se hello LineString, Polygon o punto GeoJSON espressione è valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="630d1-1217">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="630d1-1218">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="630d1-1219">È qualsiasi espressione di punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="630d1-1220">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1221">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="630d1-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="630d1-1222">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1222">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1223">Hello seguente esempio viene illustrato come toocheck se un punto valido utilizzando ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="630d1-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="630d1-1224">Ad esempio, questo punto ha un valore di latitudine che non è compreso nell'intervallo valido di hello di valori [-90, 90], pertanto hello query restituisce false.</span><span class="sxs-lookup"><span data-stu-id="630d1-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="630d1-1225">Per i poligoni, hello GeoJSON specifica richiede che hello ultima coppia di coordinate specificato deve essere hello stesso come hello innanzitutto toocreate una forma chiusa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="630d1-1226">I punti all'interno di un poligono devono essere specificati in senso antiorario.</span><span class="sxs-lookup"><span data-stu-id="630d1-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="630d1-1227">Un poligono specificato nell'ordine in senso orario rappresenta inverso hello dell'area di hello in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="630d1-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="630d1-1228">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="630d1-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="630d1-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="630d1-1230">Restituisce un valore JSON che contiene un valore booleano se hello specificato LineString, Polygon o punto GeoJSON espressione sia valido e se non è valido, è inoltre hello motivo come valore stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="630d1-1231">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="630d1-1232">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="630d1-1233">È qualsiasi espressione di punto GeoJSON o poligono valida.</span><span class="sxs-lookup"><span data-stu-id="630d1-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="630d1-1234">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="630d1-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="630d1-1235">Restituisce un valore JSON che contiene un valore booleano se hello specificato punto GeoJSON o espressione poligono sia valido e se non è valido, è inoltre hello motivo come valore stringa.</span><span class="sxs-lookup"><span data-stu-id="630d1-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="630d1-1236">**esempi**</span><span class="sxs-lookup"><span data-stu-id="630d1-1236">**Examples**</span></span>  
  
 <span data-ttu-id="630d1-1237">Hello seguente come esempio validità toocheck (con i dettagli) utilizzando ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="630d1-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="630d1-1238">Di seguito è riportato il set di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="630d1-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="630d1-1239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="630d1-1239">Next steps</span></span>  
 <span data-ttu-id="630d1-1240">[Query e sintassi SQL per Azure Cosmos DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="630d1-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="630d1-1241">Documentazione di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="630d1-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
