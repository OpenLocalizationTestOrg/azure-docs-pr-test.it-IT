---
title: criteri avanzati di gestione API aaaAzure | Documenti Microsoft
description: Informazioni su hello avanzate criteri disponibili per l'utilizzo in Gestione API di Azure.
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a>Criteri avanzati di gestione API
In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello. Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AdvancedPolicies"></a>Criteri avanzati  
  
-   [Flusso di controllo](api-management-advanced-policies.md#choose) : in modo condizionale istruzioni dei criteri in base ai risultati di hello di valutazione di hello Boolean applica [espressioni](api-management-policy-expressions.md).  
  
-   [Inoltro della richiesta](#ForwardRequest) -inoltra servizio back-end di hello richiesta toohello.

-   [Limita la concorrenza](#LimitConcurrency) -impedisce racchiuso tra i criteri di esecuzione di più di hello numero specificato di richieste in un momento.
  
-   [Log tooEvent Hub](#log-to-eventhub) -invia messaggi hello specificato formato tooan Hub di eventi definito da un'entità del Logger. 

-   [Simulare risposta](#mock-response) -esecuzione nella pipeline viene interrotta e restituisce una risposta simulata direttamente toohello chiamante.
  
-   [Ripetere](#Retry) -esecuzione di tentativi di hello racchiuso tra istruzioni dei criteri, se e fino a quando non viene soddisfatta la condizione hello. Esecuzione viene ripetuto in intervalli di tempo specificati hello e backup toohello specificato numero di tentativi.  
  
-   [Restituire una risposta](#ReturnResponse) -hello di esecuzione e restituisce pipeline interruzioni specificato risposta direttamente toohello chiamante. 
  
-   [Inviare una richiesta unidirezionale](#SendOneWayRequest) -invia una richiesta toohello URL specificato senza attendere una risposta.  
  
-   [Invio richiesta](#SendRequest) -invia una richiesta toohello URL specificato.  

-   [Impostazione del proxy HTTP](#SetHttpProxy) -consente le richieste di tooroute inoltrati tramite un proxy HTTP.  

-   [Impostare il metodo di richiesta](#SetRequestMethod) -consente di determinare il metodo HTTP hello toochange per una richiesta.  
  
-   [Impostare il codice di stato](#SetStatus) -toohello di codice stato HTTP hello modifiche valore specificato.  
  
-   [Imposta variabile](api-management-advanced-policies.md#set-variable): rende persistente un valore in una variabile di [contesto](api-management-policy-expressions.md#ContextVariables) denominata e consente di accedervi in un momento successivo.  

-   [Traccia](#Trace) -aggiunge una stringa hello [API controllo](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.  
  
-   [Attesa](#Wait) -attende racchiusi [richiesta di invio](api-management-advanced-policies.md#SendRequest), [ottenere valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey), o [flusso di controllo](api-management-advanced-policies.md#choose) toocomplete criteri prima di procedere.  
  
##  <a name="choose"></a>Flusso di controllo  
 Hello `choose` criteri si applicano criteri racchiuse costruiscono istruzioni in base hello risultato della valutazione di espressioni booleane, simile tooan if-then-else o un'opzione in un linguaggio di programmazione.  
  
###  <a name="ChoosePolicyStatement"></a>Istruzione del criterio  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 Hello il criterio di flusso di controllo deve contenere almeno un `<when/>` elemento. Hello `<otherwise/>` elemento è facoltativo. Le condizioni nella `<when/>` elementi vengono valutati nell'ordine di visualizzazione nel criterio hello. Le istruzioni del criterio racchiuse hello innanzitutto `<when/>` elemento con attributo di condizione `true` verranno applicate. Criteri racchiuso tra parentesi hello `<otherwise/>` elemento, se presente, verrà applicato se in tutti di hello `<when/>` sono attributi dell'elemento condizione `false`.  
  
### <a name="examples"></a>esempi  
  
####  <a name="ChooseExample"></a>Esempio  
 Hello esempio seguente viene illustrato un [set-variable](api-management-advanced-policies.md#set-variable) due criteri di flusso di controllo e i criteri.  
  
 Hello set variabile criteri si trovano in hello sezione in ingresso e crea un `isMobile` booleano [contesto](api-management-policy-expressions.md#ContextVariables) variabile impostata tootrue se hello `User-Agent` richiesta intestazione contiene testo hello `iPad` o `iPhone`.  
  
 criterio del flusso di controllo prima Hello è anche hello sezione in ingresso e applica in modo condizionale uno dei due [impostare il parametro di stringa di query](api-management-transformation-policies.md#SetQueryStringParameter) criteri in base al valore di hello di hello `isMobile` variabile di contesto.  
  
 criterio del flusso di controllo secondo Hello nella sezione in uscita hello e applica in modo condizionale hello [convertire XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) criteri quando `isMobile` è troppo`true`.  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a>Esempio  
 Questo esempio viene illustrato come tooperform contenuto applicando un filtro per la rimozione degli elementi di dati dalla risposta hello ricevuto dal servizio back-end hello quando si utilizza hello `Starter` prodotto. Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too34:30. Inizia dal 31:50 toosee Cenni preliminari [hello scuro Sky previsione API](https://developer.forecast.io/) utilizzato per questa dimostrazione.  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|choose|Elemento radice.|Sì|  
|when|Hello toouse condizione per hello `if` o `ifelse` parti di hello `choose` criteri. Se hello `choose` criteri ha più `when` sezioni, vengono valutati in sequenza. Una volta hello `condition` di un oggetto quando l'elemento restituisce troppo`true`e non per ulteriormente `when` condizioni vengono valutate.|Sì|  
|otherwise|Contiene hello criteri frammento toobe utilizzati se nessuna delle hello `when` condizioni restituiscono troppo`true`.|No|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|  
|---------------|-----------------|--------------|  
|condition="Boolean expression &#124; Boolean constant"|espressione booleana Hello o costante tooevaluated quando hello contenente `when` viene valutata l'istruzione dei criteri.|Sì|  
  
###  <a name="ChooseUsage"></a>Uso  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
##  <a name="ForwardRequest"></a>Inoltra richiesta  
 Hello `forward-request` criterio inoltra hello in arrivo richiesta toohello servizio back-end specificato nella richiesta di hello [contesto](api-management-policy-expressions.md#ContextVariables). Hello URL del servizio back-end specificato nel hello API [impostazioni](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) e può essere modificato utilizzando hello [impostare servizio back-end](api-management-transformation-policies.md) criteri.  
  
> [!NOTE]
>  Rimozione di richiesta di hello non vengono inoltrati criteri toohello back-end del servizio e hello nella sezione in uscita hello i risultati dei criteri vengono valutati immediatamente dopo il completamento di hello dei criteri di hello in hello in ingresso di sezione.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>Esempi  
  
#### <a name="example"></a>Esempio  
 Hello seguente criterio a livello di API inoltra tutte le richieste di servizio back-end toohello con un intervallo di timeout di 60 secondi.  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Esempio  
 Questo criterio a livello di operazione Usa hello `base` criteri back-end di elemento tooinherit hello dall'ambito di livello padre API hello.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Esempio  
 Questo criterio a livello di operazione in modo esplicito inoltra tutte le richieste toohello back-end del servizio con un timeout di 120 e non eredita padre hello criteri livello back-end dell'API.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Esempio  
 Questo criterio a livello di operazione non inoltra le richieste di servizio back-end toohello.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|forward-request|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|timeout="integer"|intervallo di timeout Hello in secondi prima del servizio back-end di hello chiamata toohello ha esito negativo.|No|No timeout|  
|follow-redirects="true &#124; false"|Specifica se i reindirizzamenti dal servizio back-end hello sono seguiti dal gateway hello o restituiti toohello chiamante.|No|false|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** back-end  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
##  <a name="LimitConcurrency"></a>Limita concorrenza  
 Hello `limit-concurrency` criteri impedisce l'esecuzione di più di hello numero specificato di richieste in un determinato momento criteri tra parentesi. In caso di superamento limite hello, le nuove richieste vengono aggiunti tooa coda, fino a raggiungere hello lunghezza massima della coda. Al momento di esaurimento della coda, le nuove richieste avranno immediatamente esito negativo.
  
###  <a name="LimitConcurrencyStatement"></a>Istruzione del criterio  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>esempi  
  
####  <a name="ChooseExample"></a>Esempio  
 Hello esempio seguente viene illustrato come toolimit numero di richieste inoltrate back-end tooa in base al valore di hello di una variabile di contesto.
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|    
|limita concorrenza|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|--------------|  
|key|Stringa. Espressione consentita. Specifica l'ambito di concorrenza hello. Può essere condivisa da più criteri.|Sì|N/D|  
|numero max|Un intero. Specifica un numero massimo di richieste non sono consentiti criteri hello tooenter.|Sì|N/D|  
|timeout|Un intero. Espressione consentita. Specifica il numero di hello di secondi durante una richiesta deve attendere tooenter un ambito prima che si verifichi "403 eccessivo numero di richieste"|No|Infinity|  
|lunghezza massima della coda|Un intero. Espressione consentita. Specifica una lunghezza massima della coda hello. Le richieste in ingresso tentativo tooenter questo criterio verrà interrotta con "403 eccessivo numero di richieste" immediatamente quando è esaurita coda hello.|No|Infinity|  
  
###  <a name="ChooseUsage"></a>Uso  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  

##  <a name="log-to-eventhub"></a>Log tooEvent Hub  
 Hello `log-to-eventhub` criteri invia messaggi hello specificato formato tooan Hub di eventi definiti da un'entità del Logger. Come suggerisce il nome, i criteri di hello vengono utilizzati per il salvataggio selezionati informazioni sul contesto di richiesta o risposta per l'analisi online o offline.  
  
> [!NOTE]
>  Per una Guida dettagliata sulla configurazione di un hub eventi e la registrazione eventi, vedere [come eventi di gestione API toolog con hub eventi di Azure](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>Esempio  
 Qualsiasi stringa può essere utilizzata come toobe valore hello registrato nell'hub eventi. In questo esempio hello data e ora, nome del servizio di distribuzione, id richiesta, l'indirizzo ip e nome dell'operazione per tutte le chiamate in ingresso sono hub eventi connesso toohello Logger registrato con hello `contoso-logger` id.  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|log-to-eventhub|Elemento radice. valore Hello di questo elemento è l'hub di eventi tooyour toolog stringa hello.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|  
|---------------|-----------------|--------------|  
|logger-id|id Hello di hello Logger registrato con il servizio Gestione API.|Sì|  
|partition-id|Specifica l'indice di hello della partizione hello in cui i messaggi vengono inviati.|Facoltativo. Questo attributo non può essere usato se si usa `partition-key`.|  
|partition-key|Specifica il valore di hello utilizzato per l'assegnazione di partizione quando vengono inviati messaggi.|Facoltativo. Questo attributo non può essere usato se si usa `partition-id`.|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  

##  <a name="mock-response"></a> Restituisci risposta  
Hello `mock-response`, come nome hello implica, viene utilizzato toomock API e operazioni. Interrompe l'esecuzione della pipeline normale e restituisce un chiamante toohello risposta simulati. criteri di Hello tenta sempre di risposte tooreturn di più alta fedeltà. Include esempi di contenuto di risposta ogni volta che è possibile. Nelle situazioni in cui vengono forniti schemi ma non esempi, genera risposte di esempio dagli schemi. Se non sono presenti né esempi né schemi, restituisce risposte senza contenuto.
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>esempi  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatoria|  
|-------------|-----------------|--------------|  
|mock-response|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|--------------|  
|status-code|Specifica il codice di stato di risposta ed è esempio corrispondente utilizzato tooselect o nello schema.|No|200|  
|content-type|Specifica `Content-Type` valore dell'intestazione di risposta e viene utilizzato tooselect esempio corrispondente o nello schema.|No|None|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti

##  <a name="Retry"></a> Riprova  
 Hello `retry` criteri esegue i relativi criteri figlio una volta e quindi ripete l'esecuzione fino al tentativo di hello `condition` diventa `false` o ripetere `count` è esaurita.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a>Esempio  
 In hello forewarding richiesta di esempio seguente viene ripetuta backup tooten volte utilizzando l'algoritmo di tentativi esponenziali. Poiché `first-fast-retry` è impostato toofalse, tutti i tentativi sono algoritmo dei tentativi exponsntial toohello soggetto.  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|retry|Elemento radice. Può contenere tutti gli altri criteri come elementi figlio.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|condition|Valore letterale booleano o [espressione](api-management-policy-expressions.md) che specifica se i tentativi devono essere interrotti (`false`) o devono continuare (`true`).|Sì|N/D|  
|count|Un numero positivo che specifica hello il numero massimo di tentativi tooattempt.|Sì|N/D|  
|interval|Un numero positivo, in secondi, specificando l'intervallo di attesa hello tra tentativi hello.|Sì|N/D|  
|max-interval|Un numero positivo, in secondi, specificando l'intervallo di attesa massimo hello tra tentativi hello. È tooimplement utilizzato un algoritmo di tentativi esponenziali.|No|N/D|  
|delta|Un numero positivo, in secondi, specificare l'incremento di intervallo di attesa hello. È utilizzato tooimplement hello tentativi lineare ed esponenziale algoritmi.|No|N/D|  
|first-fast-retry|Se impostato troppo `true` , primo tentativo di hello viene eseguita immediatamente.|No|`false`|  
  
> [!NOTE]
>  Quando solo hello `interval` è specificato, **fissa** intervallo tentativi vengono eseguiti.  
>  Quando solo hello `interval` e `delta` vengono specificati un **lineare** viene utilizzato l'algoritmo di tentativi di intervallo, in cui il tempo di attesa tra tentativi viene calcolato hello in base formula - seguente `interval + (count - 1)*delta`.  
>  Quando hello `interval`, `max-interval` e `delta` vengono specificati, **esponenziale** viene applicato l'algoritmo dei tentativi di intervallo, in cui crescono in modo esponenziale il tempo di attesa hello tra i tentativi di hello dal valore hello `interval`valore toohello `max-interval` in base a seguito di toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) . Si noti che le restrizioni sull'uso dei criteri figlio verranno ereditate da questo criterio.  
  
-   **Sezioni del criterio:**in ingresso, in uscita, back-end, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
##  <a name="ReturnResponse"></a>Restituisci risposta  
 Hello `return-response` criteri interrompe l'esecuzione della pipeline e restituisce un'istanza predefinita o chiamante toohello risposta personalizzata. La risposta predefinita è `200 OK`, senza corpo. La risposta personalizzata può essere specificata tramite una variabile di contesto o le istruzioni del criterio. Se vengono specificati entrambi, risposta hello contenuto all'interno di variabile di contesto hello viene modificato mediante le istruzioni dei criteri di hello prima della restituzione toohello chiamante.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|return-response|Elemento radice.|Sì|  
|set-header|Istruzione del criterio.[set-header](api-management-transformation-policies.md#SetHTTPheader).|No|  
|set-body|Istruzione del criterio.[set-body](api-management-transformation-policies.md#SetBody).|No|  
|set-status|Istruzione del criterio [set-status](api-management-advanced-policies.md#SetStatus).|No|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|  
|---------------|-----------------|--------------|  
|response-variable-name|Hello nome di variabile di contesto hello a cui fa riferimento, ad esempio, un upstream [richiesta di invio](api-management-advanced-policies.md#SendRequest) criteri e che contiene un `Response` oggetto|Facoltativo.|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
##  <a name="SendOneWayRequest"></a>Invia richiesta unidirezionale  
 Hello `send-one-way-request` criteri invia la richiesta di hello fornito toohello URL specificato senza attendere una risposta.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>Esempio  
 Questo criterio di esempio viene illustrato un esempio dell'utilizzo di hello `send-one-way-request` toosend criteri una messaggio tooa Slack chat room se hello codice di risposta HTTP è maggiore o uguale too500. Per ulteriori informazioni su questo esempio, vedere [tramite servizi esterni dal servizio Gestione API di Azure hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|send-one-way-request|Elemento radice.|Sì|  
|URL|Hello l'URL della richiesta di hello.|No if mode=copy; otherwise yes.|  
|statico|metodo HTTP per la richiesta di hello Hello.|No if mode=copy; otherwise yes.|  
|intestazione|Intestazione della richiesta. Usare più elementi di intestazione per più intestazioni della richiesta.|No|  
|body|corpo della richiesta Hello.|No|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|Determina se si tratta di una nuova richiesta o una copia della richiesta corrente hello. In modalità in uscita, modalità = copia non viene inizializzato il corpo della richiesta hello.|No|Nuovo|  
|name|Specifica il nome di hello di hello intestazione toobe set.|Sì|N/D|  
|exists-action|Specifica quali tootake azione quando l'intestazione hello è già specificato. Questo attributo deve avere uno dei seguenti valori hello.<br /><br /> -override - sostituisce hello valore dell'intestazione esistente hello.<br />-skip: non sostituisce il valore dell'intestazione esistente di hello.<br />-aggiungere - aggiunge hello valore toohello valore dell'intestazione esistente.<br />-delete - rimuove l'intestazione di hello dalla richiesta hello.<br /><br /> Quando impostato troppo`override` l'integrazione di più voci con hello stesso nome risultati nell'intestazione di hello viene impostato in base tooall le voci (elencate più volte); solo i valori elencati verranno impostati nel risultato hello.|No|override|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
##  <a name="SendRequest"></a> Invio richiesta  
 Hello `send-request` criteri Invia richiesta hello fornito toohello specificato l'URL, in attesa non più di hello imposta il valore di timeout.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>Esempio  
 Questo esempio viene illustrato un modo tooverify un token di riferimento con un server di autorizzazione. Per ulteriori informazioni su questo esempio, vedere [tramite servizi esterni dal servizio Gestione API di Azure hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|send-request|Elemento radice.|Sì|  
|URL|Hello l'URL della richiesta di hello.|No if mode=copy; otherwise yes.|  
|statico|metodo HTTP per la richiesta di hello Hello.|No if mode=copy; otherwise yes.|  
|intestazione|Intestazione della richiesta. Usare più elementi di intestazione per più intestazioni della richiesta.|No|  
|body|corpo della richiesta Hello.|No|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|Determina se si tratta di una nuova richiesta o una copia della richiesta corrente hello. In modalità in uscita, modalità = copia non viene inizializzato il corpo della richiesta hello.|No|Nuovo|  
|response-variable-name="string"|Se non è presente, viene usato `context.Response`.|No|N/D|  
|timeout="integer"|intervallo di timeout Hello in secondi, prima chiamata hello toohello URL non riesce.|No|60|  
|ignore-error|Se true e hello richiesta comporta un errore:<br /><br /> - Se è stato specificato response-variable-name, questo conterrà un valore null.<br />- Se response-variable-name non è stato specificato, context.Request non verrà aggiornato.|No|false|  
|name|Specifica il nome di hello di hello intestazione toobe set.|Sì|N/D|  
|exists-action|Specifica quali tootake azione quando l'intestazione hello è già specificato. Questo attributo deve avere uno dei seguenti valori hello.<br /><br /> -override - sostituisce hello valore dell'intestazione esistente hello.<br />-skip: non sostituisce il valore dell'intestazione esistente di hello.<br />-aggiungere - aggiunge hello valore toohello valore dell'intestazione esistente.<br />-delete - rimuove l'intestazione di hello dalla richiesta hello.<br /><br /> Quando impostato troppo`override` l'integrazione di più voci con hello stesso nome risultati nell'intestazione di hello viene impostato in base tooall le voci (elencate più volte); solo i valori elencati verranno impostati nel risultato hello.|No|override|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
##  <a name="SetHttpProxy"></a>Impostare il proxy HTTP  
 Hello `proxy` criteri consentono di tooroute richieste inoltrate toobackends tramite un proxy HTTP. Solo HTTP (non HTTPS) è supportata tra il gateway hello e proxy hello. Solo autenticazione Basic e NTLM.
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>Esempio  
Si noti hello utilizzo di [proprietà](api-management-howto-properties.md) come valori di tooavoid hello nome utente e password, l'archiviazione di informazioni riservate nel documento di criteri hello.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|proxy|Elemento radice|Sì|  

### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|url="string"|URL del proxy in forma di hello di HTTP.|Sì|N/D |  
|username="string"|Toobe nome utente utilizzato per l'autenticazione con il proxy di hello.|No|N/D |  
|password="string"|Toobe password utilizzata per l'autenticazione con il proxy di hello.|No|N/D |  

### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound  
  
-   **Ambiti del criterio:** tutti gli ambiti  

##  <a name="SetRequestMethod"></a> Impostare il metodo di richiesta  
 Hello `set-method` criteri consentono di metodo di richiesta HTTP hello toochange per una richiesta.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>Esempio  
 Questo esempio di criterio che utilizza hello `set-method` criteri Mostra un esempio di invio di una messaggio tooa Slack chat room se hello codice di risposta HTTP è maggiore o uguale too500. Per ulteriori informazioni su questo esempio, vedere [tramite servizi esterni dal servizio Gestione API di Azure hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|set-method|Elemento radice. valore Hello elemento hello specifica il metodo HTTP hello.|Sì|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
##  <a name="SetStatus"></a> Impostare il codice di stato  
 Hello `set-status` criteri set hello HTTP stato codice toohello valore specificato.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>Esempio  
 Questo esempio viene illustrato come tooreturn una risposta 401, se il token di autorizzazione hello non è valido. Per ulteriori informazioni, vedere [tramite servizi esterni da hello servizio Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|set-status|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|code="integer"|tooreturn codice di stato HTTP Hello.|Sì|N/D|  
|reason="string"|Descrizione del motivo di hello per la restituzione di codice di stato hello.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  

##  <a name="set-variable"></a>Impostare una variabile  
 Hello `set-variable` criteri dichiara un [contesto](api-management-policy-expressions.md#ContextVariables) variabile e assegna un valore specificato tramite un [espressione](api-management-policy-expressions.md) o un valore letterale stringa. Se l'espressione di hello contiene un valore letterale verrà convertito tooa stringa e hello il tipo di valore hello sarà `System.String`.  
  
###  <a name="set-variablePolicyStatement"></a>Istruzione del criterio  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a>Esempio  
 Hello esempio seguente viene illustrato un criterio di variabile set in hello in ingresso di sezione. Questo criterio variabile set crea un `isMobile` booleano [contesto](api-management-policy-expressions.md#ContextVariables) variabile impostata tootrue se hello `User-Agent` richiesta intestazione contiene testo hello `iPad` o `iPhone`.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|set-variable|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|  
|---------------|-----------------|--------------|  
|name|nome Hello della variabile di hello.|Sì|  
|value|valore di Hello della variabile hello. Può essere un'espressione o un valore letterale.|Sì|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
###  <a name="set-variableAllowedTypes"></a>Tipi consentiti  
 Le espressioni utilizzate in hello `set-variable` criteri devono restituire uno dei seguenti tipi di base hello.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a> Traccia  
 Hello `trace` criteri aggiunge una stringa in hello [API controllo](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output. Hello criteri verranno eseguiti solo quando la traccia è attivata, vale a dire `Ocp-Apim-Trace` intestazione della richiesta è presente e impostato troppo`true` e `Ocp-Apim-Subscription-Key` intestazione della richiesta è presente e contiene una chiave valida associata a hello amministratore account.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|trace|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|una sezione source|Visualizzatore di tracce di stringa letterale toohello significativo e specificando origine hello del messaggio hello.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Sezioni del criterio:** inbound, outbound, backend, on-error  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
##  <a name="Wait"></a> Attesa  
 Hello `wait` criteri esegue i criteri figlio diretti in parallelo e attende che tutti o uno dei relativi toocomplete criteri figlio immediati prima che venga completato. Hello attesa criteri possono avere come relativi criteri figlio immediati [richiesta di invio](api-management-advanced-policies.md#SendRequest), [ottenere valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey), e [flusso di controllo](api-management-advanced-policies.md#choose) criteri.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente hello sono disponibili due `choose` criteri come criteri figlio immediati di hello `wait` criteri. Ognuno di questi criteri `choose` viene eseguito in parallelo. Ogni `choose` criteri tenta tooretrieve valore memorizzato nella cache. Se è presente un mancato riscontro nella cache, un servizio back-end viene chiamato il valore di hello tooprovide. In questo hello esempio `wait` criteri non verrà completata fino al completamento di tutti i relativi criteri figlio immediati, poiché hello `for` attributo è impostato troppo`all`.   Nelle variabili di contesto hello in questo esempio (`execute-branch-one`, `value-one`, `execute-branch-two`, e `value-two`) vengono dichiarati di fuori ambito hello di questo criterio di esempio.  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a>Elementi  
  
|Elemento|Descrizione|Obbligatorio|  
|-------------|-----------------|--------------|  
|wait|Elemento radice. Può contenere come elementi figlio solo i criteri `send-request`, `cache-lookup-value` e `choose`.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Attributo|Descrizione|Obbligatorio|Default|  
|---------------|-----------------|--------------|-------------|  
|for|Determina se hello `wait` criteri attende che tutti i toobe criteri figlio immediati completata o solo una. I valori consentiti sono i seguenti:<br /><br /> -   `all`-attendere tutti figlio immediati criteri toocomplete<br />-i - attendere qualsiasi toocomplete criterio figlio immediati. Una volta completato il primo criterio di figlio immediati hello, hello `wait` criteri completa e viene terminata l'esecuzione di tutti gli altri criteri figlio immediati.|No|tutti|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sezioni del criterio:** inbound, outbound, back-end  
  
-   **Ambiti del criterio:** tutti gli ambiti  
  
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso di questi criteri, vedere:
-   [Criteri in Gestione API](api-management-howto-policies.md) 
-   [Espressioni di criteri](api-management-policy-expressions.md)
