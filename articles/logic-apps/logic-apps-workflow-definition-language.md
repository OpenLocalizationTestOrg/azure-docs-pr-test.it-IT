---
title: lo schema RDL aaaWorkflow - App Azure per la logica | Documenti Microsoft
description: Definire i flussi di lavoro basati sullo schema di definizione del flusso di lavoro hello per le app di logica di Azure
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Schema del linguaggio di definizione del flusso di lavoro per App per la logica di Azure

Una definizione del flusso di lavoro contiene la logica effettiva hello che viene eseguita come parte dell'app logica. Questa definizione include uno o più trigger per avviare hello logica app e uno o più azioni per hello logica app tootake.  
  
## <a name="basic-workflow-definition-structure"></a>Struttura di base della definizione del flusso di lavoro

Struttura di base hello di una definizione del flusso di lavoro è:  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> Hello [API REST di gestione del flusso di lavoro](https://docs.microsoft.com/rest/api/logic/workflows) documentazione con informazioni su come toocreate e gestire i flussi di lavoro di logica dell'applicazione.
  
|Nome dell'elemento|Obbligatorio|Descrizione|  
|------------------|--------------|-----------------|  
|$schema|No|Specifica il percorso di hello per file di schema hello JSON che descrive una versione di hello del linguaggio di definizione hello. Questo percorso è obbligatorio quando si fa riferimento esternamente a una definizione. Per questo documento, il percorso di hello è: <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|No|Specifica la versione della definizione hello. Quando si distribuisce un flusso di lavoro mediante la definizione di hello, è possibile utilizzare questo valore toomake che viene utilizzato definizione destra hello.|  
|parameters|No|Specifica i parametri utilizzati dati tooinput nella definizione di hello. È possibile definire un massimo di 50 parametri.|  
|trigger|No|Specifica le informazioni per i trigger hello iniziare hello flusso di lavoro. È possibile definire un massimo di 10 trigger.|  
|Azioni|No|Specifica le azioni effettuate durante l'esecuzione di flusso hello. È possibile definire un massimo di 250 azioni.|  
|outputs|No|Specifica le informazioni sulle risorse hello distribuito. È possibile definire un massimo di 10 output.|  
  
## <a name="parameters"></a>parameters

In questa sezione specifica tutti i parametri di hello utilizzati nella definizione del flusso di lavoro hello in fase di distribuzione. Tutti i parametri devono essere dichiarati in questa sezione prima di poter essere usati in altre sezioni della definizione di hello.  
  
Hello seguente illustra la struttura hello di una definizione di parametro:  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|Nome dell'elemento|Obbligatorio|Descrizione|  
|------------------|--------------|-----------------|  
|type|Sì|**Tipo**: string <p> **Dichiarazione**: `"parameters": {"parameter1": {"type": "string"}` <p> **Specifiche**: `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Tipo**: securestring <p> **Dichiarazione**: `"parameters": {"parameter1": {"type": "securestring"}}` <p> **Specifiche**: `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Tipo**: int <p> **Dichiarazione**: `"parameters": {"parameter1": {"type": "int"}}` <p> **Specifiche**: `"parameters": {"parameter1": {"value" : 5}}` <p> **Tipo**: bool <p> **Dichiarazione**: `"parameters": {"parameter1": {"type": "bool"}}` <p> **Specifiche**: `"parameters": {"parameter1": { "value": true }}` <p> **Tipo**: array <p> **Dichiarazione**: `"parameters": {"parameter1": {"type": "array"}}` <p> **Specifiche**: `"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **Tipo**: object <p> **Dichiarazione**: `"parameters": {"parameter1": {"type": "object"}}` <p> **Specifiche**: `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Tipo**: secureobject <p> **Dichiarazione**: `"parameters": {"parameter1": {"type": "object"}}` <p> **Specifiche**: `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Nota:** hello `securestring` e `secureobject` tipi non vengono restituiti `GET` operazioni. Tutte le password, le chiavi e i segreti devono usare questo tipo.|  
|defaultValue|No|Specifica il valore predefinito hello per il parametro hello quando viene specificato alcun valore in fase di hello hello risorsa sia stata creata.|  
|allowedValues|No|Specifica una matrice di valori consentiti per il parametro hello.|  
|metadata|No|Specifica informazioni aggiuntive sul parametro hello, ad esempio una descrizione leggibile o in fase di progettazione dati utilizzati da Visual Studio o altri strumenti.|  
  
Questo esempio viene illustrato come è possibile utilizzare un parametro nella sezione corpo hello di un'azione:  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 I parametri possono essere usati anche negli output.  
  
## <a name="triggers-and-actions"></a>Trigger e azioni  

Azioni e trigger specificano chiamate hello che possono prendere parte all'esecuzione del flusso di lavoro. Per informazioni dettagliate su questa sezione, vedere [Workflow Actions and Triggers](logic-apps-workflow-actions-triggers.md) (Azioni e trigger dei flussi di lavoro).
  
## <a name="outputs"></a>outputs  

Gli output specificano le informazioni che possono essere restituite da un'esecuzione del flusso di lavoro. Ad esempio, se si dispone di uno stato specifico o un valore che si desidera tootrack per ogni esecuzione, è possibile includere dati in hello eseguire output. dati Hello viene visualizzato nel hello API REST di gestione per tale esecuzione in Gestione hello dell'interfaccia utente per tale sequenza di hello portale di Azure. È inoltre possibile trasmettere questi sistemi esterni tooother di output come Power BI per la creazione di dashboard. Gli output sono *non* utilizzato toorespond tooincoming richieste su hello API REST del servizio. richiesta in ingresso tooan toorespond utilizzando hello `response` tipo di azione, di seguito è riportato un esempio:
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|Nome dell'elemento|Obbligatorio|Descrizione|  
|------------------|--------------|-----------------|  
|key1|Sì|Specifica l'identificatore di chiave per l'output di hello hello. Sostituire **key1** con un nome che si desidera l'output di hello tooidentify toouse.|  
|value|Sì|Specifica il valore di hello dell'output di hello.|  
|type|Sì|Specifica il tipo di hello per valore hello che è stato specificato. Ecco alcuni tipi possibili di valori: <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>Espressioni  

I valori JSON nella definizione di hello possono essere letterali o possono essere espressioni che vengono valutate quando la definizione di hello viene utilizzata. ad esempio:  
  
```json
"name": "value"
```

 oppure  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> Alcune espressioni ottengono i rispettivi valori dalle azioni di runtime che potrebbero non esistere all'inizio di hello dell'esecuzione di hello. È possibile utilizzare **funzioni** toohelp recuperare alcuni di questi valori.  
  
Le espressioni possono trovarsi in qualsiasi punto in un valore stringa JSON e restituiscono sempre un altro valore JSON. Quando un valore JSON è stato determinato toobe un'espressione, il corpo di hello dell'espressione hello viene estratto rimuovendo hello chiocciola (@). Se è necessaria una stringa letterale che inizia con @, occorre che la stringa sia preceduta da un carattere di escape con @@. Hello esempi seguenti viene illustrato come le espressioni vengono valutate.  
  
|Valore JSON|Risultato|  
|----------------|------------|  
|"parameters"|vengono restituiti Hello caratteri 'parameters'.|  
|"parameters[1]"|vengono restituiti Hello caratteri 'parameters [1]'.|  
|"@@"|Viene restituita una stringa da 1 carattere che contiene '@'.|  
|" @"|Viene restituita una stringa da 2 caratteri che contiene ' @'.|  
  
Con l'*interpolazione della stringa* è possibile inserire le espressioni anche all'interno delle stringhe in cui viene eseguito il wrapping delle espressioni in `@{ ... }`. ad esempio: <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

il risultato di Hello è sempre una stringa, che rende questo toohello simili funzionalità `concat` (funzione). Si supponga di avere definito `myNumber` come `42` e `myString` come `sampleString`:  
  
|Valore JSON|Risultato|  
|----------------|------------|  
|"@parameters('myString')"|Restituisce `sampleString` come stringa.|  
|"@{parameters('myString')}"|Restituisce `sampleString` come stringa.|  
|"@parameters('myNumber')"|Restituisce `42` come *numero*.|  
|"@{parameters('myNumber')}"|Restituisce `42` come *stringa*.|  
|"Answer is: @{parameters('myNumber')}"|Restituisce hello stringa `Answer is: 42`.|  
|"@concat('Answer is: ', string(parameters('myNumber')))"|Restituisce la stringa hello`Answer is: 42`|  
|"Answer is: @@{parameters('myNumber')}"|Restituisce hello stringa `Answer is: @{parameters('myNumber')}`.|  
  
## <a name="operators"></a>Operatori  

Gli operatori sono caratteri hello che è possibile utilizzare all'interno di espressioni o funzioni. 
  
|operatore|Descrizione|  
|--------------|-----------------|  
|.|operatore punto Hello consente tooreference proprietà di un oggetto|  
|?|operatore punto interrogativo Hello consente di fare riferimento alle proprietà null di un oggetto senza un errore di runtime. Ad esempio, è possibile utilizzare questo null toohandle espressione attivare output: <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|virgoletta singola Hello è hello solo modo toowrap i valori letterali stringa. Non è possibile utilizzare le virgolette doppie all'interno di espressioni questo punteggiatura in conflitto con l'offerta JSON hello che esegue il wrapping hello intera espressione.|  
|[]|Hello racchiusa tra parentesi quadre possono essere utilizzati tooget un valore da una matrice con un indice specifico. Ad esempio, se si dispone di un'azione che passa `range(0,10)`in toohello `forEach` funzione, è possibile utilizzare questo elementi tooget funzione out di matrici:  <p>`myArray[item()]`|  
  
## <a name="functions"></a>Funzioni  

È anche possibile chiamare le funzioni all'interno delle espressioni. Hello nella tabella seguente mostra le funzioni hello che possono essere utilizzate in un'espressione.  
  
|Expression|Versione di valutazione|  
|----------------|----------------|  
|"@function('Hello')"|Chiamate hello membro funzione del definizione hello con la stringa letterale hello Hello come primo parametro hello.|  
|"@function('It's Cool!')"|Chiama il membro di funzione hello della definizione di hello con la stringa letterale hello 'It's Cool!' come primo parametro hello|  
|"@function().prop1"|Valore della proprietà prop1 hello hello di hello restituisce `myfunction` membro della definizione di hello.|  
|"@function('Hello').prop1"|Chiamate hello membro funzione della definizione di hello con la stringa letterale hello 'Hello' come hello primo parametro e restituisce hello proprietà prop1 dell'oggetto hello.|  
|"@function(parameters('Hello'))"|Restituisce il parametro Hello hello e passa hello valore toofunction|  
  
### <a name="referencing-functions"></a>Funzioni di riferimento  

È possibile utilizzare questi output tooreference funzioni da altre azioni nel hello logica app o i valori passati in quando hello logica app è stata creata. Ad esempio, è possibile fare riferimento dati hello da un unico passaggio toouse in un altro.  
  
|Nome della funzione|Descrizione|  
|-------------------|-----------------|  
|parameters|Restituisce un valore di parametro definito nella definizione di hello. <p>`parameters('password')` <p> **Numero di parametro**: 1 <p> **Nome**: Parameter <p> **Descrizione**: obbligatoria. nome Hello del parametro hello i cui valori desiderati.|  
|action|Consente a un'espressione tooderive il relativo valore da altro nome JSON e coppie di valore o l'output di hello dell'azione di runtime corrente hello. proprietà Hello rappresentata da propertyPath nel seguente esempio hello è facoltativa. Se non viene specificato propertyPath, riferimento hello è toohello azione intero oggetto. Questa funzione può essere usata solo all'interno delle condizioni do-until di un'azione. <p>`action().outputs.body.propertyPath`|  
|Azioni|Consente a un'espressione tooderive il relativo valore da altro nome JSON e coppie di valore o l'output di hello dell'azione di runtime hello. Queste espressioni dichiarano esplicitamente che un'azione dipende da un'altra azione. proprietà Hello rappresentata da propertyPath nel seguente esempio hello è facoltativa. Se non viene specificato propertyPath, riferimento hello è toohello azione intero oggetto. È possibile utilizzare questo elemento di uno o hello condizioni dipendenze toospecify elemento, ma non è necessario toouse entrambi per hello stessa risorsa dipendente. <p>`actions('myAction').outputs.body.propertyPath` <p> **Numero di parametro**: 1 <p> **Nome**: ActionName <p> **Descrizione**: obbligatoria. nome di Hello dell'azione di hello i cui valori desiderati. <p> Sono disponibili proprietà sull'oggetto azione hello: <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Vedere hello [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=850646) per informazioni dettagliate su tali proprietà.|
|trigger|Consente a un'espressione tooderive il relativo valore da altro nome JSON e coppie di valore o l'output di hello di trigger CLR hello. proprietà Hello rappresentata da propertyPath nel seguente esempio hello è facoltativa. Se non viene specificato propertyPath, riferimento hello è oggetto intero trigger toohello. <p>`trigger().outputs.body.propertyPath` <p>Quando utilizzato all'interno di input di un trigger, funzione hello restituisce gli output di hello dell'esecuzione precedente hello. Tuttavia, quando utilizzato in condizione di un trigger, hello `trigger` funzione restituisce l'output di hello di esecuzione corrente di hello. <p> Sono disponibili proprietà sull'oggetto trigger hello: <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Vedere hello [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=850644) per informazioni dettagliate su tali proprietà.|
|actionOutputs|Questa funzione è la sintassi abbreviata per `actions('actionName').outputs` <p> **Numero di parametro**: 1 <p> **Nome**: ActionName <p> **Descrizione**: obbligatoria. nome di Hello dell'azione di hello i cui valori desiderati.|  
|actionBody e body|Queste funzioni sono la sintassi abbreviata per `actions('actionName').outputs.body` <p> **Numero di parametro**: 1 <p> **Nome**: ActionName <p> **Descrizione**: obbligatoria. nome di Hello dell'azione di hello i cui valori desiderati.|  
|triggerOutputs|Questa funzione è la sintassi abbreviata per `trigger().outputs`|  
|triggerBody|Questa funzione è la sintassi abbreviata per `trigger().outputs.body`|  
|item|Quando utilizzato all'interno di un'azione ripetuta, questa funzione restituisce l'elemento hello nella matrice di hello per l'iterazione dell'azione hello. Se ad esempio è presente un'azione che viene eseguita per ogni elemento in una matrice di messaggi, è possibile usare questa sintassi: <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>Funzioni di raccolta  

Queste funzioni vengono applicate alle raccolte e si applicano in genere tooArrays, stringhe e talvolta dizionari.  
  
|Nome della funzione|Descrizione|  
|-------------------|-----------------|  
|contains|Restituisce true se un dizionario contiene una chiave, se un elenco contiene un valore o se una stringa contiene una sottostringa. Ad esempio, questa funzione restituisce `true`: <p>`contains('abacaba','aca')` <p> **Numero di parametro**: 1 <p> **Nome**: WithinCollection <p> **Descrizione**: obbligatoria. Hello raccolta toosearch all'interno. <p> **Numero di parametro**: 2 <p> **Nome**: FindObject <p> **Descrizione**: obbligatoria. Hello toofind oggetto all'interno di hello **insieme**.|  
|length|Restituisce hello numero di elementi in una matrice o stringa. Ad esempio, questa funzione restituisce `3`:  <p>`length('abc')` <p> **Numero di parametro**: 1 <p> **Nome**: Collection <p> **Descrizione**: obbligatoria. raccolta di Hello per quali lunghezza hello tooget.|  
|empty|Restituisce true se la matrice, la stringa o l'oggetto è vuoto. Ad esempio, questa funzione restituisce `true`: <p>`empty('')` <p> **Numero di parametro**: 1 <p> **Nome**: Collection <p> **Descrizione**: obbligatoria. Se è vuota, Hello toocheck insieme.|  
|intersezione|Restituisce una singola matrice o un singolo oggetto con elementi comuni tra le matrici o gli oggetti passati. Ad esempio, questa funzione restituisce `[1, 2]`: <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>parametri di Hello per la funzione hello possono essere un set di oggetti o un set di matrici (non una combinazione di entrambi). Se sono presenti due oggetti con hello stesso nome, l'ultimo oggetto di hello con tale nome viene visualizzata nell'oggetto finale di hello. <p> **Numero parametro**: 1 ... *n* <p> **Nome**: Collection *n* <p> **Descrizione**: obbligatoria. tooevaluate raccolte Hello. Un oggetto deve essere in tutte le raccolte passate tooappear nel risultato hello.|  
|union|Restituisce una matrice o un oggetto con tutti gli elementi di hello nella matrice o oggetto funzione toothis passati. Ad esempio, questa funzione restituisce `[1, 2, 3, 10, 101]`: <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>parametri di Hello per la funzione hello possono essere un set di oggetti o un set di matrici (non una combinazione,). Se sono presenti due oggetti con hello stesso nome nell'output finale hello, nell'oggetto finale hello hello oggetto ultimo con lo stesso nome. <p> **Numero parametro**: 1 ... *n* <p> **Nome**: Collection *n* <p> **Descrizione**: obbligatoria. tooevaluate raccolte Hello. Oggetto che viene visualizzato in una delle raccolte hello viene visualizzato anche nel risultato hello.|  
|first|Restituisce hello primo elemento nella matrice hello o stringa passata. Ad esempio, questa funzione restituisce `0`: <p>`first([0,2,3])` <p> **Numero di parametro**: 1 <p> **Nome**: Collection <p> **Descrizione**: obbligatoria. Hello raccolta tootake hello primo oggetto da.|  
|last|Restituisce hello l'ultimo elemento nella matrice hello o stringa passata. Ad esempio, questa funzione restituisce `3`: <p>`last('0123')` <p> **Numero di parametro**: 1 <p> **Nome**: Collection <p> **Descrizione**: obbligatoria. Hello tootake hello ultimo oggetto raccolta da.|  
|take|Restituisce hello innanzitutto **conteggio** gli elementi di matrice hello o una stringa passata. Ad esempio, questa funzione restituisce `[1, 2]`:  <p>`take([1, 2, 3, 4], 2)` <p> **Numero di parametro**: 1 <p> **Nome**: Collection <p> **Descrizione**: obbligatoria. raccolta di Hello da dove tootake hello innanzitutto **conteggio** oggetti. <p> **Numero di parametro**: 2 <p> **Nome**: Count <p> **Descrizione**: obbligatoria. numero di oggetti tootake da hello Hello **raccolta**. Deve essere un intero positivo.|  
|skip|Restituisce gli elementi nella matrice hello a partire dall'indice di hello **conteggio**. Ad esempio, questa funzione restituisce `[3, 4]`: <p>`skip([1, 2 ,3 ,4], 2)` <p> **Numero di parametro**: 1 <p> **Nome**: Collection <p> **Descrizione**: obbligatoria. Hello hello tooskip raccolta innanzitutto **conteggio** oggetti da. <p> **Numero di parametro**: 2 <p> **Nome**: Count <p> **Descrizione**: obbligatoria. numero di oggetti tooremove dalla parte anteriore hello di Hello **raccolta**. Deve essere un intero positivo.|  
|join|Restituisce una stringa con ogni elemento di una matrice unito da un delimitatore. Ad esempio questo valore restituisce `"1,2,3,4"`:<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **Numero di parametro**: 1<br /><br /> **Nome**: Collection<br /><br /> **Descrizione**: obbligatoria. elementi di toojoin Hello insieme di.<br /><br /> **Numero di parametro**: 2<br /><br /> **Nome**: Delimiter<br /><br /> **Descrizione**: obbligatoria. elementi toodelimit di stringa Hello con.|  
  
### <a name="string-functions"></a>Funzioni stringa

Hello solo le funzioni seguenti si applica toostrings. È anche possibile usare alcune funzioni di raccolta sulle stringhe.  
  
|Nome della funzione|Descrizione|  
|-------------------|-----------------|  
|concat|Combina un numero qualsiasi di stringhe. Se ad esempio il parametro 1 è `p1`, questa funzione restituisce `somevalue-p1-somevalue`: <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **Numero parametro**: 1 ... *n* <p> **Nome**: String *n* <p> **Descrizione**: obbligatoria. Hello toocombine di stringhe in un'unica stringa.|  
|substring|Restituisce un sottoinsieme di caratteri da una stringa. Ad esempio, questa funzione restituisce `abc`: <p>`substring('somevalue-abc-somevalue',10,3)` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa Hello da quale hello verrà prelevata sottostringa. <p> **Numero di parametro**: 2 <p> **Nome**: StartIndex <p> **Descrizione**: obbligatoria. indice di Hello di in cui inizia la sottostringa hello nel parametro 1. <p> **Numero di parametro**: 3 <p> **Nome**: Length <p> **Descrizione**: obbligatoria. lunghezza Hello della sottostringa di hello.|  
|replace|Sostituisce una stringa con una stringa specifica. Ad esempio, questa funzione restituisce `hello new string`: <p>`replace('hello old string', 'old', 'new')` <p> **Numero di parametro**: 1 <p> **Nome**: string <p> **Descrizione**: obbligatoria. stringa Hello che viene eseguita la ricerca per il parametro 2 e aggiornato con il parametro 3, quando il parametro 2 è stato trovato nel parametro 1. <p> **Numero di parametro**: 2 <p> **Nome**: OldString <p> **Descrizione**: obbligatoria. Hello tooreplace stringa con il parametro 3, quando viene trovata una corrispondenza nel parametro 1 <p> **Numero di parametro**: 3 <p> **Nome**: NewString <p> **Descrizione**: obbligatoria. Hello stringa che rappresenta stringa hello tooreplace utilizzato nel parametro 2 quando viene trovata una corrispondenza nel parametro 1.|  
|guid|Questa funzione genera una stringa univoca globale (GUID). Ad esempio, questa funzione può generare questo GUID: `c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **Numero di parametro**: 1 <p> **Nome**: Format <p> **Descrizione**: facoltativa. Identificatore di formato singolo che indica [come tooformat hello valore di questo Guid](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx). il parametro di formato Hello può essere "N", "D", "B", "P" o "X". Se il valore format non viene specificato, viene usato "D".|  
|toLower|Converte una stringa di toolowercase. Ad esempio, questa funzione restituisce `two by two is four`: <p>`toLower('Two by Two is Four')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. Hello stringa tooconvert toolower maiuscole e minuscole. Se un carattere nella stringa hello non ha un equivalente in caratteri minuscoli, carattere hello è incluso invariato nella stringa restituita hello.|  
|toUpper|Converte una stringa di toouppercase. Ad esempio, questa funzione restituisce `TWO BY TWO IS FOUR`: <p>`toUpper('Two by Two is Four')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. Hello stringa tooconvert tooupper maiuscole e minuscole. Se un carattere nella stringa hello non ha un equivalente in caratteri maiuscoli, caratteri hello sono incluso invariato nella stringa restituita hello.|  
|indexof|Trovare hello l'indice di un valore all'interno di una stringa di maiuscole e minuscole. Ad esempio, questa funzione restituisce `7`: <p>`indexof('hello, world.', 'world')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa Hello che può contenere il valore di hello. <p> **Numero di parametro**: 2 <p> **Nome**: String <p> **Descrizione**: obbligatoria. Hello toosearch hello indice del valore di.|  
|lastindexof|Trovare hello l'ultimo indice di un valore all'interno di una stringa di maiuscole e minuscole. Ad esempio, questa funzione restituisce `3`: <p>`lastindexof('foofoo', 'foo')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa Hello che può contenere il valore di hello. <p> **Numero di parametro**: 2 <p> **Nome**: String <p> **Descrizione**: obbligatoria. Hello toosearch hello indice del valore di.|  
|startswith|Controlla se la stringa hello inizia con un caso di valore e minuscole. Ad esempio, questa funzione restituisce `true`: <p>`startswith('hello, world', 'hello')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa Hello che può contenere il valore di hello. <p> **Numero di parametro**: 2 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa hello del valore Hello può iniziare con.|  
|endswith|Controlla se la stringa hello termina con un caso di valore e minuscole. Ad esempio, questa funzione restituisce `true`: <p>`endswith('hello, world', 'world')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa Hello che può contenere il valore di hello. <p> **Numero di parametro**: 2 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa hello del valore Hello può terminare con.|  
|split|Suddivide una stringa hello utilizzando un separatore. Ad esempio, questa funzione restituisce `["a", "b", "c"]`: <p>`split('a;b;c',';')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa Hello divisa. <p> **Numero di parametro**: 2 <p> **Nome**: String <p> **Descrizione**: obbligatoria. separatore Hello.|  
  
### <a name="logical-functions"></a>Funzioni logiche  

Queste funzioni sono utili all'interno di condizioni e possono essere qualsiasi tipo di logica di tooevaluate utilizzati.  
  
|Nome della funzione|Descrizione|  
|-------------------|-----------------|  
|equals|Restituisce true se due valori sono uguali. Se ad esempio parameter1 è someValue, questa funzione restituisce `true`: <p>`equals(parameters('parameter1'), 'someValue')` <p> **Numero di parametro**: 1 <p> **Nome**: Object 1 <p> **Descrizione**: obbligatoria. Hello toocompare oggetto troppo**oggetto 2**. <p> **Numero di parametro**: 2 <p> **Nome**: Object 2 <p> **Descrizione**: obbligatoria. Hello toocompare oggetto troppo**1 oggetto**.|  
|less|Restituisce true se il primo argomento hello è minore di hello secondo. Si noti che i valori possono essere solo di tipo intero, a virgola mobile o stringa. Ad esempio, questa funzione restituisce `true`: <p>`less(10,100)` <p> **Numero di parametro**: 1 <p> **Nome**: Object 1 <p> **Descrizione**: obbligatoria. Hello toocheck oggetto se è minore di **oggetto 2**. <p> **Numero di parametro**: 2 <p> **Nome**: Object 2 <p> **Descrizione**: obbligatoria. Hello toocheck oggetto se è maggiore di **1 oggetto**.|  
|lessOrEquals|Restituisce true se hello primo argomento è minore o uguale a toohello secondo. Si noti che i valori possono essere solo di tipo intero, a virgola mobile o stringa. Ad esempio, questa funzione restituisce `true`: <p>`lessOrEquals(10,10)` <p> **Numero di parametro**: 1 <p> **Nome**: Object 1 <p> **Descrizione**: obbligatoria. Hello toocheck oggetto se è minore o uguale a troppo**oggetto 2**. <p> **Numero di parametro**: 2 <p> **Nome**: Object 2 <p> **Descrizione**: obbligatoria. Hello toocheck oggetto se è maggiore o uguale a troppo**1 oggetto**.|  
|greater|Restituisce true se il primo argomento hello è maggiore di hello secondo. Si noti che i valori possono essere solo di tipo intero, a virgola mobile o stringa. Ad esempio, questa funzione restituisce `false`:  <p>`greater(10,10)` <p> **Numero di parametro**: 1 <p> **Nome**: Object 1 <p> **Descrizione**: obbligatoria. Hello toocheck oggetto se è maggiore di **oggetto 2**. <p> **Numero di parametro**: 2 <p> **Nome**: Object 2 <p> **Descrizione**: obbligatoria. Hello toocheck oggetto se è minore di **1 oggetto**.|  
|greaterOrEquals|Restituisce true se il primo argomento hello è maggiore o uguale toohello secondo. Si noti che i valori possono essere solo di tipo intero, a virgola mobile o stringa. Ad esempio, questa funzione restituisce `false`: <p>`greaterOrEquals(10,100)` <p> **Numero di parametro**: 1 <p> **Nome**: Object 1 <p> **Descrizione**: obbligatoria. Hello toocheck oggetto se è maggiore o uguale a troppo**oggetto 2**. <p> **Numero di parametro**: 2 <p> **Nome**: Object 2 <p> **Descrizione**: obbligatoria. Hello toocheck oggetto se è minore o uguale troppo**1 oggetto**.|  
|e|Restituisce true se entrambi i parametri sono true. Entrambi gli argomenti devono toobe booleani. Ad esempio, questa funzione restituisce `false`: <p>`and(greater(1,10),equals(0,0))` <p> **Numero di parametro**: 1 <p> **Nome**: Boolean 1 <p> **Descrizione**: obbligatoria. primo argomento che deve essere Hello `true`. <p> **Numero di parametro**: 2 <p> **Nome**: Boolean 2 <p> **Descrizione**: obbligatoria. Hello secondo argomento deve essere `true`.|  
|oppure|Restituisce true se uno dei parametri è true. Entrambi gli argomenti devono toobe booleani. Ad esempio, questa funzione restituisce `true`: <p>`or(greater(1,10),equals(0,0))` <p> **Numero di parametro**: 1 <p> **Nome**: Boolean 1 <p> **Descrizione**: obbligatoria. primo argomento che può essere Hello `true`. <p> **Numero di parametro**: 2 <p> **Nome**: Boolean 2 <p> **Descrizione**: obbligatoria. Hello secondo argomento può essere `true`.|  
|not|Restituisce true se i parametri di hello sono `false`. Entrambi gli argomenti devono toobe booleani. Ad esempio, questa funzione restituisce `true`: <p>`not(contains('200 Success','Fail'))` <p> **Numero di parametro**: 1 <p> **Nome**: Boolean <p> **Descrizione**: restituisce true se i parametri di hello sono `false`. Entrambi gli argomenti devono toobe booleani. Questa funzione restituisce `true`: `not(contains('200 Success','Fail'))`|  
|if|Restituisce un valore specificato in base che ha prodotto espressione hello `true` o `false`.  Ad esempio, questa funzione restituisce `"yes"`: <p>`if(equals(1, 1), 'yes', 'no')` <p> **Numero di parametro**: 1 <p> **Nome**: Expression <p> **Descrizione**: obbligatoria. Deve restituire un valore booleano che determina quale espressione hello di valore. <p> **Numero di parametro**: 2 <p> **Nome**: True <p> **Descrizione**: obbligatoria. Hello tooreturn valore se l'espressione hello è `true`. <p> **Numero di parametro**: 3 <p> **Nome**: False <p> **Descrizione**: obbligatoria. Hello tooreturn valore se l'espressione hello è `false`.|  
  
### <a name="conversion-functions"></a>Funzioni di conversione  

Queste funzioni sono utilizzati tooconvert tra ognuno dei tipi nativi di hello in linguaggio hello:  
  
- string  
  
- numero intero  
  
- float  
  
- boolean  
  
- matrici  
  
- dizionari  

-   form  
  
|Nome della funzione|Descrizione|  
|-------------------|-----------------|  
|int|Converte un valore integer tooan parametro hello. Ad esempio, questa funzione restituisce 100 sotto forma di numero, invece di una stringa: <p>`int('100')` <p> **Numero di parametro**: 1 <p> **Nome**: Value <p> **Descrizione**: obbligatoria. Hello valore integer convertito tooan.|  
|string|Convertire una stringa di tooa parametro hello. Ad esempio, questa funzione restituisce `'10'`: <p>`string(10)` <p>È anche possibile convertire una stringa tooa oggetto. Ad esempio, se hello `myPar` parametro è un oggetto con una proprietà `abc : xyz`, questa funzione restituisce `{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **Numero di parametro**: 1 <p> **Nome**: Value <p> **Descrizione**: obbligatoria. Hello valore stringa tooa convertito.|  
|json|Convertire valore del tipo JSON tooa parametro hello ed è hello opposto di `string()`. Ad esempio, questa funzione restituisce `[1,2,3]` come matrice, invece di una stringa: <p>`json('[1,2,3]')` <p>Analogamente, è possibile convertire un oggetto tooan di stringa. Ad esempio, questa funzione restituisce `{ "abc" : "xyz" }`: <p>`json('{"abc" : "xyz"}')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. Hello stringa che rappresenta il valore di tipo nativo tooa convertito. <p>Hello `json()` funzione supporta il XML di input troppo. Ad esempio, hello valore del parametro: <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>viene convertito toothis JSON: <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|float|Convertire numero a virgola mobile tooa argomento parametro hello. Ad esempio, questa funzione restituisce `10.333`: <p>`float('10.333')` <p> **Numero di parametro**: 1 <p> **Nome**: Value <p> **Descrizione**: obbligatoria. Hello valore che rappresenta numero a virgola mobile tooa convertito.|  
|bool|Convertire hello parametro tooa valore booleano. Ad esempio, questa funzione restituisce `false`: <p>`bool(0)` <p> **Numero di parametro**: 1 <p> **Nome**: Value <p> **Descrizione**: obbligatoria. valore convertito tooa Hello booleano.|  
|coalesce|Restituisce l'oggetto di non null prima di hello negli argomenti di hello passati. **Nota**: una stringa vuota non è Null. Se ad esempio i parametri 1 e 2 non sono definiti, questa funzione restituisce `fallback`:  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **Numero parametro**: 1 ... *n* <p> **Nome**: Object*n* <p> **Descrizione**: obbligatoria. Hello toocheck di oggetti per i valori null.|  
|base64|Restituisce hello rappresentazione base64 della stringa di input hello. Ad esempio, questa funzione restituisce `c29tZSBzdHJpbmc=`: <p>`base64('some string')` <p> **Numero di parametro**: 1 <p> **Nome**: String 1 <p> **Descrizione**: obbligatoria. Hello tooencode stringa in una rappresentazione base64.|  
|base64ToBinary|Restituisce una rappresentazione binaria di una stringa con codifica Base64. Ad esempio, questa funzione restituisce la rappresentazione binaria di hello di `some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa con codifica base64 Hello.|  
|base64ToString|Restituisce una rappresentazione di stringa di una stringa con codifica Based64. Ad esempio, questa funzione restituisce `some string`: <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. stringa con codifica base64 Hello.|  
|Binary|Restituisce una rappresentazione binaria di un valore.  Ad esempio, questa funzione restituisce una rappresentazione binaria di `some string`: <p>`binary('some string')` <p> **Numero di parametro**: 1 <p> **Nome**: Value <p> **Descrizione**: obbligatoria. Hello valore toobinary convertito.|  
|dataUriToBinary|Restituisce una rappresentazione binaria di un URI di dati. Ad esempio, questa funzione restituisce la rappresentazione binaria di hello di `some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. dati Hello rappresentazione toobinary tooconvert URI.|  
|dataUriToString|Restituisce una rappresentazione di stringa di un URI di dati. Ad esempio, questa funzione restituisce `some string`: <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numero di parametro**: 1 <p> **Nome**: String<p> **Descrizione**: obbligatoria. dati Hello rappresentazione tooString tooconvert URI.|  
|dataUri|Restituisce un URI di dati di un valore. Ad esempio, questa funzione restituisce questo URI di dati `text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=`: <p>`dataUri('some string')` <p> **Numero di parametro**: 1<p> **Nome**: Value<p> **Descrizione**: obbligatoria. toodata tooconvert Hello valore URI.|  
|decodeBase64|Restituisce una rappresentazione di stringa di una stringa di input con codifica Based64. Ad esempio, questa funzione restituisce `some string`: <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: restituisce una rappresentazione di stringa di una stringa di input con codifica Based64.|  
|encodeUriComponent|Stringa di hello escape-URL che viene passato. Ad esempio, questa funzione restituisce `You+Are%3ACool%2FAwesome`: <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. caratteri tooescape unsafe-URL di stringa Hello da.|  
|decodeUriComponent|Stringa di escape-URL-annullare hello che viene passato. Ad esempio, questa funzione restituisce `You Are:Cool/Awesome`: <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. Hello toodecode hello URL-unsafe caratteri della stringa da.|  
|decodeDataUri|Restituisce una rappresentazione binaria di una stringa di URI di dati di input. Ad esempio, questa funzione restituisce la rappresentazione binaria di hello di `some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numero di parametro**: 1 <p> **Nome**: String <p> **Descrizione**: obbligatoria. Hello dataURI toodecode in una rappresentazione binaria.|  
|uriComponent|Restituisce una rappresentazione con codifica URI di un valore. Ad esempio, questa funzione restituisce `You+Are%3ACool%2FAwesome`: <p>`uriComponent('You Are:Cool/Awesome')` <p> **Numero di parametro**: 1<p> **Nome**: String <p> **Descrizione**: obbligatoria. Hello toobe di stringa con codifica URI.|  
|uriComponentToBinary|Restituisce una rappresentazione binaria di una stringa con codifica URI. Ad esempio, questa funzione restituisce una rappresentazione binaria di `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Numero di parametro**: 1 <p> **Nome**: String<p> **Descrizione**: obbligatoria. stringa con codifica URI Hello.|  
|uriComponentToString|Restituisce una rappresentazione di stringa di una stringa con codifica URI. Ad esempio, questa funzione restituisce `You Are:Cool/Awesome`: <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Numero di parametro**: 1<p> **Nome**: String<p> **Descrizione**: obbligatoria. stringa con codifica URI Hello.|  
|xml|Restituisce una rappresentazione XML del valore di hello. Ad esempio, questa funzione restituisce contenuto XML rappresentato da `'\<name>Alan\</name>'`: <p>`xml('\<name>Alan\</name>')` <p>Hello `xml()` funzione supporta l'oggetto JSON di input troppo. Ad esempio, hello parametro `{ "abc": "xyz" }` viene convertito tooXML contenuto:`\<abc>xyz\</abc>` <p> **Numero di parametro**: 1<p> **Nome**: Value<p> **Descrizione**: obbligatoria. Hello valore tooconvert tooXML.|  
|xpath|Restituisce una matrice di nodi XML corrispondono hello espressione di xpath di un valore che restituisce espressioni xpath hello. <p> **Esempio 1** <p>Si supponga che il valore di hello del parametro `p1` è una rappresentazione di stringa di questo file XML: <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>Questo codice: `xpath(xml(parameters('p1'), '/lab/robot/name')` <p>Restituisce <p>`[ <name>R1</name>, <name>R2</name> ]` <p>Mentre questo codice: <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>Restituisce <p>`13` <p> <p> **Esempio 2** <p>Hello specificato dopo il contenuto XML: <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>Questo codice: `@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>O questo codice: <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>Restituisce <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>E questo codice: `@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>Restituisce <p>``xyz`` <p> **Numero di parametro**: 1 <p> **Nome**: Xml <p> **Descrizione**: obbligatoria. Hello XML nel quale tooevaluate hello XPath espressione. <p> **Numero di parametro**: 2 <p> **Nome**: XPath <p> **Descrizione**: obbligatoria. Hello tooevaluate di espressione XPath.|  
|array|Convertire una matrice di tooan parametro hello. Ad esempio, questa funzione restituisce `["abc"]`: <p>`array('abc')` <p> **Numero di parametro**: 1 <p> **Nome**: Value <p> **Descrizione**: obbligatoria. valore di Hello matrice tooan convertito.|
|createArray|Crea una matrice di parametri di hello. Ad esempio, questa funzione restituisce `["a", "c"]`: <p>`createArray('a', 'c')` <p> **Numero parametro**: 1 ... *n* <p> **Nome**: Any *n* <p> **Descrizione**: obbligatoria. Hello toocombine di valori in una matrice.|
|triggerFormDataValue|Restituisce un valore singolo che corrisponde al nome della chiave hello da dati del modulo o di output con codifica form trigger.  Se sono presenti più corrispondenze, verrà generato un errore.  Ad esempio, verranno restituito i seguenti hello `bar`:`triggerFormDataValue('foo')`<br /><br />**Numero di parametro**: 1<br /><br />**Nome**: KeyName<br /><br />**Descrizione**: obbligatoria. nome della chiave Hello di hello form dati valore tooreturn.|
|triggerFormDataMultiValues|Restituisce una matrice di valori corrispondenti al nome di chiave hello da dati del modulo o di output con codifica form trigger.  Ad esempio, verranno restituito i seguenti hello `["bar"]`:`triggerFormDataValue('foo')`<br /><br />**Numero di parametro**: 1<br /><br />**Nome**: KeyName<br /><br />**Descrizione**: obbligatoria. nome della chiave Hello hello dei dati del form valori tooreturn.|
|triggerMultipartBody|Restituisce hello corpo di una parte del trigger hello un output più parti.<br /><br />**Numero di parametro**: 1<br /><br />**Nome**: Index<br /><br />**Descrizione**: obbligatoria. indice di Hello di hello parte tooretrieve.|
|formDataValue|Restituisce un valore singolo che corrisponde al nome della chiave hello da dati del modulo o di output con codifica form azione.  Se sono presenti più corrispondenze, verrà generato un errore.  Ad esempio, verranno restituito i seguenti hello `bar`:`formDataValue('someAction', 'foo')`<br /><br />**Numero di parametro**: 1<br /><br />**Nome**: ActionName<br /><br />**Descrizione**: obbligatoria. nome Hello dell'azione di hello con dati del modulo di risposta codificati come form.<br /><br />**Numero di parametro**: 2<br /><br />**Nome**: KeyName<br /><br />**Descrizione**: obbligatoria. nome della chiave Hello di hello form dati valore tooreturn.|
|formDataMultiValues|Restituisce una matrice di valori corrispondenti al nome di chiave hello da dati del modulo o di output con codifica form azione.  Ad esempio, verranno restituito i seguenti hello `["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**Numero di parametro**: 1<br /><br />**Nome**: ActionName<br /><br />**Descrizione**: obbligatoria. nome Hello dell'azione di hello con dati del modulo di risposta codificati come form.<br /><br />**Numero di parametro**: 2<br /><br />**Nome**: KeyName<br /><br />**Descrizione**: obbligatoria. nome della chiave Hello hello dei dati del form valori tooreturn.|
|multipartBody|Restituisce hello corpo di una parte di un output più parti di un'azione.<br /><br />**Numero di parametro**: 1<br /><br />**Nome**: ActionName<br /><br />**Descrizione**: obbligatoria. nome Hello dell'azione di hello con una risposta multipart.<br /><br />**Numero di parametro**: 2<br /><br />**Nome**: Index<br /><br />**Descrizione**: obbligatoria. indice di Hello di hello parte tooretrieve.|

### <a name="math-functions"></a>Funzioni matematiche  

Queste funzioni possono essere usate per qualsiasi tipo di numero, ovvero **numeri interi** e **numeri a virgola mobile**.  
  
|Nome della funzione|Descrizione|  
|-------------------|-----------------|  
|add|Restituisce il risultato di hello dall'aggiunta di due numeri hello. Ad esempio, questa funzione restituisce `20.333`: <p>`add(10,10.333)` <p> **Numero di parametro**: 1 <p> **Nome**: Summand 1 <p> **Descrizione**: obbligatoria. Hello tooadd numero troppo**Summand 2**. <p> **Numero di parametro**: 2 <p> **Nome**: Summand 2 <p> **Descrizione**: obbligatoria. Hello tooadd numero troppo**Summand 1**.|  
|sub|Restituisce il risultato di hello dalla sottrazione di due numeri. Ad esempio, questa funzione restituisce `-0.333`: <p>`sub(10,10.333)` <p> **Numero di parametro**: 1 <p> **Nome**: Minuend <p> **Descrizione**: obbligatoria. numero di Hello **sottraendo** rimossa. <p> **Numero di parametro**: 2 <p> **Nome**: Subtrahend <p> **Descrizione**: obbligatoria. numero tooremove da hello Hello **minuendo**.|  
|mul|Restituisce il risultato di hello dalla moltiplicazione di due numeri hello. Ad esempio, questa funzione restituisce `103.33`: <p>`mul(10,10.333)` <p> **Numero di parametro**: 1 <p> **Nome**: Multiplicand 1 <p> **Descrizione**: obbligatoria. Hello numero toomultiply **2 moltiplicando** con. <p> **Numero di parametro**: 2 <p> **Nome**: Multiplicand 2 <p> **Descrizione**: obbligatoria. Hello numero toomultiply **moltiplicando 1** con.|  
|div|Restituisce il risultato di hello dalla divisione di due numeri hello. Ad esempio, questa funzione restituisce `1.0333`: <p>`div(10.333,10)` <p> **Numero di parametro**: 1 <p> **Nome**: Dividend <p> **Descrizione**: obbligatoria. Hello toodivide numero da hello **divisore**. <p> **Numero di parametro**: 2 <p> **Nome**: Divisor <p> **Descrizione**: obbligatoria. hello toodivide numero Hello **dividendo** da.|  
|mod|Restituisce il resto di hello dopo aver diviso due numeri di hello (modulo). Ad esempio, questa funzione restituisce `2`: <p>`mod(10,4)` <p> **Numero di parametro**: 1 <p> **Nome**: Dividend <p> **Descrizione**: obbligatoria. Hello toodivide numero da hello **divisore**. <p> **Numero di parametro**: 2 <p> **Nome**: Divisor <p> **Descrizione**: obbligatoria. hello toodivide numero Hello **dividendo** da. Dopo la divisione di hello, viene eseguito il resto di hello.|  
|Min|Sono disponibili due modelli diversi per chiamare questa funzione. <p>Qui `min` accetta una matrice, e restituisce la funzione hello `0`: <p>`min([0,1,2])` <p>In alternativa, questa funzione può accettare un elenco di valori delimitato da virgole e restituisce `0`: <p>`min(0,1,2)` <p> **Nota**: tutti i valori devono essere numeri, pertanto se il parametro hello è una matrice, matrice hello ha tooonly presentano un numero. <p> **Numero di parametro**: 1 <p> **Nome**: Collection o Value <p> **Descrizione**: obbligatoria. Una matrice di valore minimo di valori toofind hello o hello valore prima di un set. <p> **Numero di parametro**: 2 ... *n* <p> **Nome**: Value *n* <p> **Descrizione**: facoltativa. Se il primo parametro hello è un valore, è possibile passare valori aggiuntivi e hello minimo di tutti i valori passati viene restituito.|  
|max|Sono disponibili due modelli diversi per chiamare questa funzione. <p>Qui `max` accetta una matrice, e restituisce la funzione hello `2`: <p>`max([0,1,2])` <p>In alternativa, questa funzione può accettare un elenco di valori delimitato da virgole e restituisce `2`: <p>`max(0,1,2)` <p> **Nota**: tutti i valori devono essere numeri, pertanto se il parametro hello è una matrice, matrice hello ha tooonly presentano un numero. <p> **Numero di parametro**: 1 <p> **Nome**: Collection o Value <p> **Descrizione**: obbligatoria. Una matrice di valore massimo di valori toofind hello o hello valore prima di un set. <p> **Numero di parametro**: 2 ... *n* <p> **Nome**: Value *n* <p> **Descrizione**: facoltativa. Se il primo parametro hello è un valore, è possibile passare valori aggiuntivi e hello massimo di tutti i valori passati viene restituito.|  
|range|Genera una matrice di numeri interi a partire da un numero specifico. Definire lunghezza hello di hello matrice restituita. <p>Ad esempio, questa funzione restituisce `[3,4,5,6]`: <p>`range(3,4)` <p> **Numero di parametro**: 1 <p> **Nome**: StartIndex <p> **Descrizione**: obbligatoria. Hello primo intero hello matrice. <p> **Numero di parametro**: 2 <p> **Nome**: Count <p> **Descrizione**: obbligatoria. Questo valore è hello numero di numeri interi nella matrice hello.|  
|rand|Genera l'errore casuale integer all'interno di hello specificato intervallo (inclusivo solo nel primo end). Ad esempio, questa funzione può restituire `0` o "1": <p>`rand(0,2)` <p> **Numero di parametro**: 1 <p> **Nome**: Minimum <p> **Descrizione**: obbligatoria. intero più basso Hello che può essere restituito. <p> **Numero di parametro**: 2 <p> **Nome**: Maximum <p> **Descrizione**: obbligatoria. Questo valore è l'intero successivo hello dopo l'intero più elevato di hello che può essere restituito.|  
  
### <a name="date-functions"></a>Funzioni di data  
  
|Nome della funzione|Descrizione|  
|-------------------|-----------------|  
|utcnow|Restituisce hello timestamp corrente come stringa, ad esempio: `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **Numero di parametro**: 1 <p> **Nome**: Format <p> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").|  
|addseconds|Aggiunge un numero intero di secondi tooa stringa timestamp passato. numero di Hello di secondi può essere positivo o negativo. Per impostazione predefinita, il risultato di hello è una stringa in ISO 8601 formato ("o"), a meno che non viene fornito un identificatore di formato. Ad esempio, `2015-03-15T13:27:00Z`: <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **Numero di parametro**: 1 <p> **Nome**: Timestamp <p> **Descrizione**: obbligatoria. Stringa che contiene ora hello. <p> **Numero di parametro**: 2 <p> **Nome**: Seconds <p> **Descrizione**: obbligatoria. numero di Hello di tooadd secondi. Può essere negativo toosubtract secondi. <p> **Numero di parametro**: 3 <p> **Nome**: Format <p> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").|  
|addminutes|Aggiunge un numero intero di minuti tooa stringa timestamp passato. numero di Hello di minuti può essere positivo o negativo. Per impostazione predefinita, il risultato di hello è una stringa in ISO 8601 formato ("o"), a meno che non viene fornito un identificatore di formato. Ad esempio, `2015-03-15T14:00:36Z`: <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **Numero di parametro**: 1 <p> **Nome**: Timestamp <p> **Descrizione**: obbligatoria. Stringa che contiene ora hello. <p> **Numero di parametro**: 2 <p> **Nome**: Minutes <p> **Descrizione**: obbligatoria. numero di Hello di tooadd minuti. Può essere negativo toosubtract minuti. <p> **Numero di parametro**: 3 <p> **Nome**: Format <p> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").|  
|addhours|Aggiunge un numero intero di ore tooa stringa timestamp passato. numero di ore di Hello può essere positivo o negativo. Per impostazione predefinita, il risultato di hello è una stringa in ISO 8601 formato ("o"), a meno che non viene fornito un identificatore di formato. Ad esempio, `2015-03-16T01:27:36Z`: <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **Numero di parametro**: 1 <p> **Nome**: Timestamp <p> **Descrizione**: obbligatoria. Stringa che contiene ora hello. <p> **Numero di parametro**: 2 <p> **Nome**: Hours <p> **Descrizione**: obbligatoria. numero di Hello di tooadd ore. Può essere negativo toosubtract ore. <p> **Numero di parametro**: 3 <p> **Nome**: Format <p> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").|  
|adddays|Aggiunge un numero intero di giorni tooa stringa timestamp passato. numero di Hello di giorni può essere positivo o negativo. Per impostazione predefinita, il risultato di hello è una stringa in ISO 8601 formato ("o"), a meno che non viene fornito un identificatore di formato. Ad esempio, `2015-02-23T13:27:36Z`: <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **Numero di parametro**: 1 <p> **Nome**: Timestamp <p> **Descrizione**: obbligatoria. Stringa che contiene ora hello. <p> **Numero di parametro**: 2 <p> **Nome**: Days <p> **Descrizione**: obbligatoria. numero di Hello di tooadd giorni. Può essere negativo toosubtract giorni. <p> **Numero di parametro**: 3 <p> **Nome**: Format <p> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").|  
|formatDateTime|Restituisce una stringa con formato data. Per impostazione predefinita, il risultato di hello è una stringa in ISO 8601 formato ("o"), a meno che non viene fornito un identificatore di formato. Ad esempio, `2015-02-23T13:27:36Z`: <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **Numero di parametro**: 1 <p> **Nome**: Date <p> **Descrizione**: obbligatoria. Stringa che contiene la data di hello. <p> **Numero di parametro**: 2 <p> **Nome**: Format <p> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").|  
|startOfHour|Hello restituisce avviare di hello ora tooa stringa timestamp passato. Ad esempio, `2017-03-15T13:00:00Z`:<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **Numero di parametro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrizione**: obbligatoria. Questa è una stringa che contiene ora hello.<br /><br />**Numero di parametro**: 2<br /><br /> **Nome**: Format<br /><br /> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").|  
|startOfDay|Hello restituisce avviare di hello giorno tooa stringa timestamp passato. Ad esempio, `2017-03-15T00:00:00Z`:<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **Numero di parametro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrizione**: obbligatoria. Questa è una stringa che contiene ora hello.<br /><br />**Numero di parametro**: 2<br /><br /> **Nome**: Format<br /><br /> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").| 
|startOfMonth|Hello restituisce avviare di hello mese tooa stringa timestamp passato. Ad esempio, `2017-03-01T00:00:00Z`:<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Numero di parametro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrizione**: obbligatoria. Questa è una stringa che contiene ora hello.<br /><br />**Numero di parametro**: 2<br /><br /> **Nome**: Format<br /><br /> **Descrizione**: facoltativa. Entrambi un [singolo carattere identificatore di formato](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) o [modello di formato personalizzato](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) che indica come tooformat hello valore di questo timestamp. Se non è stato fornito alcun formato, viene utilizzato il formato ISO 8601 hello ("o").| 
|dayOfWeek|Restituisce hello componente giorno della settimana di un timestamp di stringa.  Domenica è 0, lunedì è 1 e così via. Ad esempio, `3`:<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **Numero di parametro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrizione**: obbligatoria. Questa è una stringa che contiene ora hello.| 
|dayOfMonth|Restituisce hello giorno del componente di mese di un timestamp di stringa. Ad esempio, `15`:<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Numero di parametro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrizione**: obbligatoria. Questa è una stringa che contiene ora hello.| 
|dayOfYear|Restituisce hello giorno del componente relativo all'anno di una stringa di timestamp. Ad esempio, `74`:<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **Numero di parametro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrizione**: obbligatoria. Questa è una stringa che contiene ora hello.| 
|ticks|Hello restituisce tick proprietà di un timestamp di stringa. Ad esempio, `1489603019`:<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **Numero di parametro**: 1<br /><br /> **Nome**: Timestamp<br /><br /> **Descrizione**: obbligatoria. Questa è una stringa che contiene ora hello.| 
  
### <a name="workflow-functions"></a>Funzioni del flusso di lavoro  

Queste funzioni consentono di ottenere informazioni su hello flusso di lavoro in fase di esecuzione.  
  
|Nome della funzione|Descrizione|  
|-------------------|-----------------|  
|listCallbackUrl|Restituisce un trigger di hello tooinvoke toocall stringa o un'azione. <p> **Nota**: questa funzione può essere usata solo in un oggetto **httpWebhook** e **apiConnectionWebhook**, non in un oggetto **manual**, **recurrence**, **http** o **apiConnection**. <p>Ad esempio, hello `listCallbackUrl()` risultato della funzione: <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|flusso di lavoro|Questa funzione fornisce tutti i dettagli di hello per hello flusso di lavoro in fase di esecuzione hello. <p> Sono disponibili proprietà sull'oggetto del flusso di lavoro hello: <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> valore di hello Hello `run` proprietà è un oggetto con le proprietà seguenti: <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>Vedere hello [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=525617) per informazioni dettagliate su tali proprietà.<p> Ad esempio, tooget hello nome di hello corrente eseguita, utilizzare hello `"@workflow().run.name"` espressione. |

## <a name="next-steps"></a>Passaggi successivi

[Azioni e trigger del flusso di lavoro](logic-apps-workflow-actions-triggers.md)
