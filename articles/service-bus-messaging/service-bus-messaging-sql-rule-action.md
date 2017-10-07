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
# <a name="sqlruleaction-syntax"></a>Sintassi di SQLRuleAction

Oggetto *SqlRuleAction* è un'istanza di hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classe e rappresenta set di azioni scritto nel linguaggio SQL basato su sintassi che viene eseguita in un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
In questo argomento elenca i dettagli sui hello la grammatica SQL di azione regola.  
  
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
  
## <a name="arguments"></a>Argomenti  
  
-   `<scope>`stringa facoltativa che indica di ambito hello di hello `<property_name>`. I valori validi sono `sys` o `user`. Hello `sys` valore indica l'ambito del sistema in cui `<property_name>` è un nome di proprietà pubblica di hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`indica l'ambito di utente in cui `<property_name>` è una chiave di hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dizionario. `user`ambito è l'ambito predefinito hello se `<scope>` non è specificato.  
  
### <a name="remarks"></a>Osservazioni  

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
  
     di seguito Hello sono esempi di costanti lungo:  
  
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
  
Costanti booleane sono rappresentate dalle parole chiave hello `TRUE` o `FALSE`. i valori Hello vengono archiviati come `System.Boolean`.  
  
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

- SET è utilizzato toocreate un nuovo valore di hello proprietà o l'aggiornamento di una proprietà esistente.
- Rimuovi sono tooremove utilizzata una proprietà.
- SET esegue la conversione implicita se possibile, quando il tipo di espressione hello e il tipo di proprietà esistente hello sono diversi.
- Se viene fatto riferimento a proprietà di sistema inesistenti, l'azione ha esito negativo.
- L'azione non ha invece esito negativo se viene fatto riferimento a proprietà utente inesistenti.
- Una proprietà inesistente utente viene valutata come "Sconosciuto" internamente, seguente hello stessa semantica [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) durante la valutazione degli operatori.

## <a name="next-steps"></a>Passaggi successivi

- [Classe SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [Classe SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
