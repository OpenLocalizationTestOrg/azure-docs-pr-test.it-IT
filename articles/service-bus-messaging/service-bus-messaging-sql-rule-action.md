---
title: riferimento alla sintassi aaaSQLRuleAction in Azure | Documenti Microsoft
description: Informazioni dettagliate sulla grammatica di SQLRuleAction.
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
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="57661-103">Sintassi di SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="57661-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="57661-104">Oggetto *SqlRuleAction* è un'istanza di hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classe e rappresenta set di azioni scritto nel linguaggio SQL basato su sintassi che viene eseguita in un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="57661-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="57661-105">In questo argomento elenca i dettagli sui hello la grammatica SQL di azione regola.</span><span class="sxs-lookup"><span data-stu-id="57661-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
## <a name="arguments"></a><span data-ttu-id="57661-106">Argomenti</span><span class="sxs-lookup"><span data-stu-id="57661-106">Arguments</span></span>  
  
-   <span data-ttu-id="57661-107">`<scope>`stringa facoltativa che indica di ambito hello di hello `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="57661-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="57661-108">I valori validi sono `sys` o `user`.</span><span class="sxs-lookup"><span data-stu-id="57661-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="57661-109">Hello `sys` valore indica l'ambito del sistema in cui `<property_name>` è un nome di proprietà pubblica di hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="57661-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="57661-110">`user`indica l'ambito di utente in cui `<property_name>` è una chiave di hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dizionario.</span><span class="sxs-lookup"><span data-stu-id="57661-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="57661-111">`user`ambito è l'ambito predefinito hello se `<scope>` non è specificato.</span><span class="sxs-lookup"><span data-stu-id="57661-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="57661-112">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="57661-112">Remarks</span></span>  

<span data-ttu-id="57661-113">Tooaccess un tentativo di una proprietà di sistema inesistente è un errore, mentre una proprietà di utente tooaccess inesistente un tentativo non è un errore.</span><span class="sxs-lookup"><span data-stu-id="57661-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="57661-114">Una proprietà utente inesistente viene invece valutata internamente come valore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="57661-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="57661-115">Un valore sconosciuto viene gestito in modo speciale durante la valutazione degli operatori.</span><span class="sxs-lookup"><span data-stu-id="57661-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="57661-116">property_name</span><span class="sxs-lookup"><span data-stu-id="57661-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="57661-117">Argomenti</span><span class="sxs-lookup"><span data-stu-id="57661-117">Arguments</span></span>  
 <span data-ttu-id="57661-118">`<regular_identifier>`è una stringa rappresentata dall'hello seguenti espressioni regolari:</span><span class="sxs-lookup"><span data-stu-id="57661-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="57661-119">L'espressione corrisponde a qualsiasi stringa che inizia con una lettera seguita da uno o più caratteri di sottolineatura/lettere/cifre.</span><span class="sxs-lookup"><span data-stu-id="57661-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="57661-120">`[:IsLetter:]` indica qualsiasi carattere Unicode classificato come lettera Unicode.</span><span class="sxs-lookup"><span data-stu-id="57661-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="57661-121">`System.Char.IsLetter(c)` restituisce `true` se `c` è una lettera Unicode.</span><span class="sxs-lookup"><span data-stu-id="57661-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="57661-122">`[:IsDigit:]` indica qualsiasi carattere Unicode classificato come cifra decimale.</span><span class="sxs-lookup"><span data-stu-id="57661-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="57661-123">`System.Char.IsDigit(c)` restituisce `true` se `c` è una cifra Unicode.</span><span class="sxs-lookup"><span data-stu-id="57661-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="57661-124">`<regular_identifier>` non può essere una parola chiave riservata.</span><span class="sxs-lookup"><span data-stu-id="57661-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="57661-125">`<delimited_identifier>` è qualsiasi stringa racchiusa tra parentesi quadra aperta e parentesi quadra chiusa ([]).</span><span class="sxs-lookup"><span data-stu-id="57661-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="57661-126">Una parentesi quadra chiusa è rappresentata con due parentesi quadre chiuse.</span><span class="sxs-lookup"><span data-stu-id="57661-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="57661-127">Hello negli esempi seguenti vengono `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="57661-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="57661-128">`<quoted_identifier>` è qualsiasi stringa racchiusa tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="57661-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="57661-129">Le virgolette doppie nell'identificatore sono rappresentate con due virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="57661-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="57661-130">Non è consigliabile toouse identificatori tra virgolette perché può facilmente essere confuso con una costante di stringa.</span><span class="sxs-lookup"><span data-stu-id="57661-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="57661-131">Usare se possibile un identificatore delimitato.</span><span class="sxs-lookup"><span data-stu-id="57661-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="57661-132">Hello seguito è riportato un esempio di `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="57661-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="57661-133">pattern</span><span class="sxs-lookup"><span data-stu-id="57661-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="57661-134">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="57661-134">Remarks</span></span>
  
 <span data-ttu-id="57661-135">`<pattern>` deve essere un'espressione valutata come stringa.</span><span class="sxs-lookup"><span data-stu-id="57661-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="57661-136">Viene utilizzato come modello per hello operatore LIKE.</span><span class="sxs-lookup"><span data-stu-id="57661-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="57661-137">Può contenere i caratteri jolly hello:</span><span class="sxs-lookup"><span data-stu-id="57661-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="57661-138">`%`: qualsiasi stringa di zero o più caratteri.</span><span class="sxs-lookup"><span data-stu-id="57661-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="57661-139">`_`: qualsiasi carattere singolo.</span><span class="sxs-lookup"><span data-stu-id="57661-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="57661-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="57661-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="57661-141">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="57661-141">Remarks</span></span>
  
 <span data-ttu-id="57661-142">`<escape_char>` deve essere un'espressione valutata come stringa di lunghezza 1.</span><span class="sxs-lookup"><span data-stu-id="57661-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="57661-143">È utilizzato come un carattere di escape per hello operatore LIKE.</span><span class="sxs-lookup"><span data-stu-id="57661-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="57661-144">Ad esempio, `property LIKE 'ABC\%' ESCAPE '\'` corrisponde a `ABC%` anziché a una stringa che inizia con `ABC`.</span><span class="sxs-lookup"><span data-stu-id="57661-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="57661-145">costante</span><span class="sxs-lookup"><span data-stu-id="57661-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="57661-146">Argomenti</span><span class="sxs-lookup"><span data-stu-id="57661-146">Arguments</span></span>  
  
