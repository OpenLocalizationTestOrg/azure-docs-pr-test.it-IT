---
title: Informazioni di riferimento sulla sintassi di SQLFilter nel bus di servizio di Azure | Microsoft Docs
description: Informazioni dettagliate sulla grammatica di SQLFilter.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: 3aaec8f9b6a3bbcf814f771405c3b589de6f7ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="9a8f0-103">Sintassi di SQLFilter</span><span class="sxs-lookup"><span data-stu-id="9a8f0-103">SQLFilter syntax</span></span>

<span data-ttu-id="9a8f0-104">*SqlFilter* è un'istanza della [classe SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) e rappresenta un'espressione filtro basata sul linguaggio SQL che viene valutata su una [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="9a8f0-104">A *SqlFilter* is an instance of the [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="9a8f0-105">Un SqlFilter supporta un sottoinsieme dello standard SQL-92.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="9a8f0-106">Questo argomento offre informazioni dettagliate sulla grammatica di SqlFilter.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-106">This topic lists details about SqlFilter grammar.</span></span>  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a><span data-ttu-id="9a8f0-107">Argomenti</span><span class="sxs-lookup"><span data-stu-id="9a8f0-107">Arguments</span></span>  
  
-   <span data-ttu-id="9a8f0-108">`<scope>` è una stringa facoltativa che indica l'ambito di `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="9a8f0-109">I valori validi sono `sys` o `user`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="9a8f0-110">Il valore `sys` indica l'ambito del sistema. In questo caso, `<property_name>` sarà il nome di una proprietà pubblica della [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="9a8f0-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="9a8f0-111">`user` indica l'ambito dell'utente. In questo caso, `<property_name>` sarà una chiave del dizionario della [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="9a8f0-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="9a8f0-112">Se l'argomento `<scope>` non è specificato, l'ambito predefinito è `user`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="9a8f0-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="9a8f0-113">Remarks</span></span>

<span data-ttu-id="9a8f0-114">Il tentativo di accedere a una proprietà di sistema inesistente costituisce un errore, mentre il tentativo di accedere a una proprietà utente inesistente non è un errore.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="9a8f0-115">Una proprietà utente inesistente viene invece valutata internamente come valore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="9a8f0-116">Un valore sconosciuto viene gestito in modo speciale durante la valutazione degli operatori.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="9a8f0-117">property_name</span><span class="sxs-lookup"><span data-stu-id="9a8f0-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="9a8f0-118">Argomenti</span><span class="sxs-lookup"><span data-stu-id="9a8f0-118">Arguments</span></span>  

 <span data-ttu-id="9a8f0-119">`<regular_identifier>` è una stringa rappresentata dall'espressione regolare seguente:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="9a8f0-120">L'espressione corrisponde a qualsiasi stringa che inizia con una lettera seguita da uno o più caratteri di sottolineatura/lettere/cifre.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="9a8f0-121">`[:IsLetter:]` indica qualsiasi carattere Unicode classificato come lettera Unicode.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="9a8f0-122">`System.Char.IsLetter(c)` restituisce `true` se `c` è una lettera Unicode.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="9a8f0-123">`[:IsDigit:]` indica qualsiasi carattere Unicode classificato come cifra decimale.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="9a8f0-124">`System.Char.IsDigit(c)` restituisce `true` se `c` è una cifra Unicode.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="9a8f0-125">`<regular_identifier>` non può essere una parola chiave riservata.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="9a8f0-126">`<delimited_identifier>` è qualsiasi stringa racchiusa tra parentesi quadra aperta e parentesi quadra chiusa ([]).</span><span class="sxs-lookup"><span data-stu-id="9a8f0-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="9a8f0-127">Una parentesi quadra chiusa è rappresentata con due parentesi quadre chiuse.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="9a8f0-128">Di seguito sono riportati esempi di `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="9a8f0-129">`<quoted_identifier>` è qualsiasi stringa racchiusa tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="9a8f0-130">Le virgolette doppie nell'identificatore sono rappresentate con due virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="9a8f0-131">Non è consigliabile usare identificatori racchiusi tra virgolette perché possono essere facilmente confusi con una costante di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="9a8f0-132">Usare se possibile un identificatore delimitato.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="9a8f0-133">Di seguito è riportato un esempio di `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="9a8f0-134">pattern</span><span class="sxs-lookup"><span data-stu-id="9a8f0-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9a8f0-135">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="9a8f0-135">Remarks</span></span>
  
<span data-ttu-id="9a8f0-136">`<pattern>` deve essere un'espressione valutata come stringa.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="9a8f0-137">Viene usato come modello per l'operatore LIKE</span><span class="sxs-lookup"><span data-stu-id="9a8f0-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="9a8f0-138">e può contenere i caratteri jolly seguenti.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="9a8f0-139">`%`: qualsiasi stringa di zero o più caratteri.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="9a8f0-140">`_`: qualsiasi carattere singolo.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="9a8f0-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="9a8f0-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9a8f0-142">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="9a8f0-142">Remarks</span></span>  

<span data-ttu-id="9a8f0-143">`<escape_char>` deve essere un'espressione valutata come stringa di lunghezza 1.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="9a8f0-144">Viene usato come carattere di escape per l'operatore LIKE.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="9a8f0-145">Ad esempio, `property LIKE 'ABC\%' ESCAPE '\'` corrisponde a `ABC%` anziché a una stringa che inizia con `ABC`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="9a8f0-146">costante</span><span class="sxs-lookup"><span data-stu-id="9a8f0-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="9a8f0-147">Argomenti</span><span class="sxs-lookup"><span data-stu-id="9a8f0-147">Arguments</span></span>  
  
-   <span data-ttu-id="9a8f0-148">`<integer_constant>` è una stringa di numeri non racchiusi tra virgolette e non contenenti separatori decimali.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="9a8f0-149">I valori sono archiviati internamente come `System.Int64` e seguono lo stesso intervallo.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="9a8f0-150">Questi sono esempi di costanti di tipo long:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="9a8f0-151">`<decimal_constant>` è una stringa di numeri non racchiusi tra virgolette e contenente un separatore decimale.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="9a8f0-152">I valori sono archiviati internamente come `System.Double` e seguono lo stesso intervallo e la stessa precisione.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="9a8f0-153">In una versione futura, questo numero potrebbe essere archiviato in un tipo di dati diverso per supportare una semantica numerica esatta e non dover quindi fare affidamento sul fatto che il tipo di dati sottostante per `<decimal_constant>` sia `System.Double`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="9a8f0-154">Di seguito sono riportati esempi di costanti decimali:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="9a8f0-155">`<approximate_number_constant>` è un numero scritto in notazione scientifica.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="9a8f0-156">I valori sono archiviati internamente come `System.Double` e seguono lo stesso intervallo e la stessa precisione.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="9a8f0-157">Di seguito sono riportati esempi di costanti numeriche approssimative:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="9a8f0-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="9a8f0-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="9a8f0-159">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="9a8f0-159">Remarks</span></span>  

<span data-ttu-id="9a8f0-160">Le costanti booleane sono rappresentate dalle parole chiave **TRUE** e **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="9a8f0-161">I valori sono archiviati come `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="9a8f0-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="9a8f0-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9a8f0-163">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="9a8f0-163">Remarks</span></span>  

<span data-ttu-id="9a8f0-164">Le costanti di tipo stringa sono racchiuse tra virgolette singole e includono qualsiasi carattere Unicode valido.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="9a8f0-165">Le virgolette singole incorporate in una costante di tipo stringa sono rappresentate con due virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="9a8f0-166">funzione</span><span class="sxs-lookup"><span data-stu-id="9a8f0-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="9a8f0-167">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="9a8f0-167">Remarks</span></span>
  
<span data-ttu-id="9a8f0-168">La funzione `newid()` restituisce un **System.Guid** generato dal metodo `System.Guid.NewGuid()`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="9a8f0-169">La funzione `property(name)` restituisce il valore della proprietà a cui viene fatto riferimento con `name`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="9a8f0-170">Il valore di `name` può essere qualsiasi espressione valida che restituisce un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="9a8f0-171">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="9a8f0-171">Considerations</span></span>
  
<span data-ttu-id="9a8f0-172">Tenere presente la semantica di [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) seguente:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="9a8f0-173">Nei nomi delle proprietà non viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="9a8f0-174">Gli operatori seguono la semantica di conversione implicita C#, quando possibile.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="9a8f0-175">Le proprietà di sistema sono proprietà pubbliche esposte in istanze di [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="9a8f0-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="9a8f0-176">Tenere presente la semantica di `IS [NOT] NULL` seguente:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="9a8f0-177">`property IS NULL` viene valutato come `true` se la proprietà non esiste o se il valore della proprietà è `null`.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="9a8f0-178">Semantica di valutazione delle proprietà</span><span class="sxs-lookup"><span data-stu-id="9a8f0-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="9a8f0-179">Il tentativo di valutare una proprietà di sistema inesistente genera un'eccezione [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception).</span><span class="sxs-lookup"><span data-stu-id="9a8f0-179">An attempt to evaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="9a8f0-180">Una proprietà non esistente verrà valutata internamente come **valore sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="9a8f0-181">Valutazione dei valori sconosciuti negli operatori aritmetici:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="9a8f0-182">Per gli operatori binari, se il lato sinistro e/o destro degli operandi viene valutato come **valore sconosciuto**, il risultato è un **valore sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="9a8f0-183">Per gli operatori unari, se un operando viene valutato come **valore sconosciuto**, il risultato è un **valore sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="9a8f0-184">Valutazione dei valori sconosciuti negli operatori di confronto binari:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="9a8f0-185">Se il lato sinistro e/o destro degli operandi viene valutato come **valore sconosciuto**, il risultato è un **valore sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="9a8f0-186">Valutazione dei valori sconosciuti in `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="9a8f0-187">Se qualsiasi operando viene valutato come **valore sconosciuto**, il risultato è un **valore sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-187">If any operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="9a8f0-188">Valutazione dei valori sconosciuti in `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="9a8f0-189">Se l'operando di sinistra viene valutato come **valore sconosciuto**, il risultato è un **valore sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-189">If the left operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="9a8f0-190">Valutazione dei valori sconosciuti nell'operatore **AND**:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-190">Unknown evaluation in **AND** operator:</span></span>  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 <span data-ttu-id="9a8f0-191">Valutazione dei valori sconosciuti nell'operatore **OR**:</span><span class="sxs-lookup"><span data-stu-id="9a8f0-191">Unknown evaluation in **OR** operator:</span></span>  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="9a8f0-192">Semantica di binding degli operatori</span><span class="sxs-lookup"><span data-stu-id="9a8f0-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="9a8f0-193">Gli operatori di confronto come `>`, `>=`, `<`, `<=`, `!=` e `=` seguono la stessa semantica dell'associazione di operatori C# nelle conversioni implicite e nelle promozioni del tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="9a8f0-194">Gli operatori aritmetici come `+`, `-`, `*`, `/` e `%` seguono la stessa semantica dell'associazione di operatori C# nelle conversioni implicite e nelle promozioni del tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="9a8f0-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a8f0-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9a8f0-195">Next steps</span></span>

- [<span data-ttu-id="9a8f0-196">Classe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="9a8f0-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="9a8f0-197">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="9a8f0-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)