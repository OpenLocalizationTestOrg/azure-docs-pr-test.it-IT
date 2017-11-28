---
title: 'API di DocumentDB per Azure Cosmos DB: sintassi SQL | Microsoft Docs'
description: Documentazione di riferimento per il linguaggio delle query SQL dell'API di DocumentDB per Azure Cosmos DB.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="2ecc8-103">API di DocumentDB per Azure Cosmos DB: riferimento per la sintassi SQL</span><span class="sxs-lookup"><span data-stu-id="2ecc8-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="2ecc8-104">L'API di DocumentDB per Azure Cosmos DB supporta l'esecuzione di query sui documenti usando un linguaggio SQL (Structured Query Language) familiare come una grammatica per i documenti JSON gerarchici senza richiedere uno schema esplicito o la creazione di indici secondari.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="2ecc8-105">Questo argomento indica la documentazione di riferimento per il linguaggio delle query SQL dell'API di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="2ecc8-106">Per una procedura dettagliata sul linguaggio delle query SQL dell'API di DocumentDB, vedere l'articolo relativo alle [query SQL per l'API di DocumentDB di Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="2ecc8-107">Consigliamo di visitare anche il [Query Playground](http://www.documentdb.com/sql/demo) in cui è possibile provare Azure Cosmos DB ed eseguire query SQL usando il set di dati disponibile.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="2ecc8-108">Query SELECT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-108">SELECT query</span></span>  
<span data-ttu-id="2ecc8-109">Recupera i documenti JSON dal database.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="2ecc8-110">Supporta la valutazione delle espressioni, le proiezioni, il filtraggio e i join.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="2ecc8-111">Le convenzioni usate per descrivere le istruzioni SELECT sono riportate nella sezione relativa alle convenzioni della sintassi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="2ecc8-112">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="2ecc8-113">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-113">**Remarks**</span></span>  
  
 <span data-ttu-id="2ecc8-114">Per i dettagli su ogni clausola, vedere le sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="2ecc8-115">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="2ecc8-116">Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="2ecc8-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="2ecc8-117">Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="2ecc8-118">Clausola ORDER BY</span><span class="sxs-lookup"><span data-stu-id="2ecc8-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="2ecc8-119">Le clausole nell'istruzione SELECT devono essere ordinate come indicato sopra.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="2ecc8-120">Una clausola facoltativa può essere omessa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="2ecc8-121">Ma se si usano clausole facoltative, è necessario specificarle nell'ordine corretto.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="2ecc8-122">**Ordine di elaborazione logico dell'istruzione SELECT**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="2ecc8-123">L'ordine in cui vengono elaborate clausole è:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="2ecc8-124">Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="2ecc8-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="2ecc8-125">Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="2ecc8-126">Clausola ORDER BY</span><span class="sxs-lookup"><span data-stu-id="2ecc8-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="2ecc8-127">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="2ecc8-128">Si noti che l'ordine è diverso da quello in cui appaiono nella sintassi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="2ecc8-129">L'ordinamento è tale che tutti i nuovi simboli introdotti da una clausola elaborata sono visibili e possono essere usati nelle clausole elaborate successivamente.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="2ecc8-130">Ad esempio, gli alias dichiarati in una clausola FROM sono accessibili nelle clausole WHERE e SELECT.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="2ecc8-131">**Spazi vuoti e commenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="2ecc8-132">Tutti i caratteri di spazio vuoto che non fanno parte di una stringa o un identificatore delimitato non fanno parte della grammatica del linguaggio e vengono ignorati durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="2ecc8-133">Il linguaggio di query supporta i commenti in stile T-SQL come</span><span class="sxs-lookup"><span data-stu-id="2ecc8-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="2ecc8-134">istruzione SQL `-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="2ecc8-135">Anche se i commenti e gli spazi vuoti non hanno alcun significato nella grammatica, devono essere usati per separare i token.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="2ecc8-136">Ad esempio: `-1e5` è un token numero singolo, mentre `: – 1 e5` è un token meno seguito dal numero 1 e dall'identificatore e5.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="2ecc8-137"><a name="bk_select_query"></a> Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="2ecc8-138">Le clausole nell'istruzione SELECT devono essere ordinate come indicato sopra.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="2ecc8-139">Una clausola facoltativa può essere omessa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="2ecc8-140">Ma se si usano clausole facoltative, è necessario specificarle nell'ordine corretto.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="2ecc8-141">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="2ecc8-142">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="2ecc8-143">Proprietà o valore da selezionare per il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="2ecc8-144">Specifica che il valore deve essere recuperato senza apportare alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="2ecc8-145">In particolare, se il valore elaborato è un oggetto, tutte le proprietà verranno recuperate.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="2ecc8-146">Specifica l'elenco di proprietà da recuperare.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="2ecc8-147">Ogni valore restituito sarà un oggetto con le proprietà specificate.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="2ecc8-148">Specifica che deve essere recuperato il valore JSON anziché l'oggetto JSON completo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="2ecc8-149">A differenza di `<property_list>` non esegue il wrapping del valore previsto in un oggetto.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="2ecc8-150">Espressione che rappresenta il valore da calcolare.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="2ecc8-151">Vedere la sezione [Espressioni scalari](#bk_scalar_expressions) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="2ecc8-152">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-152">**Remarks**</span></span>  
  
<span data-ttu-id="2ecc8-153">La sintassi di `SELECT *` è valida solo se la clausola FROM ha dichiarato esattamente un alias.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="2ecc8-154">`SELECT *` offre una proiezione dell'identità, che può essere utile se non è necessaria alcuna proiezione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="2ecc8-155">SELECT * è valida solo se viene specificata la clausola FROM e se viene introdotta solo una singola origine di input.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="2ecc8-156">Si noti che `SELECT <select_list>` e `SELECT *` sono "zucchero sintattico" e può essere espressi in alternativa usando semplici istruzioni SELECT, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="2ecc8-157">Equivale a:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="2ecc8-158">Equivale a:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="2ecc8-159">**Vedere anche**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-159">**See Also**</span></span>  
  
[<span data-ttu-id="2ecc8-160">Espressioni scalari</span><span class="sxs-lookup"><span data-stu-id="2ecc8-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="2ecc8-161">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="2ecc8-162"><a name="bk_from_clause"></a> Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="2ecc8-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="2ecc8-163">Specifica l'origine o le origini unite in join.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="2ecc8-164">La clausola FROM è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-164">The FROM clause is optional.</span></span> <span data-ttu-id="2ecc8-165">Se non viene specificata, le altre clausole verranno comunque eseguite come se la clausola FROM specificasse un singolo documento.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="2ecc8-166">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-166">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="2ecc8-167">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="2ecc8-168">Specifica un'origine dati, con o senza un alias.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="2ecc8-169">Se non viene specificato, l'alias verrà dedotto da `<collection_expression>` usando le seguenti regole:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="2ecc8-170">Se l'espressione è un nome di raccolta, come alias verrà usato il nome della raccolta.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="2ecc8-171">Se l'espressione è `<collection_expression>` seguito da un nome di proprietà, come alias verrà usato il nome della proprietà.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="2ecc8-172">Se l'espressione è un nome di raccolta, come alias verrà usato il nome della raccolta.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="2ecc8-173">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="2ecc8-174">Specifica che l'oggetto `input_alias` è un set di valori restituiti dall'espressione di raccolta sottostante.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="2ecc8-175">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="2ecc8-176">Specifica che `input_alias` deve rappresentare il set di valori ottenuto eseguendo l'iterazione su tutti gli elementi di ogni matrice restituita dall'espressione di raccolta sottostante.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="2ecc8-177">Tutti i valori restituiti dall'espressione di raccolta sottostante che non sono matrici vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="2ecc8-178">Specifica l'espressione di raccolta da usare per recuperare i documenti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="2ecc8-179">Specifica che il documento deve essere recuperato dalla raccolta predefinita attualmente connessa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="2ecc8-180">Specifica che il documento deve essere recuperato dalla raccolta specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="2ecc8-181">Il nome della raccolta deve corrispondere al nome della raccolta a cui si è attualmente connessi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="2ecc8-182">Specifica che il documento deve essere recuperato dall'altra origine definita dall'alias indicato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="2ecc8-183">Specifica che il documento deve essere recuperato eseguendo l'accesso alla proprietà `property_name` o all'elemento di matrice array_index per tutti i documenti recuperati dall'espressione di raccolta specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="2ecc8-184">Specifica che il documento deve essere recuperato eseguendo l'accesso alla proprietà `property_name` o all'elemento di matrice array_index per tutti i documenti recuperati dall'espressione di raccolta specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="2ecc8-185">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-185">**Remarks**</span></span>  
  
<span data-ttu-id="2ecc8-186">Tutti gli alias specificati o dedotti in `<from_source>(` devono essere univoci.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="2ecc8-187">La sintassi `<collection_expression>.`nome proprietà equivale a `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="2ecc8-188">Tuttavia, la seconda sintassi può essere usata se un nome di proprietà contiene un carattere non identificatore.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="2ecc8-189">**Proprietà mancanti, elementi di matrice mancanti, gestione dei valori non definita**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="2ecc8-190">Se un'espressione di raccolta accede alle proprietà o agli elementi di matrice e il valore non esiste, tale valore verrà ignorato e non elaborato ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="2ecc8-191">**Definizione dell'ambito per il contesto dell'espressione di raccolta**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="2ecc8-192">Un'espressione di raccolta può avere come ambito una raccolta o un documento:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="2ecc8-193">Un'espressione ha un ambito raccolta se l'origine dell'espressione di raccolta sottostante è ROOT o `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="2ecc8-194">Un'espressione di questo tipo rappresenta un set di documenti recuperati direttamente dalla raccolta e non dipende dall'elaborazione di altre espressioni di raccolta.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="2ecc8-195">Un'espressione ha un ambito documento se l'origine dell'espressione di raccolta sottostante è `input_alias` introdotta in precedenza nella query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="2ecc8-196">Tale espressione rappresenta un set di documenti ottenuti dalla valutazione dell'espressione di raccolta nell'ambito di ogni documento appartenente al set associato alla raccolta con alias.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="2ecc8-197">Il set risultante sarà un'unione di set ottenuti dalla valutazione dell'espressione di raccolta per ogni documento del set sottostante.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="2ecc8-198">**Join**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-198">**Joins**</span></span>  
  
<span data-ttu-id="2ecc8-199">Nella versione corrente, Azure Cosmos DB supporta gli inner join.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="2ecc8-200">Altre funzionalità di join saranno presto disponibili.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="2ecc8-201">Gli inner join generano un prodotto incrociato completo dei set che partecipano al join.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="2ecc8-202">Il risultato di un join a N vie è un set di tuple a N elementi, in cui ogni valore presente nella tupla è associato al set con alias che partecipa al join e l'accesso al set è possibile facendo riferimento a tale alias in altre clausole.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="2ecc8-203">La valutazione del join dipende dall'ambito del contesto dei set partecipanti:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="2ecc8-204">Un join tra il set di raccolta A e il set di raccolta con ambito B genera un prodotto incrociato di tutti gli elementi presenti nei set A e B.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="2ecc8-205">Un join tra il set A e il set con ambito documento B genera un'unione di tutti i set ottenuti dalla valutazione di un set con ambito documento B per ogni documento del set A.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="2ecc8-206">Nella versione corrente l'elaborazione delle query supporta al massimo un'espressione con ambito raccolta.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="2ecc8-207">**Esempi di join:**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="2ecc8-208">Verrà ora esaminata la seguente clausola FROM: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="2ecc8-209">Consentire a ogni origine di definire `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="2ecc8-210">Questa clausola FROM restituisce un set di N tuple (tuple con N valori).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="2ecc8-211">Ogni tupla ha valori prodotti dall'iterazione di tutti gli alias della raccolta sui rispettivi set.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="2ecc8-212">*Esempio di JOIN 1, con 2 origini:*</span><span class="sxs-lookup"><span data-stu-id="2ecc8-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="2ecc8-213">Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="2ecc8-214">Consentire a `<from_source2>` di avere un ambito documento che fa riferimento a input_alias1 e di rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="2ecc8-215">{1, 2} per `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="2ecc8-216">{3} per `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="2ecc8-217">{4, 5} per `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="2ecc8-218">La clausola FROM `<from_source1> JOIN <from_source2>` produrrà le tuple seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="2ecc8-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="2ecc8-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="2ecc8-220">*Esempio di JOIN 2, con 3 origini:*</span><span class="sxs-lookup"><span data-stu-id="2ecc8-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="2ecc8-221">Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="2ecc8-222">Consentire a `<from_source2>` di avere un ambito documento che fa riferimento `input_alias1` e di rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="2ecc8-223">{1, 2} per `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="2ecc8-224">{3} per `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="2ecc8-225">{4, 5} per `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="2ecc8-226">Consentire a `<from_source3>` di avere un ambito documento che fa riferimento `input_alias2` e di rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="2ecc8-227">{100, 200} per `input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="2ecc8-228">{300} per `input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="2ecc8-229">La clausola FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` produrrà le tuple seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="2ecc8-230">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="2ecc8-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="2ecc8-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="2ecc8-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2ecc8-232">Mancano le tuple per altri valori di `input_alias1`, `input_alias2`, per cui `<from_source3>` non ha restituito alcun valore.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="2ecc8-233">*Esempio di JOIN 3, con 3 origini:*</span><span class="sxs-lookup"><span data-stu-id="2ecc8-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="2ecc8-234">Consentire a <from_source1> di avere un ambito raccolta e di rappresentare il set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="2ecc8-235">Consentire a `<from_source1>` di avere un ambito raccolta e di rappresentare il set {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="2ecc8-236">Consentire a <from_source2> di avere un ambito documento che fa riferimento a input_alias1 e di rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="2ecc8-237">{1, 2} per `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="2ecc8-238">{3} per `input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="2ecc8-239">{4, 5} per `input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="2ecc8-240">Consentire a `<from_source3>` di avere ambito `input_alias1` e rappresentare i set:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="2ecc8-241">{100, 200} per `input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="2ecc8-242">{300} per `input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="2ecc8-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="2ecc8-243">La clausola FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` produrrà le tuple seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="2ecc8-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="2ecc8-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="2ecc8-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="2ecc8-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2ecc8-246">Viene generato un prodotto incrociato tra `<from_source2>` e `<from_source3>` perché entrambi hanno come ambito lo stesso elemento `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="2ecc8-247">Sono state create 4 (2x2) tuple con valore A, 0 tuple con valore B (1 x 0) e 2 (2x1) tuple con valore C.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="2ecc8-248">**Vedere anche**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-248">**See also**</span></span>  
  
 [<span data-ttu-id="2ecc8-249">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="2ecc8-250"><a name="bk_where_clause"></a> Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="2ecc8-251">Specifica la condizione di ricerca per i documenti restituiti dalla query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="2ecc8-252">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="2ecc8-253">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="2ecc8-254">Specifica la condizione che deve essere soddisfatta per i documenti da restituire.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="2ecc8-255">Espressione che rappresenta il valore da calcolare.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="2ecc8-256">Vedere la sezione [Espressioni scalari](#bk_scalar_expressions) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="2ecc8-257">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-257">**Remarks**</span></span>  
  
 <span data-ttu-id="2ecc8-258">Affinché il documento venga restituito, un'espressione specificata come condizione di filtro deve restituire true.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="2ecc8-259">Solo un valore booleano true soddisferà la condizione, i valori non definiti, null, false, numero, matrice o oggetto non soddisfano la condizione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="2ecc8-260"><a name="bk_orderby_clause"></a> Clausola ORDER BY</span><span class="sxs-lookup"><span data-stu-id="2ecc8-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="2ecc8-261">Specifica l'ordinamento dei risultati restituiti dalla query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="2ecc8-262">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="2ecc8-263">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="2ecc8-264">Specifica una proprietà o espressione in cui ordinare il set di risultati della query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="2ecc8-265">Una colonna di ordinamento può essere specificata come alias di nome o di colonna.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="2ecc8-266">È possibile specificare più colonne di ordinamento.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="2ecc8-267">I nomi delle colonne devono essere univoci.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-267">Column names must be unique.</span></span> <span data-ttu-id="2ecc8-268">La sequenza delle colonne di ordinamento nella clausola ORDER BY definisce l'organizzazione del set di risultati ordinato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="2ecc8-269">Ovvero, il set di risultati viene ordinato in base alla prima proprietà e quindi l'elenco così ordinato viene ordinato in base alla seconda proprietà e così via.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="2ecc8-270">I nomi delle colonne a cui si fa riferimento nella clausola ORDER BY devono corrispondere a una colonna dell'elenco di selezione o a una colonna definita in una tabella specificata nella clausola FROM senza ambiguità.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="2ecc8-271">Specifica una singola proprietà o espressione in cui ordinare il set di risultati della query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="2ecc8-272">Vedere la sezione [Espressioni scalari](#bk_scalar_expressions) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="2ecc8-273">Specifica che i valori presenti nella colonna specificata devono essere ordinati in ordine crescente o decrescente.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="2ecc8-274">ASC (crescente) esegue l'ordinamento dal valore più basso a quello più alto.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="2ecc8-275">DESC (decrescente) esegue l'ordinamento dal valore più alto a quello più basso.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="2ecc8-276">L'ordinamento predefinito è ASC (crescente).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-276">ASC is the default sort order.</span></span> <span data-ttu-id="2ecc8-277">I valori Null vengono considerati come i valori più bassi possibile.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="2ecc8-278">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-278">**Remarks**</span></span>  
  
 <span data-ttu-id="2ecc8-279">Benché la sintassi di query supporti più proprietà di ordinamento, il runtime di query di Azure Cosmos DB supporta l'ordinamento solo in base a una singola proprietà e solo in base ai nomi di proprietà, ovvero non in base a proprietà calcolate.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="2ecc8-280">L'ordinamento richiede anche che i criteri di indicizzazione includano un indice di intervallo per la proprietà e il tipo specificato, con la massima precisione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="2ecc8-281">Per informazioni dettagliate, fare riferimento alla documentazione sui criteri di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="2ecc8-282"><a name="bk_scalar_expressions"></a> Espressioni scalari</span><span class="sxs-lookup"><span data-stu-id="2ecc8-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="2ecc8-283">Un'espressione scalare è una combinazione di simboli e operatori che si può valutare per ottenere un singolo valore.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="2ecc8-284">Le espressioni semplici possono essere costanti, riferimenti a proprietà, riferimenti a elementi di matrice, riferimenti ad alias o chiamate di funzioni.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="2ecc8-285">Le espressioni semplici possono essere combinate in espressioni complesse usando gli operatori.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="2ecc8-286">Per informazioni dettagliate sui valori che possono essere contenuti nelle espressioni scalari, vedere la sezione relativa alle [costanti](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="2ecc8-287">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-287">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-288">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="2ecc8-289">Rappresenta un valore costante.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-289">Represents a constant value.</span></span> <span data-ttu-id="2ecc8-290">Per informazioni dettagliate, vedere la sezione [Costanti](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="2ecc8-291">Rappresenta un valore definito dall'elemento `input_alias` introdotto nella clausola `FROM`.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="2ecc8-292">Questo valore è sicuramente diverso da un valore **non definito**: i valori **non definiti** presenti nell'input verranno ignorati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="2ecc8-293">Rappresenta un valore della proprietà di un oggetto.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="2ecc8-294">Se la proprietà non esiste o si fa riferimento alla proprietà per un valore che non è un oggetto, l'espressione restituisce un valore **non definito**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="2ecc8-295">Rappresenta un valore della proprietà con nome `property_name` o un elemento di matrice con indice `array_index` di un oggetto o una matrice.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="2ecc8-296">Se l'indice della proprietà o matrice non esiste o si fa riferimento all'indice della proprietà o matrice per un valore che non è un oggetto o una matrice, l'espressione restituisce un valore non definito.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="2ecc8-297">Rappresenta un operatore applicato a un singolo valore.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="2ecc8-298">Per informazioni dettagliate, vedere la sezione [Operatori](#bk_operators).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="2ecc8-299">Rappresenta un operatore applicato a due valori.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="2ecc8-300">Per informazioni dettagliate, vedere la sezione [Operatori](#bk_operators).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="2ecc8-301">Rappresenta un valore definito da un risultato di una chiamata di funzione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="2ecc8-302">Nome della funzione scalare definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="2ecc8-303">Nome della funzione scalare predefinita.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="2ecc8-304">Rappresenta un valore ottenuto creando un nuovo oggetto con proprietà specificate e i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="2ecc8-305">Rappresenta un valore ottenuto creando una nuova matrice con valori specificati come elementi</span><span class="sxs-lookup"><span data-stu-id="2ecc8-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="2ecc8-306">Rappresenta un valore del nome di parametro specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="2ecc8-307">I nomi di parametro devono avere un singolo carattere @ come primo carattere.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="2ecc8-308">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-308">**Remarks**</span></span>  
  
 <span data-ttu-id="2ecc8-309">Quando si chiama una funzione scalare predefinita o definita dall'utente è necessario definire tutti gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="2ecc8-310">Se uno degli argomenti non è definito, la funzione non verrà chiamata e il risultato sarà indefinito.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="2ecc8-311">Quando si crea un oggetto, qualsiasi proprietà a cui viene assegnato un valore non definito verrà ignorata e non inclusa nell'oggetto creato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="2ecc8-312">Quando si crea una matrice, qualsiasi valore di elemento a cui viene assegnato un valore **non definito** verrà ignorato e non incluso nell'oggetto creato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="2ecc8-313">Ciò causa la sostituzione dell'elemento da parte dell'elemento definito successivo in modo tale che la matrice creata non abbia indici ignorati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="2ecc8-314"><a name="bk_operators"></a> Operatori</span><span class="sxs-lookup"><span data-stu-id="2ecc8-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="2ecc8-315">Questa sezione descrive gli operatori supportati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-315">This section describes the supported operators.</span></span> <span data-ttu-id="2ecc8-316">Ogni operatore può essere assegnato a esattamente una categoria.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="2ecc8-317">Vedere la tabella delle **categorie di operatori** riportata di seguito per informazioni dettagliate sulla gestione dei valori **non definiti**, sui requisiti di tipi per valori di input e sulla gestione dei valori con tipi non corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="2ecc8-318">**Categorie di operatori:**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="2ecc8-319">**Categoria**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-319">**Category**</span></span>|<span data-ttu-id="2ecc8-320">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="2ecc8-321">**aritmetico**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-321">**arithmetic**</span></span>|<span data-ttu-id="2ecc8-322">L'operatore prevede che gli input siano numerici.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="2ecc8-323">Anche l'output è un numero.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-323">Output is also a Number.</span></span> <span data-ttu-id="2ecc8-324">Se uno degli input è **non definito** o di tipo diverso da un numero, il risultato è **non definito**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="2ecc8-325">**bit per bit**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-325">**bitwise**</span></span>|<span data-ttu-id="2ecc8-326">L'operatore prevede che gli input siano numeri interi con segno a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="2ecc8-327">Anche l'output è un numero intero con segno a 32 bit.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="2ecc8-328">Gli eventuali valori non interi vengono arrotondati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="2ecc8-329">I valori positivi verranno arrotondati per difetto, i valori negativi per eccesso.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="2ecc8-330">Qualsiasi valore esterno all'intervallo di interi a 32 bit verrà convertito prendendo gli ultimi 32 bit della relativa notazione di complemento a due.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="2ecc8-331">Se uno degli input è **non definito** o di tipo diverso da un numero, il risultato è **non definito**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="2ecc8-332">**Nota:** il comportamento descritto sopra è compatibile con il comportamento di un operatore bit per bit di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="2ecc8-333">**logico**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-333">**logical**</span></span>|<span data-ttu-id="2ecc8-334">L'operatore prevede che gli input siano valori booleani.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="2ecc8-335">Anche l'output è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="2ecc8-336">Se uno degli input è **non definito** o di tipo diverso da un valore booleano, il risultato sarà **non definito**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="2ecc8-337">**confronto**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-337">**comparison**</span></span>|<span data-ttu-id="2ecc8-338">L'operatore prevede che gli input abbiano lo stesso tipo e non siano indefiniti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="2ecc8-339">L'output è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="2ecc8-340">Se uno degli input è **non definito** o gli input hanno tipi diversi, il risultato è **non definito**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="2ecc8-341">Vedere la tabella dell'**ordinamento dei valori per il confronto** per informazioni dettagliate sull'ordinamento dei valori.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="2ecc8-342">**string**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-342">**string**</span></span>|<span data-ttu-id="2ecc8-343">L'operatore prevede che gli input siano stringhe.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="2ecc8-344">Anche l'output è una stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-344">Output is also a String.</span></span><br /><span data-ttu-id="2ecc8-345">Se uno degli input è **non definito** o di tipo diverso da una stringa, il risultato è **non definito**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="2ecc8-346">**Operatori unari:**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="2ecc8-347">**Nome**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-347">**Name**</span></span>|<span data-ttu-id="2ecc8-348">**Operatore**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-348">**Operator**</span></span>|<span data-ttu-id="2ecc8-349">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="2ecc8-350">**aritmetico**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="2ecc8-351">Restituisce il valore numerico.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="2ecc8-352">Negazione bit per bit.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-352">Bitwise negation.</span></span> <span data-ttu-id="2ecc8-353">Restituisce il valore numerico negato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="2ecc8-354">**bit per bit**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-354">**bitwise**</span></span>|~|<span data-ttu-id="2ecc8-355">Complemento a uno.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-355">Ones' complement.</span></span> <span data-ttu-id="2ecc8-356">Restituisce un complemento di un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="2ecc8-357">**Logico**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-357">**Logical**</span></span>|<span data-ttu-id="2ecc8-358">**NOT**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-358">**NOT**</span></span>|<span data-ttu-id="2ecc8-359">Negazione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-359">Negation.</span></span> <span data-ttu-id="2ecc8-360">Restituisce un valore booleano negato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="2ecc8-361">**Operatori binari:**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="2ecc8-362">**Nome**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-362">**Name**</span></span>|<span data-ttu-id="2ecc8-363">**Operatore**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-363">**Operator**</span></span>|<span data-ttu-id="2ecc8-364">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="2ecc8-365">**aritmetico**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="2ecc8-366">Addizione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-366">Addition.</span></span><br /><br /> <span data-ttu-id="2ecc8-367">Sottrazione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="2ecc8-368">Moltiplicazione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="2ecc8-369">Divisione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-369">Division.</span></span><br /><br /> <span data-ttu-id="2ecc8-370">Modulazione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-370">Modulation.</span></span>|  
|<span data-ttu-id="2ecc8-371">**bit per bit**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-371">**bitwise**</span></span>|<span data-ttu-id="2ecc8-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="2ecc8-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="2ecc8-373">OR bit per bit.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="2ecc8-374">AND bit per bit.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="2ecc8-375">XOR bit per bit.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="2ecc8-376">Spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="2ecc8-377">Spostamento a destra.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="2ecc8-378">Spostamento a destra riempimento zero.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="2ecc8-379">**logico**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-379">**logical**</span></span>|<span data-ttu-id="2ecc8-380">**AND**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-380">**AND**</span></span><br /><br /> <span data-ttu-id="2ecc8-381">**OR**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-381">**OR**</span></span>|<span data-ttu-id="2ecc8-382">Congiunzione logica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-382">Logical conjunction.</span></span> <span data-ttu-id="2ecc8-383">Restituisce **true** se entrambi gli argomenti sono **true**, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="2ecc8-384">Congiunzione logica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-384">Logical conjunction.</span></span> <span data-ttu-id="2ecc8-385">Restituisce **true** se entrambi gli argomenti sono **true**, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="2ecc8-386">**confronto**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="2ecc8-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="2ecc8-388">**??**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-388">**??**</span></span>|<span data-ttu-id="2ecc8-389">Uguale a.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-389">Equals.</span></span> <span data-ttu-id="2ecc8-390">Restituisce **true** se gli argomenti sono uguali, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="2ecc8-391">Diverso da.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-391">Not equal to.</span></span> <span data-ttu-id="2ecc8-392">Restituisce **true** se gli argomenti non sono uguali, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="2ecc8-393">Maggiore di.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-393">Greater Than.</span></span> <span data-ttu-id="2ecc8-394">Restituisce **true** se il primo argomento è maggiore del secondo, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="2ecc8-395">Maggiore o uguale a.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-395">Greater Than or Equal To.</span></span> <span data-ttu-id="2ecc8-396">Restituisce **true** se il primo argomento è maggiore o uguale al secondo, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="2ecc8-397">Minore di.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-397">Less Than.</span></span> <span data-ttu-id="2ecc8-398">Restituisce **true** se il primo argomento è minore del secondo, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="2ecc8-399">Minore o uguale a.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-399">Less Than or Equal To.</span></span> <span data-ttu-id="2ecc8-400">Restituisce **true** se il primo argomento è minore o uguale al secondo, altrimenti restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="2ecc8-401">Unione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-401">Coalesce.</span></span> <span data-ttu-id="2ecc8-402">Restituisce il secondo argomento se il primo argomento è un valore **non definito**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="2ecc8-403">**Stringa**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-403">**String**</span></span>|<span data-ttu-id="2ecc8-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-404">**&#124;&#124;**</span></span>|<span data-ttu-id="2ecc8-405">Concatenazione.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-405">Concatenation.</span></span> <span data-ttu-id="2ecc8-406">Restituisce una concatenazione di entrambi gli argomenti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="2ecc8-407">**Operatori ternari:**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="2ecc8-408">Operatore ternario</span><span class="sxs-lookup"><span data-stu-id="2ecc8-408">Ternary operator</span></span>|<span data-ttu-id="2ecc8-409">?</span><span class="sxs-lookup"><span data-stu-id="2ecc8-409">?</span></span>|<span data-ttu-id="2ecc8-410">Restituisce il secondo argomento se il primo argomento restituisce **true**, altrimenti restituisce il terzo argomento.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="2ecc8-411">**Ordinamento dei valori per il confronto**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="2ecc8-412">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-412">**Type**</span></span>|<span data-ttu-id="2ecc8-413">**Ordine dei valori**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="2ecc8-414">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-414">**Undefined**</span></span>|<span data-ttu-id="2ecc8-415">Non confrontabile.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-415">Not comparable.</span></span>|  
|<span data-ttu-id="2ecc8-416">**Null**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-416">**Null**</span></span>|<span data-ttu-id="2ecc8-417">Singolo valore: **null**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-417">Single value: **null**</span></span>|  
|<span data-ttu-id="2ecc8-418">**Number**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-418">**Number**</span></span>|<span data-ttu-id="2ecc8-419">Numero reale naturale.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="2ecc8-420">Il valore infinito negativo è minore di qualsiasi altro valore numerico.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="2ecc8-421">Il valore infinito positivo è maggiore di qualsiasi altro valore numerico. il valore **NaN** non è confrontabile.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="2ecc8-422">Il confronto con **NaN** restituisce un valore **non definito**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="2ecc8-423">**String**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-423">**String**</span></span>|<span data-ttu-id="2ecc8-424">Ordine lessicografico.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="2ecc8-425">**Array**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-425">**Array**</span></span>|<span data-ttu-id="2ecc8-426">Nessun ordinamento, ma equo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="2ecc8-427">**Object**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-427">**Object**</span></span>|<span data-ttu-id="2ecc8-428">Nessun ordinamento, ma equo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="2ecc8-429">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-429">**Remarks**</span></span>  
  
 <span data-ttu-id="2ecc8-430">In Azure Cosmos DB i tipi di valori sono spesso sconosciuti finché non vengono materialmente recuperati dal database.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="2ecc8-431">Per supportare un'esecuzione efficiente delle query, gran parte degli operatori presentano rigorosi requisiti di tipi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="2ecc8-432">Inoltre, gli operatori di per sé non eseguono conversioni implicite.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="2ecc8-433">Ciò significa che una query come: SELECT * FROM ROOT r WHERE r.Age = 21 restituisce solo documenti con la proprietà Age uguale al numero 21.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="2ecc8-434">I documenti con la proprietà Age uguale alla stringa "21" o alla stringa "0021" non corrispondono, poiché l'espressione "21" = 21 restituisce un valore non definito.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="2ecc8-435">Questo consente un uso migliore degli indici, poiché la ricerca di un valore specifico, ovvero il numero 21, è più veloce rispetto alla ricerca di un numero indefinito di possibili corrispondenze (il numero 21 o le stringhe "21", "021", "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="2ecc8-436">Ciò si differenzia dal modo in cui JavaScript valuta gli operatori per valori di tipi diversi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="2ecc8-437">**Confronto e uguaglianza di oggetti e matrici**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="2ecc8-438">Il confronto dei valori di oggetto o matrice con gli operatori di intervallo (>, >=, <, <=) produce un risultato indefinito poiché non è definito un ordine per i valori di oggetto o matrice.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="2ecc8-439">Tuttavia l'uso degli operatori di uguaglianza/disuguaglianza (=,! =, <>) è supportato e i valori vengono confrontati strutturalmente.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="2ecc8-440">Le matrici sono uguali se entrambe le matrici hanno stesso numero di elementi e sono uguali anche gli elementi nelle posizioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="2ecc8-441">Se il confronto di qualsiasi coppia di elementi produce un risultato indefinito, il risultato del confronto di matrici è indefinito.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="2ecc8-442">Gli oggetti sono uguali se entrambi gli oggetti hanno le stesse proprietà definite e se anche i valori delle proprietà corrispondenti sono uguali.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="2ecc8-443">Se il confronto di qualsiasi coppia di valori di proprietà produce un risultato indefinito, il risultato del confronto di oggetti è indefinito.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="2ecc8-444"><a name="bk_constants"></a> Costanti</span><span class="sxs-lookup"><span data-stu-id="2ecc8-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="2ecc8-445">Una costante, nota anche come valore letterale o scalare, è un simbolo che rappresenta un valore di dati specifico.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="2ecc8-446">Il formato di una costante dipende dal tipo di dati del valore che rappresenta.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="2ecc8-447">**Tipi di dati scalari supportati:**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="2ecc8-448">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-448">**Type**</span></span>|<span data-ttu-id="2ecc8-449">**Ordine dei valori**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="2ecc8-450">**Undefined**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-450">**Undefined**</span></span>|<span data-ttu-id="2ecc8-451">Singolo valore: **non definito**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="2ecc8-452">**Null**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-452">**Null**</span></span>|<span data-ttu-id="2ecc8-453">Singolo valore: **null**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-453">Single value: **null**</span></span>|  
|<span data-ttu-id="2ecc8-454">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-454">**Boolean**</span></span>|<span data-ttu-id="2ecc8-455">Valori: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="2ecc8-456">**Number**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-456">**Number**</span></span>|<span data-ttu-id="2ecc8-457">Un numero a virgola mobile e precisione doppia, standard IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="2ecc8-458">**String**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-458">**String**</span></span>|<span data-ttu-id="2ecc8-459">Una sequenza di zero o più caratteri Unicode.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="2ecc8-460">Le stringhe devono essere racchiuse tra virgolette singole o doppie.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="2ecc8-461">**Array**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-461">**Array**</span></span>|<span data-ttu-id="2ecc8-462">Una sequenza di zero o più elementi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="2ecc8-463">Ogni elemento può essere un valore di qualsiasi tipo di dati scalare, tranne Undefined.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="2ecc8-464">**Object**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-464">**Object**</span></span>|<span data-ttu-id="2ecc8-465">Un set non ordinato di zero o più coppie nome/valore.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="2ecc8-466">Il nome è una stringa Unicode, il valore può essere di qualsiasi tipo di dati scalare, tranne **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="2ecc8-467">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-467">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-468">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="2ecc8-469">Rappresenta un valore non definito di tipo Undefined.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="2ecc8-470">Rappresenta un valore **null** di tipo **Null**.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="2ecc8-471">Rappresenta una costante di tipo Boolean.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="2ecc8-472">Rappresenta un valore **false** di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="2ecc8-473">Rappresenta un valore **true** di tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="2ecc8-474">Rappresenta una costante.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="2ecc8-475">I valori letterali decimali sono numeri rappresentati usando la notazione decimale o la notazione scientifica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="2ecc8-476">I valori letterali esadecimali sono numeri rappresentati usando il prefisso "0x" seguito da una o più cifre esadecimali.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="2ecc8-477">Rappresenta una costante di tipo String.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="2ecc8-478">I valori letterali stringa sono stringhe Unicode rappresentate da una sequenza di zero o più caratteri Unicode o sequenze di escape.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="2ecc8-479">I valori letterali stringa sono racchiusi tra virgolette singole (apostrofo: ') o virgolette doppie (virgolette inglesi: ").</span><span class="sxs-lookup"><span data-stu-id="2ecc8-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="2ecc8-480">Sono consentite le sequenze di escape seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="2ecc8-481">**Sequenza di escape**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-481">**Escape sequence**</span></span>|<span data-ttu-id="2ecc8-482">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-482">**Description**</span></span>|<span data-ttu-id="2ecc8-483">**Carattere Unicode**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="2ecc8-484">\\'</span><span class="sxs-lookup"><span data-stu-id="2ecc8-484">\\'</span></span>|<span data-ttu-id="2ecc8-485">apostrofo (')</span><span class="sxs-lookup"><span data-stu-id="2ecc8-485">apostrophe (')</span></span>|<span data-ttu-id="2ecc8-486">U + 0027</span><span class="sxs-lookup"><span data-stu-id="2ecc8-486">U+0027</span></span>|  
|<span data-ttu-id="2ecc8-487">\\"</span><span class="sxs-lookup"><span data-stu-id="2ecc8-487">\\"</span></span>|<span data-ttu-id="2ecc8-488">virgolette doppie (")</span><span class="sxs-lookup"><span data-stu-id="2ecc8-488">quotation mark (")</span></span>|<span data-ttu-id="2ecc8-489">U + 0022</span><span class="sxs-lookup"><span data-stu-id="2ecc8-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="2ecc8-490">barra rovesciata (\\)</span><span class="sxs-lookup"><span data-stu-id="2ecc8-490">reverse solidus (\\)</span></span>|<span data-ttu-id="2ecc8-491">U + 005C</span><span class="sxs-lookup"><span data-stu-id="2ecc8-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="2ecc8-492">barra (/)</span><span class="sxs-lookup"><span data-stu-id="2ecc8-492">solidus (/)</span></span>|<span data-ttu-id="2ecc8-493">U + 002F</span><span class="sxs-lookup"><span data-stu-id="2ecc8-493">U+002F</span></span>|  
|<span data-ttu-id="2ecc8-494">\b</span><span class="sxs-lookup"><span data-stu-id="2ecc8-494">\b</span></span>|<span data-ttu-id="2ecc8-495">BACKSPACE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-495">backspace</span></span>|<span data-ttu-id="2ecc8-496">U + 0008</span><span class="sxs-lookup"><span data-stu-id="2ecc8-496">U+0008</span></span>|  
|<span data-ttu-id="2ecc8-497">\f</span><span class="sxs-lookup"><span data-stu-id="2ecc8-497">\f</span></span>|<span data-ttu-id="2ecc8-498">avanzamento carta</span><span class="sxs-lookup"><span data-stu-id="2ecc8-498">form feed</span></span>|<span data-ttu-id="2ecc8-499">U + 000C</span><span class="sxs-lookup"><span data-stu-id="2ecc8-499">U+000C</span></span>|  
|\n|<span data-ttu-id="2ecc8-500">avanzamento riga</span><span class="sxs-lookup"><span data-stu-id="2ecc8-500">line feed</span></span>|<span data-ttu-id="2ecc8-501">U + 000A</span><span class="sxs-lookup"><span data-stu-id="2ecc8-501">U+000A</span></span>|  
|<span data-ttu-id="2ecc8-502">\r</span><span class="sxs-lookup"><span data-stu-id="2ecc8-502">\r</span></span>|<span data-ttu-id="2ecc8-503">ritorno a capo</span><span class="sxs-lookup"><span data-stu-id="2ecc8-503">carriage return</span></span>|<span data-ttu-id="2ecc8-504">U + 000D</span><span class="sxs-lookup"><span data-stu-id="2ecc8-504">U+000D</span></span>|  
|<span data-ttu-id="2ecc8-505">\t</span><span class="sxs-lookup"><span data-stu-id="2ecc8-505">\t</span></span>|<span data-ttu-id="2ecc8-506">TAB</span><span class="sxs-lookup"><span data-stu-id="2ecc8-506">tab</span></span>|<span data-ttu-id="2ecc8-507">U + 0009</span><span class="sxs-lookup"><span data-stu-id="2ecc8-507">U+0009</span></span>|  
|<span data-ttu-id="2ecc8-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="2ecc8-508">\uXXXX</span></span>|<span data-ttu-id="2ecc8-509">Carattere Unicode definito da 4 cifre esadecimali.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="2ecc8-510">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="2ecc8-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="2ecc8-511"><a name="bk_query_perf_guidelines"></a> Linee guida sulle prestazioni delle query</span><span class="sxs-lookup"><span data-stu-id="2ecc8-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="2ecc8-512">Per poter eseguire una query in modo efficiente per una raccolta di grandi dimensioni, è necessario usare filtri che possano essere gestiti attraverso uno o più indici.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="2ecc8-513">Per la ricerca negli indici vengono considerati questi filtri:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="2ecc8-514">Usare l'operatore di uguaglianza (=) con un'espressione percorso documenti e una costante.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="2ecc8-515">Usare gli operatori di intervallo (<, \<=, >, >=) con un'espressione percorso documenti e costanti numeriche.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="2ecc8-516">Con "espressione percorso documenti" si indica qualsiasi espressione che identifica un percorso costante nei documenti provenienti dalla raccolta di database a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="2ecc8-517">**Espressione percorso documenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="2ecc8-518">Le espressioni percorso documenti sono espressioni usate in un percorso di funzioni di valutazione dell'indicizzatore proprietà o matrice per un documento proveniente da documenti di una raccolta di database.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="2ecc8-519">Questo percorso può essere usato per identificare la posizione dei valori a cui si fa riferimento in un filtro direttamente all'interno dei documenti della raccolta di database.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="2ecc8-520">Per essere considerata un'espressione percorso documenti, è necessario che un'espressione:</span><span class="sxs-lookup"><span data-stu-id="2ecc8-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="2ecc8-521">Faccia riferimento direttamente alla radice della raccolta.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="2ecc8-522">Faccia riferimento all'indicizzatore di proprietà o matrici costanti di un'espressione percorso documenti</span><span class="sxs-lookup"><span data-stu-id="2ecc8-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="2ecc8-523">Faccia riferimento a un alias che rappresenta un'espressione percorso documenti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="2ecc8-524">**Convenzioni della sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="2ecc8-525">Nella tabella seguente vengono descritte le convenzioni usate per descrivere la sintassi nel riferimento del linguaggio di query dell'API di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="2ecc8-526">**Convenzione**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-526">**Convention**</span></span>|<span data-ttu-id="2ecc8-527">**Usata per**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="2ecc8-528">LETTERE MAIUSCOLE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-528">UPPERCASE</span></span>|<span data-ttu-id="2ecc8-529">Parole chiave che non fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="2ecc8-530">lettere minuscole</span><span class="sxs-lookup"><span data-stu-id="2ecc8-530">lowercase</span></span>|<span data-ttu-id="2ecc8-531">Parole chiave che fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="2ecc8-532">\<non terminale></span><span class="sxs-lookup"><span data-stu-id="2ecc8-532">\<nonterminal></span></span>|<span data-ttu-id="2ecc8-533">Non terminale, definito separatamente.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="2ecc8-534">\<non terminale> ::=</span><span class="sxs-lookup"><span data-stu-id="2ecc8-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="2ecc8-535">Definizione di sintassi dell'elemento non terminale.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="2ecc8-536">altro_terminale</span><span class="sxs-lookup"><span data-stu-id="2ecc8-536">other_terminal</span></span>|<span data-ttu-id="2ecc8-537">Terminale (token), descritto dettagliatamente con parole.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="2ecc8-538">identificatore</span><span class="sxs-lookup"><span data-stu-id="2ecc8-538">identifier</span></span>|<span data-ttu-id="2ecc8-539">Identificatore.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-539">Identifier.</span></span> <span data-ttu-id="2ecc8-540">Consente solo i seguenti caratteri: a-z A-Z 0-9 _Il primo carattere non può essere una cifra.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="2ecc8-541">"stringa"</span><span class="sxs-lookup"><span data-stu-id="2ecc8-541">"string"</span></span>|<span data-ttu-id="2ecc8-542">Stringa tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-542">Quoted string.</span></span> <span data-ttu-id="2ecc8-543">Consente qualsiasi stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-543">Allows any valid string.</span></span> <span data-ttu-id="2ecc8-544">Vedere la descrizione di string_literal.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="2ecc8-545">'simbolo'</span><span class="sxs-lookup"><span data-stu-id="2ecc8-545">'symbol'</span></span>|<span data-ttu-id="2ecc8-546">Simbolo letterale che fa parte della sintassi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="2ecc8-547">&#124; (barra verticale)</span><span class="sxs-lookup"><span data-stu-id="2ecc8-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="2ecc8-548">Alternative per gli elementi di sintassi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-548">Alternatives for syntax items.</span></span> <span data-ttu-id="2ecc8-549">È possibile usare solo uno degli elementi specificati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="2ecc8-550">[ ] /(parentesi quadre)</span><span class="sxs-lookup"><span data-stu-id="2ecc8-550">[ ] /(brackets)</span></span>|<span data-ttu-id="2ecc8-551">Le parentesi quadre racchiudono uno o più elementi facoltativi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="2ecc8-552">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="2ecc8-552">[ ,...n ]</span></span>|<span data-ttu-id="2ecc8-553">Indica che l'elemento precedente può essere ripetuto n volte.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="2ecc8-554">Le occorrenze sono separate da virgole.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="2ecc8-555">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="2ecc8-555">[ ...n ]</span></span>|<span data-ttu-id="2ecc8-556">Indica che l'elemento precedente può essere ripetuto n volte.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="2ecc8-557">Le occorrenze sono separate da spazi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="2ecc8-558"><a name="bk_built_in_functions"></a> Funzioni predefinite</span><span class="sxs-lookup"><span data-stu-id="2ecc8-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="2ecc8-559">In Azure Cosmos DB sono disponibili molte funzioni SQL predefinite.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="2ecc8-560">Le categorie di funzioni predefinite sono elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="2ecc8-561">Funzione</span><span class="sxs-lookup"><span data-stu-id="2ecc8-561">Function</span></span>|<span data-ttu-id="2ecc8-562">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ecc8-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="2ecc8-563">Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="2ecc8-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="2ecc8-564">Le funzioni matematiche eseguono un calcolo basato in genere su valori di input passati come argomenti e restituiscono un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="2ecc8-565">Funzioni di controllo del tipo</span><span class="sxs-lookup"><span data-stu-id="2ecc8-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="2ecc8-566">Le funzioni di controllo del tipo consentono di controllare il tipo di un'espressione nell'ambito delle query SQL.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="2ecc8-567">Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="2ecc8-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="2ecc8-568">Le funzioni stringa eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, il valore numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="2ecc8-569">Funzioni di matrice</span><span class="sxs-lookup"><span data-stu-id="2ecc8-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="2ecc8-570">Le funzioni di matrice eseguono un'operazione su un valore di input di matrice e restituiscono un valore numerico, booleano o matrice.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="2ecc8-571">Funzioni spaziali</span><span class="sxs-lookup"><span data-stu-id="2ecc8-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="2ecc8-572">Le funzioni spaziali eseguono un'operazione su un valore di input di oggetto spaziale e restituiscono un valore numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="2ecc8-573"><a name="bk_mathematical_functions"></a> Funzioni matematiche</span><span class="sxs-lookup"><span data-stu-id="2ecc8-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="2ecc8-574">Le seguenti funzioni eseguono un calcolo basato in genere su valori di input passati come argomenti e restituiscono un valore numerico.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="2ecc8-575">ABS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="2ecc8-576">ACOS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="2ecc8-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="2ecc8-578">ATAN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="2ecc8-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="2ecc8-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="2ecc8-580">CEILING</span><span class="sxs-lookup"><span data-stu-id="2ecc8-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="2ecc8-581">COS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="2ecc8-582">COT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="2ecc8-583">DEGREES</span><span class="sxs-lookup"><span data-stu-id="2ecc8-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="2ecc8-584">EXP</span><span class="sxs-lookup"><span data-stu-id="2ecc8-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="2ecc8-585">FLOOR</span><span class="sxs-lookup"><span data-stu-id="2ecc8-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="2ecc8-586">LOG</span><span class="sxs-lookup"><span data-stu-id="2ecc8-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="2ecc8-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="2ecc8-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="2ecc8-588">PI</span><span class="sxs-lookup"><span data-stu-id="2ecc8-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="2ecc8-589">POWER</span><span class="sxs-lookup"><span data-stu-id="2ecc8-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="2ecc8-590">RADIANS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="2ecc8-591">ROUND</span><span class="sxs-lookup"><span data-stu-id="2ecc8-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="2ecc8-592">SIN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="2ecc8-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="2ecc8-594">SQUARE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="2ecc8-595">SIGN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="2ecc8-596">TAN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="2ecc8-597">TRUNC</span><span class="sxs-lookup"><span data-stu-id="2ecc8-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="2ecc8-598"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="2ecc8-599">Restituisce il valore assoluto (positivo) dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-600">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-601">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-602">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-603">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-603">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-604">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-605">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-605">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-606">Nell'esempio seguente vengono illustrati i risultati dell'uso della funzione ABS su tre numeri diversi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="2ecc8-607">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="2ecc8-608"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="2ecc8-609">Restituisce l'angolo, espresso in radianti, il cui coseno corrisponde all'espressione numerica specificata. Denominato anche arcocoseno.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="2ecc8-610">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-611">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-612">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-613">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-613">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-614">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-615">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-615">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-616">L'esempio seguente restituisce l'arcocoseno di -1.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="2ecc8-617">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="2ecc8-618"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="2ecc8-619">Restituisce l'angolo, espresso in radianti, il cui seno è l'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="2ecc8-620">Detta anche arcoseno.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="2ecc8-621">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-622">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-623">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-624">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-624">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-625">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-626">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-626">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-627">L'esempio seguente restituisce l'arcoseno di -1.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="2ecc8-628">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="2ecc8-629"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="2ecc8-630">Restituisce l'angolo, espresso in radianti, la cui tangente è l'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="2ecc8-631">Detta anche arcotangente.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="2ecc8-632">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-633">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-634">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-635">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-635">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-636">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-637">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-637">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-638">L'esempio seguente restituisce l'arcotangente del valore specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="2ecc8-639">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="2ecc8-640"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="2ecc8-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="2ecc8-641">Restituisce il valore principale dell'arcotangente di y/x, espresso in radianti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="2ecc8-642">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-643">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-644">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-645">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-645">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-646">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-647">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-647">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-648">L'esempio seguente calcola l'arcotangente per i componenti x e y specificati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="2ecc8-649">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="2ecc8-650"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="2ecc8-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="2ecc8-651">Restituisce il più piccolo valore integer maggiore di o uguale all'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-652">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-653">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-654">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-655">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-655">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-656">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-657">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-657">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-658">L'esempio seguente usa valori numerici positivi, negativi e zero con la funzione CEILING.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="2ecc8-659">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="2ecc8-660"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="2ecc8-661">Restituisce il coseno trigonometrico dell'angolo specificato, espresso in radianti, nell'espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="2ecc8-662">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-663">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-664">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-665">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-665">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-666">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-667">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-667">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-668">L'esempio seguente calcola il coseno dell'angolo specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="2ecc8-669">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="2ecc8-670"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="2ecc8-671">Restituisce la cotangente trigonometrica dell'angolo specificato, espresso in radianti, nell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-672">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-673">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-674">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-675">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-675">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-676">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-677">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-677">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-678">L'esempio seguente calcola la cotangente dell'angolo specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="2ecc8-679">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="2ecc8-680"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="2ecc8-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="2ecc8-681">Restituisce l'angolo corrispondente in gradi di un angolo specificato in radianti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="2ecc8-682">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-683">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-684">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-685">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-685">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-686">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-687">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-687">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-688">L'esempio seguente restituisce il numero di gradi di un angolo di PI/2 radianti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="2ecc8-689">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="2ecc8-690"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="2ecc8-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="2ecc8-691">Restituisce il valore integer più alto, minore di o uguale all'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-692">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-693">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-694">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-695">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-695">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-696">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-697">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-697">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-698">L'esempio seguente usa valori numerici positivi, negativi e zero con la funzione FLOOR.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="2ecc8-699">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="2ecc8-700"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="2ecc8-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="2ecc8-701">Restituisce il valore esponenziale dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-702">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-703">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-704">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-705">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-705">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-706">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-707">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-707">**Remarks**</span></span>  
  
 <span data-ttu-id="2ecc8-708">La costante **e** (2,718281 …) è la base dei logaritmi naturali.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="2ecc8-709">L'esponente di un numero è la costante **e** elevata alla potenza del numero.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="2ecc8-710">Ad esempio, EXP(1.0) = e^1.0 = 2,71828182845905 e EXP(10) = e^10 = 22026,4657948067.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="2ecc8-711">Il valore esponenziale del logaritmo naturale di un numero è il numero stesso: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="2ecc8-712">E il logaritmo naturale dell'esponente di un numero è il numero stesso: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="2ecc8-713">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-713">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-714">Nell'esempio seguente viene dichiarata una variabile e restituito il valore esponenziale della variabile specificata (10).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="2ecc8-715">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="2ecc8-716">L'esempio seguente restituisce il valore esponenziale del logaritmo naturale di 20 e il logaritmo naturale dell'esponente di 20.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="2ecc8-717">Poiché queste funzioni sono inverse l'una dell'altra, il valore restituito con arrotondamento per il calcolo a virgola mobile in entrambi i casi è 20.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="2ecc8-718">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="2ecc8-719"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="2ecc8-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="2ecc8-720">Restituisce il logaritmo naturale dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-721">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="2ecc8-722">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-723">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="2ecc8-724">Argomento numerico facoltativo che imposta la base per il logaritmo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="2ecc8-725">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-725">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-726">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-727">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-727">**Remarks**</span></span>  
  
 <span data-ttu-id="2ecc8-728">Per impostazione predefinita, LOG() restituisce il logaritmo naturale.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="2ecc8-729">È possibile modificare la base del logaritmo e impostare un altro valore usando il parametro di base facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="2ecc8-730">Il logaritmo naturale è il logaritmo in base **e**, dove **e** è una costante irrazionale approssimativamente uguale a 2,718281828.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="2ecc8-731">Il logaritmo naturale dell'esponente di un numero è il numero stesso: LOG ( EXP ( n ) ) = n.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="2ecc8-732">E il valore esponenziale del logaritmo naturale di un numero è il numero stesso: EXP( LOG( n ) ) = n.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="2ecc8-733">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-733">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-734">Nell'esempio seguente viene dichiarata una variabile e restituito il logaritmo della variabile specificata (10).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="2ecc8-735">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="2ecc8-736">L'esempio seguente calcola il logaritmo per l'esponente di un numero.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="2ecc8-737">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="2ecc8-738"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="2ecc8-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="2ecc8-739">Restituisce il logaritmo in base 10 dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-740">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-741">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-742">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-743">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-743">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-744">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-745">**Osservazioni**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-745">**Remarks**</span></span>  
  
 <span data-ttu-id="2ecc8-746">Le funzioni LOG10 e POWER sono inversamente correlate tra loro.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="2ecc8-747">Ad esempio, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="2ecc8-748">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-748">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-749">Nell'esempio seguente viene dichiarata una variabile e restituito il valore LOG10 della variabile specificata (100).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="2ecc8-750">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="2ecc8-751"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="2ecc8-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="2ecc8-752">Restituisce il valore costante di pi greco.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="2ecc8-753">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="2ecc8-754">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-755">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-756">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-756">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-757">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-758">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-758">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-759">L'esempio seguente restituisce il valore di pi greco.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="2ecc8-760">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="2ecc8-761"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="2ecc8-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="2ecc8-762">Restituisce il valore dell'espressione specificata alla potenza specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="2ecc8-763">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="2ecc8-764">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-765">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="2ecc8-766">È la potenza a cui elevare `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="2ecc8-767">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-767">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-768">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-769">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-769">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-770">Nell'esempio seguente viene elevato un numero alla potenza di 3 (cubo del numero).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="2ecc8-771">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="2ecc8-772"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="2ecc8-773">Restituisce radianti quando viene immessa un'espressione numerica, espresso in gradi.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="2ecc8-774">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-775">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-776">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-777">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-777">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-778">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-779">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-779">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-780">L'esempio seguente accetta alcuni angoli come input e restituisce i valori in radianti corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="2ecc8-781">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="2ecc8-782"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="2ecc8-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="2ecc8-783">Restituisce un valore numerico, arrotondato al valore integer più vicino.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="2ecc8-784">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-785">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-786">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-787">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-787">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-788">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-789">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-789">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-790">L'esempio seguente arrotonda numeri positivi e negativi al numero intero più prossimo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="2ecc8-791">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="2ecc8-792"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="2ecc8-793">Restituisce il segno positivo (+1), zero (0) o negativo (-1) dell'espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-794">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-795">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-796">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-797">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-797">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-798">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-799">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-799">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-800">L'esempio seguente restituisce i valori SIGN dei numeri da -2 a 2.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="2ecc8-801">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="2ecc8-802"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="2ecc8-803">Restituisce il seno trigonometrico dell'angolo specificato, espresso in radianti, nell'espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="2ecc8-804">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-805">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-806">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-807">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-807">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-808">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-809">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-809">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-810">L'esempio seguente calcola il seno dell'angolo specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="2ecc8-811">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="2ecc8-812"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="2ecc8-813">Restituisce la radice quadrata del valore numerico specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="2ecc8-814">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-815">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-816">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-817">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-817">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-818">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-819">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-819">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-820">L'esempio seguente restituisce le radici quadrate dei numeri da 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="2ecc8-821">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="2ecc8-822"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="2ecc8-823">Restituisce il quadrato del valore numerico specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="2ecc8-824">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-825">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-826">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-827">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-827">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-828">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-829">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-829">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-830">L'esempio seguente restituisce i quadrati dei numeri da 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="2ecc8-831">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="2ecc8-832"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="2ecc8-833">Restituisce la tangente dell'angolo specificato, espresso in radianti, nell'espressione specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="2ecc8-834">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-835">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-836">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-837">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-837">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-838">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-839">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-839">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-840">L'esempio seguente calcola la tangente di PI()/2.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="2ecc8-841">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="2ecc8-842"><a name="bk_trunc"></a> TRUNC</span><span class="sxs-lookup"><span data-stu-id="2ecc8-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="2ecc8-843">Restituisce un valore numerico, troncato al valore integer più vicino.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="2ecc8-844">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="2ecc8-845">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="2ecc8-846">È un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-847">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-847">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-848">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-849">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-849">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-850">L'esempio seguente tronca numeri positivi e negativi al numero intero più prossimo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="2ecc8-851">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="2ecc8-852"><a name="bk_type_checking_functions"></a> Funzioni di controllo del tipo</span><span class="sxs-lookup"><span data-stu-id="2ecc8-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="2ecc8-853">Le funzioni seguenti supportano il controllo del tipo per i valori di input e ogni funzione restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="2ecc8-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="2ecc8-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="2ecc8-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="2ecc8-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="2ecc8-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="2ecc8-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="2ecc8-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="2ecc8-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="2ecc8-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="2ecc8-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="2ecc8-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="2ecc8-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="2ecc8-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="2ecc8-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="2ecc8-862"><a name="bk_is_array"></a> IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="2ecc8-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="2ecc8-863">Restituisce un valore booleano che indica se il tipo di espressione specificata è una matrice.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="2ecc8-864">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="2ecc8-865">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="2ecc8-866">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-867">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-867">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-868">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-869">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-869">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-870">L'esempio seguente controlla gli oggetti di tipo booleano JSON, numero, stringa, null, oggetto, matrice e non definito usando la funzione IS_ARRAY.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-871">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="2ecc8-872"><a name="bk_is_bool"></a> IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="2ecc8-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="2ecc8-873">Restituisce un valore booleano che indica se il tipo di espressione specificata è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="2ecc8-874">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="2ecc8-875">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="2ecc8-876">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-877">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-877">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-878">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-879">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-879">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-880">L'esempio seguente controlla gli oggetti di tipo booleano JSON, numero, stringa, null, oggetto, matrice e non definito usando la funzione IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-881">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="2ecc8-882"><a name="bk_is_defined"></a> IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="2ecc8-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="2ecc8-883">Restituisce un valore booleano che indica se alla proprietà è stata assegnato un valore.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="2ecc8-884">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="2ecc8-885">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="2ecc8-886">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-887">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-887">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-888">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-889">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-889">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-890">L'esempio seguente verifica la presenza di una proprietà all'interno del documento JSON specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="2ecc8-891">La prima parte restituisce true perché "a" è presente, ma la seconda restituisce false perché "b" è assente.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="2ecc8-892">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="2ecc8-893"><a name="bk_is_null"></a> IS_NULL</span><span class="sxs-lookup"><span data-stu-id="2ecc8-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="2ecc8-894">Restituisce un valore booleano che indica se il tipo di espressione specificata è nulla.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="2ecc8-895">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="2ecc8-896">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="2ecc8-897">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-898">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-898">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-899">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-900">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-900">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-901">L'esempio seguente controlla gli oggetti di tipo booleano JSON, numero, stringa, null, oggetto, matrice e non definito usando la funzione IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-902">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="2ecc8-903"><a name="bk_is_number"></a> IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="2ecc8-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="2ecc8-904">Restituisce un valore booleano che indica se il tipo di espressione specificata è un numero.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="2ecc8-905">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="2ecc8-906">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="2ecc8-907">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-908">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-908">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-909">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-910">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-910">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-911">L'esempio seguente controlla gli oggetti di tipo booleano JSON, numero, stringa, null, oggetto, matrice e non definito usando la funzione IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-912">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="2ecc8-913"><a name="bk_is_object"></a> IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="2ecc8-914">Restituisce un valore booleano che indica se il tipo di espressione specificata è un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="2ecc8-915">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="2ecc8-916">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="2ecc8-917">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-918">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-918">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-919">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-920">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-920">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-921">L'esempio seguente controlla gli oggetti di tipo booleano JSON, numero, stringa, null, oggetto, matrice e non definito usando la funzione IS_OBJECT.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-922">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="2ecc8-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="2ecc8-924">Restituisce un valore booleano che indica se il tipo di espressione specificata è un primitivo (stringa, valore booleano, numerico o null).</span><span class="sxs-lookup"><span data-stu-id="2ecc8-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="2ecc8-925">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="2ecc8-926">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="2ecc8-927">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-928">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-928">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-929">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-930">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-930">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-931">L'esempio seguente controlla gli oggetti di tipo booleano JSON, numero, stringa, null, oggetto, matrice e non definito usando la funzione IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-932">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="2ecc8-933"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="2ecc8-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="2ecc8-934">Restituisce un valore booleano che indica se il tipo di espressione specificata è una stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="2ecc8-935">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="2ecc8-936">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="2ecc8-937">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-938">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-938">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-939">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-940">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-940">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-941">L'esempio seguente controlla gli oggetti di tipo booleano JSON, numero, stringa, null, oggetto, matrice e non definito usando la funzione IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="2ecc8-942">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="2ecc8-943"><a name="bk_string_functions"></a> Funzioni stringa</span><span class="sxs-lookup"><span data-stu-id="2ecc8-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="2ecc8-944">Le funzioni scalari seguenti eseguono un'operazione su un valore di stringa di input e restituiscono una stringa, il valore numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="2ecc8-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="2ecc8-946">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="2ecc8-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="2ecc8-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="2ecc8-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="2ecc8-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="2ecc8-949">LEFT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="2ecc8-950">LENGTH</span><span class="sxs-lookup"><span data-stu-id="2ecc8-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="2ecc8-951">LOWER</span><span class="sxs-lookup"><span data-stu-id="2ecc8-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="2ecc8-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="2ecc8-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="2ecc8-953">REPLACE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="2ecc8-954">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="2ecc8-955">REVERSE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="2ecc8-956">RIGHT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="2ecc8-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="2ecc8-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="2ecc8-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="2ecc8-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="2ecc8-959">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="2ecc8-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="2ecc8-960">UPPER</span><span class="sxs-lookup"><span data-stu-id="2ecc8-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="2ecc8-961"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="2ecc8-962">Restituisce una stringa che rappresenta il risultato della concatenazione di due o più valori di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="2ecc8-963">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="2ecc8-964">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-965">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-966">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-966">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-967">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-968">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-968">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-969">L'esempio seguente restituisce la stringa concatenata dei valori specificati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="2ecc8-970">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="2ecc8-971"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="2ecc8-972">Restituisce un valore booleano che indica se la prima espressione stringa contiene il secondo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="2ecc8-973">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-974">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-975">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-976">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-976">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-977">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-978">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-978">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-979">Nell'esempio seguente viene verificato se "abc" contiene "ab" e contiene "d".</span><span class="sxs-lookup"><span data-stu-id="2ecc8-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="2ecc8-980">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="2ecc8-981"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="2ecc8-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="2ecc8-982">Restituisce un valore booleano che indica se la prima espressione stringa termina con il secondo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="2ecc8-983">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-984">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-985">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-986">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-986">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-987">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-988">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-988">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-989">L'esempio seguente restituisce "abc" che termina con "b" e "bc".</span><span class="sxs-lookup"><span data-stu-id="2ecc8-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="2ecc8-990">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="2ecc8-991"><a name="bk_index_of"></a> INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="2ecc8-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="2ecc8-992">Restituisce la posizione iniziale della prima occorrenza della seconda stringa di espressione all'interno della prima espressione stringa specificata oppure -1 se la stringa non viene trovata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="2ecc8-993">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-994">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-995">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-996">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-996">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-997">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-998">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-998">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-999">L'esempio seguente restituisce l'indice di diverse sottostringhe all'interno di "abc".</span><span class="sxs-lookup"><span data-stu-id="2ecc8-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="2ecc8-1000">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="2ecc8-1001"><a name="bk_left"></a> LEFT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="2ecc8-1002">Restituisce la parte sinistra di una stringa con il numero specificato di caratteri.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="2ecc8-1003">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1004">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1005">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="2ecc8-1006">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1007">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1008">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1009">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1009">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1010">L'esempio seguente restituisce la parte sinistra di "abc" per diversi valori di lunghezza.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="2ecc8-1011">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="2ecc8-1012"><a name="bk_length"></a> LENGTH</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="2ecc8-1013">Restituisce il numero di caratteri dell'espressione stringa specificata.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1014">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1015">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1016">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1017">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1018">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1019">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1019">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1020">L'esempio seguente restituisce la lunghezza di una stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="2ecc8-1021">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="2ecc8-1022"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="2ecc8-1023">Restituisce un'espressione stringa dopo la conversione di dati in caratteri maiuscoli in caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="2ecc8-1024">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1025">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1026">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1027">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1028">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1029">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1029">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1030">L'esempio seguente illustra come usare LOWER in una query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="2ecc8-1031">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="2ecc8-1032"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="2ecc8-1033">Restituisce un'espressione stringa dopo aver rimosso gli spazi vuoti iniziali.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="2ecc8-1034">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1035">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1036">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1037">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1038">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1039">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1039">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1040">L'esempio seguente illustra come usare LTRIM all'interno di una query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="2ecc8-1041">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="2ecc8-1042"><a name="bk_replace"></a> REPLACE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="2ecc8-1043">Sostituisce tutte le occorrenze di un valore stringa specificato con un altro valore stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="2ecc8-1044">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1045">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1046">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1047">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1048">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1049">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1049">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1050">L'esempio seguente illustra come usare REPLACE in una query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="2ecc8-1051">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="2ecc8-1052"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="2ecc8-1053">Ripete un valore stringa in un numero di volte specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="2ecc8-1054">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1055">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1056">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="2ecc8-1057">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1058">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1059">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1060">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1060">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1061">L'esempio seguente illustra come usare REPLICATE in una query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="2ecc8-1062">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="2ecc8-1063"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="2ecc8-1064">Restituisce l'inverso di un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="2ecc8-1065">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1066">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1067">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1068">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1069">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1070">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1070">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1071">L'esempio seguente illustra come usare REVERSE in una query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="2ecc8-1072">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="2ecc8-1073"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="2ecc8-1074">Restituisce la parte destra di una stringa con il numero specificato di caratteri.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="2ecc8-1075">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1076">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1077">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="2ecc8-1078">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1079">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1080">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1081">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1081">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1082">L'esempio seguente restituisce la parte destra di "abc" per diversi valori di lunghezza.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="2ecc8-1083">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="2ecc8-1084"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="2ecc8-1085">Restituisce un'espressione di stringa dopo aver rimosso gli spazi vuoti finali.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="2ecc8-1086">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1087">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1088">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1089">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1090">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1091">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1091">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1092">L'esempio seguente illustra come usare RTRIM all'interno di una query.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="2ecc8-1093">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="2ecc8-1094"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="2ecc8-1095">Restituisce un valore booleano che indica se la prima espressione stringa inizia con il secondo.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="2ecc8-1096">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1097">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1098">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1099">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1100">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1101">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1101">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1102">L'esempio seguente verifica se la stringa "abc" inizia con "b" e "a".</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="2ecc8-1103">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="2ecc8-1104"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="2ecc8-1105">Restituisce parte di un'espressione stringa a partire dalla posizione in base al carattere zero specificata e continua fino alla lunghezza specificata o alla fine della stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="2ecc8-1106">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="2ecc8-1107">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1108">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="2ecc8-1109">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1110">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1111">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1112">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1112">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1113">L'esempio seguente restituisce la sottostringa di "abc" a partire da 1 e per una lunghezza di 1 carattere.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="2ecc8-1114">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="2ecc8-1115"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="2ecc8-1116">Restituisce un'espressione stringa dopo aver convertito i caratteri minuscoli in caratteri maiuscoli.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="2ecc8-1117">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1118">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="2ecc8-1119">È qualsiasi espressione di stringa valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1120">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1121">Restituisce un'espressione di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1122">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1122">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1123">L'esempio seguente illustra come usare UPPER in una query</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="2ecc8-1124">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="2ecc8-1125"><a name="bk_array_functions"></a> Funzioni di matrice</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="2ecc8-1126">Le funzioni scalari seguenti eseguono un'operazione su un valore di input di matrice e restituiscono un valore numerico, booleano o matrice</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="2ecc8-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="2ecc8-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="2ecc8-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="2ecc8-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="2ecc8-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="2ecc8-1132">Restituisce una matrice che rappresenta il risultato della concatenazione di due o più valori della matrice.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="2ecc8-1133">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="2ecc8-1134">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="2ecc8-1135">È qualsiasi espressione di matrice valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1136">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1137">Restituisce un'espressione di matrice.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1138">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1138">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1139">L'esempio seguente illustra come concatenare due matrici.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="2ecc8-1140">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="2ecc8-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="2ecc8-1142">Restituisce un valore booleano che indica se la matrice contiene il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="2ecc8-1143">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="2ecc8-1144">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="2ecc8-1145">È qualsiasi espressione di matrice valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="2ecc8-1146">È qualsiasi espressione valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1147">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1148">Restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="2ecc8-1149">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1149">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1150">L'esempio seguente illustra come verificare l'appartenenza a una matrice usando ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="2ecc8-1151">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="2ecc8-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="2ecc8-1153">Restituisce il numero di elementi dell'espressione di matrice specificato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1154">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1155">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="2ecc8-1156">È qualsiasi espressione di matrice valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1157">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1158">Restituisce un'espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1159">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1159">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1160">L'esempio seguente illustra come ottenere la lunghezza di una matrice usando ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="2ecc8-1161">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="2ecc8-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="2ecc8-1163">Restituisce parte di un'espressione di matrice.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="2ecc8-1164">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="2ecc8-1165">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="2ecc8-1166">È qualsiasi espressione di matrice valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="2ecc8-1167">È qualsiasi espressione numerica valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1168">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1169">Restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="2ecc8-1170">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1170">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1171">L'esempio seguente illustra come ottenere una parte di una matrice usando ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="2ecc8-1172">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="2ecc8-1173"><a name="bk_spatial_functions"></a> Funzioni spaziali</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="2ecc8-1174">Le seguenti funzioni scalari eseguono un'operazione su un valore di input di oggetto spaziale e restituiscono un valore numerico o booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="2ecc8-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="2ecc8-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="2ecc8-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="2ecc8-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="2ecc8-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="2ecc8-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="2ecc8-1181">Restituisce la distanza tra le due espressioni GeoJSON punto, poligono o LineString.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="2ecc8-1182">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1183">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="2ecc8-1184">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1185">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1186">Restituisce un'espressione numerica che contiene la distanza.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="2ecc8-1187">È espressa in metri per il sistema di riferimento predefinito.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="2ecc8-1188">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1188">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1189">L'esempio seguente indica come restituire tutti i documenti della famiglia che si trovano entro 30 km dalla posizione specificata usando la funzione predefinita ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="2ecc8-1190">.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="2ecc8-1191">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="2ecc8-1192"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="2ecc8-1193">Restituisce un'espressione booleana che indica se l'oggetto GeoJSON (punto, poligono o LineString) specificato nel primo argomento è all'interno dell'oggetto GeoJSON (punto, poligono o LineString) nel secondo argomento.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="2ecc8-1194">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1195">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="2ecc8-1196">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="2ecc8-1197">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1198">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1199">Restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="2ecc8-1200">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1200">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1201">L'esempio seguente indica come trovare tutti i documenti della famiglia all'interno di un poligono usando ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="2ecc8-1202">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="2ecc8-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="2ecc8-1204">Restituisce un'espressione booleana che indica se l'oggetto GeoJSON (punto, poligono o LineString) specificato nel primo argomento interseca l'oggetto GeoJSON (punto, poligono o LineString) nel secondo argomento.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="2ecc8-1205">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1206">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="2ecc8-1207">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="2ecc8-1208">È qualsiasi espressione di oggetto punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1209">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1210">Restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="2ecc8-1211">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1211">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1212">L'esempio seguente indica come individuare tutte le aree che intersecano il poligono dato.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="2ecc8-1213">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="2ecc8-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="2ecc8-1215">Restituisce un valore booleano che indica se l'espressione GeoJSON punto, poligono o LineString specificata è valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="2ecc8-1216">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1217">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="2ecc8-1218">È qualsiasi espressione di punto GeoJSON, poligono o LineString valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1219">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1220">Restituisce un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1221">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1221">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1222">Nell'esempio seguente viene illustrato come controllare se un punto è valido usando ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="2ecc8-1223">Ad esempio, questo punto ha un valore di latitudine che non rientra nell'intervallo valido di valori [-90, 90], quindi la query restituisce false.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="2ecc8-1224">Per i poligoni, la specifica GeoJSON richiede che l'ultima coppia di coordinate indicata corrisponda alla prima, in modo da creare una forma chiusa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="2ecc8-1225">I punti all'interno di un poligono devono essere specificati in senso antiorario.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="2ecc8-1226">Un poligono specificato in senso orario rappresenta l'inverso dell'area al suo interno.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="2ecc8-1227">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="2ecc8-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="2ecc8-1229">Restituisce un valore JSON che contiene un valore booleano valore se l'espressione GeoJSON punto, poligono o LineString specificata è valida e, se non valida, anche il motivo come valore stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="2ecc8-1230">**Sintassi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="2ecc8-1231">**Argomenti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="2ecc8-1232">È qualsiasi espressione di punto GeoJSON o poligono valida.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="2ecc8-1233">**Tipi restituiti**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="2ecc8-1234">Restituisce un valore JSON che contiene un valore booleano valore se l'espressione punto o poligono GeoJSON specificata è valida e, se non valida, anche il motivo come valore stringa.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="2ecc8-1235">**esempi**</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1235">**Examples**</span></span>  
  
 <span data-ttu-id="2ecc8-1236">Nell'esempio seguente viene illustrato come controllare la validità (con i dettagli) usando ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="2ecc8-1237">Questo è il set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="2ecc8-1238">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1238">Next steps</span></span>  
 <span data-ttu-id="2ecc8-1239">[Query e sintassi SQL per Azure Cosmos DB](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="2ecc8-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="2ecc8-1240">Documentazione di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2ecc8-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