-   <span data-ttu-id="57661-147">`<integer_constant>` è una stringa di numeri non racchiusi tra virgolette e non contenenti separatori decimali.</span><span class="sxs-lookup"><span data-stu-id="57661-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="57661-148">i valori Hello vengono archiviati come `System.Int64` internamente, e seguire hello stesso intervallo.</span><span class="sxs-lookup"><span data-stu-id="57661-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="57661-149">di seguito Hello sono esempi di costanti lungo:</span><span class="sxs-lookup"><span data-stu-id="57661-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="57661-150">`<decimal_constant>` è una stringa di numeri non racchiusi tra virgolette e contenente un separatore decimale.</span><span class="sxs-lookup"><span data-stu-id="57661-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="57661-151">i valori Hello vengono archiviati come `System.Double` internamente e seguire hello stesso intervallo/precisione.</span><span class="sxs-lookup"><span data-stu-id="57661-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="57661-152">In una versione futura, questo numero potrebbe essere archiviato in un dati diversi toosupport esatto numero la semantica dei tipi, è consigliabile non fare affidamento hello fatti hello sottostante è di tipo di dati `System.Double` per `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="57661-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="57661-153">Hello di seguito è riportati esempi di costanti decimali:</span><span class="sxs-lookup"><span data-stu-id="57661-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="57661-154">`<approximate_number_constant>` è un numero scritto in notazione scientifica.</span><span class="sxs-lookup"><span data-stu-id="57661-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="57661-155">i valori Hello vengono archiviati come `System.Double` internamente e seguire hello stesso intervallo/precisione.</span><span class="sxs-lookup"><span data-stu-id="57661-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="57661-156">di seguito Hello sono esempi di costanti numero approssimative di:</span><span class="sxs-lookup"><span data-stu-id="57661-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="57661-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="57661-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="57661-158">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="57661-158">Remarks</span></span>
  
<span data-ttu-id="57661-159">Costanti booleane sono rappresentate dalle parole chiave hello `TRUE` o `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="57661-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="57661-160">i valori Hello vengono archiviati come `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="57661-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="57661-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="57661-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="57661-162">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="57661-162">Remarks</span></span>
  
<span data-ttu-id="57661-163">Le costanti di tipo stringa sono racchiuse tra virgolette singole e includono qualsiasi carattere Unicode valido.</span><span class="sxs-lookup"><span data-stu-id="57661-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="57661-164">Le virgolette singole incorporate in una costante di tipo stringa sono rappresentate con due virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="57661-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="57661-165">funzione</span><span class="sxs-lookup"><span data-stu-id="57661-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="57661-166">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="57661-166">Remarks</span></span>  

<span data-ttu-id="57661-167">Hello `newid()` restituisce un **GUID** generati da hello `System.Guid.NewGuid()` metodo.</span><span class="sxs-lookup"><span data-stu-id="57661-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="57661-168">Hello `property(name)` funzione restituisce il valore di hello della proprietà hello a cui fa riferimento `name`.</span><span class="sxs-lookup"><span data-stu-id="57661-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="57661-169">Hello `name` valore può essere qualsiasi espressione valida che restituisce un valore stringa.</span><span class="sxs-lookup"><span data-stu-id="57661-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="57661-170">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="57661-170">Considerations</span></span>

- <span data-ttu-id="57661-171">SET è utilizzato toocreate un nuovo valore di hello proprietà o l'aggiornamento di una proprietà esistente.</span><span class="sxs-lookup"><span data-stu-id="57661-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="57661-172">Rimuovi sono tooremove utilizzata una proprietà.</span><span class="sxs-lookup"><span data-stu-id="57661-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="57661-173">SET esegue la conversione implicita se possibile, quando il tipo di espressione hello e il tipo di proprietà esistente hello sono diversi.</span><span class="sxs-lookup"><span data-stu-id="57661-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="57661-174">Se viene fatto riferimento a proprietà di sistema inesistenti, l'azione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="57661-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="57661-175">L'azione non ha invece esito negativo se viene fatto riferimento a proprietà utente inesistenti.</span><span class="sxs-lookup"><span data-stu-id="57661-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="57661-176">Una proprietà inesistente utente viene valutata come "Sconosciuto" internamente, seguente hello stessa semantica [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) durante la valutazione degli operatori.</span><span class="sxs-lookup"><span data-stu-id="57661-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57661-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57661-177">Next steps</span></span>

- [<span data-ttu-id="57661-178">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="57661-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="57661-179">Classe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="57661-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
