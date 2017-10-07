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
# <a name="sqlfilter-syntax"></a>Sintassi di SQLFilter

Oggetto *SqlFilter* è un'istanza di hello [SqlFilter classe](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)e rappresenta un'espressione di filtro basato sul linguaggio SQL che viene valutata una [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). Un SqlFilter supporta un subset dello standard SQL-92 hello.  
  
 Questo argomento offre informazioni dettagliate sulla grammatica di SqlFilter.  
  
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
  
## <a name="arguments"></a>Argomenti  
  
-   `<scope>`stringa facoltativa che indica di ambito hello di hello `<property_name>`. I valori validi sono `sys` o `user`. Hello `sys` valore indica l'ambito del sistema in cui `<property_name>` è un nome di proprietà pubblica di hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`indica l'ambito di utente in cui `<property_name>` è una chiave di hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dizionario. `user`ambito è l'ambito predefinito hello se `<scope>` non è specificato.  
  
## <a name="remarks"></a>Osservazioni

Tooaccess un tentativo di una proprietà di sistema inesistente è un errore, mentre una proprietà di utente tooaccess inesistente un tentativo non è un errore. Una proprietà utente inesistente viene invece valutata internamente come valore sconosciuto. Un valore sconosciuto viene gestito in modo speciale durante la valutazione degli operatori.  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Argomenti  

 `<regular_identifier>`è una stringa rappresentata dall'hello seguenti espressioni regolari:  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
L'espressione corrisponde a qualsiasi stringa che inizia con una lettera seguita da uno o più caratteri di sottolineatura/lettere/cifre.  
  
`[:IsLetter:]` indica qualsiasi carattere Unicode classificato come lettera Unicode. `System.Char.IsLetter(c)` restituisce `true` se `c` è una lettera Unicode.  
  
`[:IsDigit:]` indica qualsiasi carattere Unicode classificato come cifra decimale. `System.Char.IsDigit(c)` restituisce `true` se `c` è una cifra Unicode.  
  
`<regular_identifier>` non può essere una parola chiave riservata.  
  
`<delimited_identifier>` è qualsiasi stringa racchiusa tra parentesi quadra aperta e parentesi quadra chiusa ([]). Una parentesi quadra chiusa è rappresentata con due parentesi quadre chiuse. Hello negli esempi seguenti vengono `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>` è qualsiasi stringa racchiusa tra virgolette doppie. Le virgolette doppie nell'identificatore sono rappresentate con due virgolette doppie. Non è consigliabile toouse identificatori tra virgolette perché può facilmente essere confuso con una costante di stringa. Usare se possibile un identificatore delimitato. Hello seguito è riportato un esempio di `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>pattern  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Osservazioni
  
`<pattern>` deve essere un'espressione valutata come stringa. Viene utilizzato come modello per hello operatore LIKE.      Può contenere i caratteri jolly hello:  
  
-   `%`: qualsiasi stringa di zero o più caratteri.  
  
-   `_`: qualsiasi carattere singolo.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Osservazioni  

`<escape_char>` deve essere un'espressione valutata come stringa di lunghezza 1. È utilizzato come un carattere di escape per hello operatore LIKE.  
  
 Ad esempio, `property LIKE 'ABC\%' ESCAPE '\'` corrisponde a `ABC%` anziché a una stringa che inizia con `ABC`.  
  
## <a name="constant"></a>costante  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Argomenti  
  
-   `<integer_constant>` è una stringa di numeri non racchiusi tra virgolette e non contenenti separatori decimali. i valori Hello vengono archiviati come `System.Int64` internamente, e seguire hello stesso intervallo.  
  
     Questi sono esempi di costanti di tipo long:  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>` è una stringa di numeri non racchiusi tra virgolette e contenente un separatore decimale. i valori Hello vengono archiviati come `System.Double` internamente e seguire hello stesso intervallo/precisione.  
  
     In una versione futura, questo numero potrebbe essere archiviato in un dati diversi toosupport esatto numero la semantica dei tipi, è consigliabile non fare affidamento hello fatti hello sottostante è di tipo di dati `System.Double` per `<decimal_constant>`.  
  
     Hello di seguito è riportati esempi di costanti decimali:  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>` è un numero scritto in notazione scientifica. i valori Hello vengono archiviati come `System.Double` internamente e seguire hello stesso intervallo/precisione. di seguito Hello sono esempi di costanti numero approssimative di:  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Osservazioni  

Costanti booleane sono rappresentate dalle parole chiave hello **TRUE** o **FALSE**. i valori Hello vengono archiviati come `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Osservazioni  

Le costanti di tipo stringa sono racchiuse tra virgolette singole e includono qualsiasi carattere Unicode valido. Le virgolette singole incorporate in una costante di tipo stringa sono rappresentate con due virgolette singole.  
  
## <a name="function"></a>funzione  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Osservazioni
  
Hello `newid()` restituisce un **GUID** generati da hello `System.Guid.NewGuid()` metodo.  
  
Hello `property(name)` funzione restituisce il valore di hello della proprietà hello a cui fa riferimento `name`. Hello `name` valore può essere qualsiasi espressione valida che restituisce un valore stringa.  
  
## <a name="considerations"></a>Considerazioni
  
Si consideri il seguente hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantica:  
  
-   Nei nomi delle proprietà non viene fatta distinzione tra maiuscole e minuscole.  
  
-   Gli operatori seguono la semantica di conversione implicita C#, quando possibile.  
  
-   Le proprietà di sistema sono proprietà pubbliche esposte in istanze di [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).  
  
    Si consideri il seguente hello `IS [NOT] NULL` semantica:  
  
    -   `property IS NULL`viene valutato come `true` se non esiste o non hello valore della proprietà delle proprietà hello è `null`.  
  
### <a name="property-evaluation-semantics"></a>Semantica di valutazione delle proprietà  
  
-   Un tentativo tooevaluate genera una proprietà di sistema non esiste un [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) eccezione.  
  
-   Una proprietà non esistente verrà valutata internamente come **valore sconosciuto**.  
  
 Valutazione dei valori sconosciuti negli operatori aritmetici:  
  
-   Per gli operatori binari, se uno hello sinistra / destra operandi viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.  
  
-   Per gli operatori unari, se un operando viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.  
  
 Valutazione dei valori sconosciuti negli operatori di confronto binari:  
  
-   Se uno hello sinistra / destra operandi viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.  
  
 Valutazione dei valori sconosciuti in `[NOT] LIKE`:  
  
-   Se qualsiasi operando viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.  
  
 Valutazione dei valori sconosciuti in `[NOT] IN`:  
  
-   Se l'operando sinistro hello viene valutato come **sconosciuto**, risultato hello è **sconosciuto**.  
  
 Valutazione dei valori sconosciuti nell'operatore **AND**:  
  
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
  
 Valutazione dei valori sconosciuti nell'operatore **OR**:  
  
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
  
### <a name="operator-binding-semantics"></a>Semantica di binding degli operatori
  
-   Gli operatori di confronto, ad esempio `>`, `>=`, `<`, `<=`, `!=`, e `=` seguire hello stessa semantica dell'operatore c# hello associazione dati di tipo promozioni e conversioni implicite.  
  
-   Operatori aritmetici, ad esempio `+`, `-`, `*`, `/`, e `%` seguire hello stessa semantica dell'operatore c# hello associazione dati di tipo promozioni e conversioni implicite.

## <a name="next-steps"></a>Passaggi successivi

- [Classe SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [Classe SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)