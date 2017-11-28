---
title: riferimento alla sintassi di SQLFilter Bus di servizio aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="6ad1e-103">Sintassi di SQLFilter</span><span class="sxs-lookup"><span data-stu-id="6ad1e-103">SQLFilter syntax</span></span>

<span data-ttu-id="6ad1e-104">Oggetto *SqlFilter* è un'istanza di hello [SqlFilter classe](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)e rappresenta un'espressione di filtro basato sul linguaggio SQL che viene valutata una [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="6ad1e-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="6ad1e-105">Un SqlFilter supporta un subset dello standard SQL-92 hello.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="6ad1e-106">Questo argomento offre informazioni dettagliate sulla grammatica di SqlFilter.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="6ad1e-107">Argomenti</span><span class="sxs-lookup"><span data-stu-id="6ad1e-107">Arguments</span></span>  
  
-   <span data-ttu-id="6ad1e-108">`<scope>`stringa facoltativa che indica di ambito hello di hello `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="6ad1e-109">I valori validi sono `sys` o `user`.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="6ad1e-110">Hello `sys` valore indica l'ambito del sistema in cui `<property_name>` è un nome di proprietà pubblica di hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="6ad1e-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="6ad1e-111">`user`indica l'ambito di utente in cui `<property_name>` è una chiave di hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dizionario.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="6ad1e-112">`user`ambito è l'ambito predefinito hello se `<scope>` non è specificato.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="6ad1e-113">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="6ad1e-113">Remarks</span></span>

<span data-ttu-id="6ad1e-114">Tooaccess un tentativo di una proprietà di sistema inesistente è un errore, mentre una proprietà di utente tooaccess inesistente un tentativo non è un errore.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="6ad1e-115">Una proprietà utente inesistente viene invece valutata internamente come valore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="6ad1e-116">Un valore sconosciuto viene gestito in modo speciale durante la valutazione degli operatori.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="6ad1e-117">property_name</span><span class="sxs-lookup"><span data-stu-id="6ad1e-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="6ad1e-118">Argomenti</span><span class="sxs-lookup"><span data-stu-id="6ad1e-118">Arguments</span></span>  

 <span data-ttu-id="6ad1e-119">`<regular_identifier>`è una stringa rappresentata dall'hello seguenti espressioni regolari:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="6ad1e-120">L'espressione corrisponde a qualsiasi stringa che inizia con una lettera seguita da uno o più caratteri di sottolineatura/lettere/cifre.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="6ad1e-121">`[:IsLetter:]` indica qualsiasi carattere Unicode classificato come lettera Unicode.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="6ad1e-122">`System.Char.IsLetter(c)` restituisce `true` se `c` è una lettera Unicode.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="6ad1e-123">`[:IsDigit:]` indica qualsiasi carattere Unicode classificato come cifra decimale.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="6ad1e-124">`System.Char.IsDigit(c)` restituisce `true` se `c` è una cifra Unicode.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="6ad1e-125">`<regular_identifier>` non può essere una parola chiave riservata.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="6ad1e-126">`<delimited_identifier>` è qualsiasi stringa racchiusa tra parentesi quadra aperta e parentesi quadra chiusa ([]).</span><span class="sxs-lookup"><span data-stu-id="6ad1e-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="6ad1e-127">Una parentesi quadra chiusa è rappresentata con due parentesi quadre chiuse.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="6ad1e-128">Hello negli esempi seguenti vengono `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="6ad1e-129">`<quoted_identifier>` è qualsiasi stringa racchiusa tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="6ad1e-130">Le virgolette doppie nell'identificatore sono rappresentate con due virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="6ad1e-131">Non è consigliabile toouse identificatori tra virgolette perché può facilmente essere confuso con una costante di stringa.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="6ad1e-132">Usare se possibile un identificatore delimitato.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="6ad1e-133">Hello seguito è riportato un esempio di `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="6ad1e-134">pattern</span><span class="sxs-lookup"><span data-stu-id="6ad1e-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="6ad1e-135">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="6ad1e-135">Remarks</span></span>
  
<span data-ttu-id="6ad1e-136">`<pattern>` deve essere un'espressione valutata come stringa.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="6ad1e-137">Viene utilizzato come modello per hello operatore LIKE.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="6ad1e-138">Può contenere i caratteri jolly hello:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="6ad1e-139">`%`: qualsiasi stringa di zero o più caratteri.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="6ad1e-140">`_`: qualsiasi carattere singolo.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="6ad1e-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="6ad1e-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="6ad1e-142">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="6ad1e-142">Remarks</span></span>  

<span data-ttu-id="6ad1e-143">`<escape_char>` deve essere un'espressione valutata come stringa di lunghezza 1.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="6ad1e-144">È utilizzato come un carattere di escape per hello operatore LIKE.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="6ad1e-145">Ad esempio, `property LIKE 'ABC\%' ESCAPE '\'` corrisponde a `ABC%` anziché a una stringa che inizia con `ABC`.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="6ad1e-146">costante</span><span class="sxs-lookup"><span data-stu-id="6ad1e-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="6ad1e-147">Argomenti</span><span class="sxs-lookup"><span data-stu-id="6ad1e-147">Arguments</span></span>  
  
-   <span data-ttu-id="6ad1e-148">`<integer_constant>` è una stringa di numeri non racchiusi tra virgolette e non contenenti separatori decimali.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="6ad1e-149">i valori Hello vengono archiviati come `System.Int64` internamente, e seguire hello stesso intervallo.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="6ad1e-150">Questi sono esempi di costanti di tipo long:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="6ad1e-151">`<decimal_constant>` è una stringa di numeri non racchiusi tra virgolette e contenente un separatore decimale.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="6ad1e-152">i valori Hello vengono archiviati come `System.Double` internamente e seguire hello stesso intervallo/precisione.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="6ad1e-153">In una versione futura, questo numero potrebbe essere archiviato in un dati diversi toosupport esatto numero la semantica dei tipi, è consigliabile non fare affidamento hello fatti hello sottostante è di tipo di dati `System.Double` per `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="6ad1e-154">Hello di seguito è riportati esempi di costanti decimali:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="6ad1e-155">`<approximate_number_constant>` è un numero scritto in notazione scientifica.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="6ad1e-156">i valori Hello vengono archiviati come `System.Double` internamente e seguire hello stesso intervallo/precisione.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="6ad1e-157">di seguito Hello sono esempi di costanti numero approssimative di:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="6ad1e-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="6ad1e-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="6ad1e-159">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="6ad1e-159">Remarks</span></span>  

<span data-ttu-id="6ad1e-160">Costanti booleane sono rappresentate dalle parole chiave hello **TRUE** o **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="6ad1e-161">i valori Hello vengono archiviati come `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="6ad1e-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="6ad1e-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="6ad1e-163">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="6ad1e-163">Remarks</span></span>  

<span data-ttu-id="6ad1e-164">Le costanti di tipo stringa sono racchiuse tra virgolette singole e includono qualsiasi carattere Unicode valido.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="6ad1e-165">Le virgolette singole incorporate in una costante di tipo stringa sono rappresentate con due virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="6ad1e-166">funzione</span><span class="sxs-lookup"><span data-stu-id="6ad1e-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="6ad1e-167">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="6ad1e-167">Remarks</span></span>
  
<span data-ttu-id="6ad1e-168">Hello `newid()` restituisce un **GUID** generati da hello `System.Guid.NewGuid()` metodo.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="6ad1e-169">Hello `property(name)` funzione restituisce il valore di hello della proprietà hello a cui fa riferimento `name`.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="6ad1e-170">Hello `name` valore può essere qualsiasi espressione valida che restituisce un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="6ad1e-171">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="6ad1e-171">Considerations</span></span>
  
<span data-ttu-id="6ad1e-172">Si consideri il seguente hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantica:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="6ad1e-173">Nei nomi delle proprietà non viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="6ad1e-174">Gli operatori seguono la semantica di conversione implicita C#, quando possibile.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="6ad1e-175">Le proprietà di sistema sono proprietà pubbliche esposte in istanze di [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="6ad1e-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="6ad1e-176">Si consideri il seguente hello `IS [NOT] NULL` semantica:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="6ad1e-177">`property IS NULL`viene valutato come `true` se non esiste o non hello valore della proprietà delle proprietà hello è `null`.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="6ad1e-178">Semantica di valutazione delle proprietà</span><span class="sxs-lookup"><span data-stu-id="6ad1e-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="6ad1e-179">Un tentativo tooevaluate genera una proprietà di sistema non esiste un [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) eccezione.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="6ad1e-180">Una proprietà non esistente verrà valutata internamente come **valore sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="6ad1e-181">Valutazione dei valori sconosciuti negli operatori aritmetici:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="6ad1e-182">Per gli operatori binari, se uno hello sinistra / destra operandi viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="6ad1e-183">Per gli operatori unari, se un operando viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="6ad1e-184">Valutazione dei valori sconosciuti negli operatori di confronto binari:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="6ad1e-185">Se uno hello sinistra / destra operandi viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="6ad1e-186">Valutazione dei valori sconosciuti in `[NOT] LIKE`:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="6ad1e-187">Se qualsiasi operando viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="6ad1e-188">Valutazione dei valori sconosciuti in `[NOT] IN`:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="6ad1e-189">Se l'operando sinistro hello viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="6ad1e-190">Valutazione dei valori sconosciuti nell'operatore **AND**:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="6ad1e-191">Valutazione dei valori sconosciuti nell'operatore **OR**:</span><span class="sxs-lookup"><span data-stu-id="6ad1e-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="6ad1e-192">Semantica di binding degli operatori</span><span class="sxs-lookup"><span data-stu-id="6ad1e-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="6ad1e-193">Gli operatori di confronto, ad esempio `>`, `>=`, `<`, `<=`, `!=`, e `=` seguire hello stessa semantica dell'operatore c# hello associazione dati di tipo promozioni e conversioni implicite.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="6ad1e-194">Operatori aritmetici, ad esempio `+`, `-`, `*`, `/`, e `%` seguire hello stessa semantica dell'operatore c# hello associazione dati di tipo promozioni e conversioni implicite.</span><span class="sxs-lookup"><span data-stu-id="6ad1e-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ad1e-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6ad1e-195">Next steps</span></span>

- [<span data-ttu-id="6ad1e-196">Classe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="6ad1e-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="6ad1e-197">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="6ad1e-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)