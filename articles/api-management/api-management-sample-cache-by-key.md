---
title: aaaCustom la memorizzazione nella cache in Gestione API di Azure
description: Informazioni su come toocache gli elementi dalla chiave in Gestione API di Azure
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a>Memorizzazione nella cache personalizzata in Gestione API di Azure
Servizio gestione API di Azure include il supporto incorporato per [la memorizzazione nella cache di risposta HTTP](api-management-howto-cache.md) utilizzando l'URL della risorsa hello come chiave hello. Hello chiave può essere modificata da intestazioni di richiesta usando hello `vary-by` proprietà. Ciò è utile per la memorizzazione nella cache delle risposte HTTP intere (noto anche come rappresentazioni), ma a volte risulta utile toojust cache una parte di una rappresentazione. nuovo Hello [valore di ricerca cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) e [valore di archivio della cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) criteri offrono possibilità di hello toostore e recuperare dati arbitrari all'interno delle definizioni di criteri. Questa possibilità aggiunge inoltre toohello valore introdotto [richiesta di invio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) criteri perché è ora possibile memorizzare nella cache le risposte da servizi esterni.

## <a name="architecture"></a>Architettura
Servizio gestione API Usa una cache di dati condiviso per tenant in modo che, quando si scala toomultiple unità si riceveranno sempre accesso toohello stessi dati memorizzati nella cache. Tuttavia, quando si lavora con una distribuzione con più aree sono indipendenti cache all'interno di ognuna delle regioni hello. Scadenza toothis, è importante toonot trattare cache di hello come archivio dati, in cui è l'unica fonte di hello di alcune delle informazioni contenute. Se si ha e successivamente deciso tootake sfruttare la distribuzione con più aree di hello, i clienti con gli utenti che viaggiano perdano l'accesso ai dati memorizzati nella cache toothat.

## <a name="fragment-caching"></a>Memorizzazione di frammenti
Esistono casi in cui viene restituite risposte contengono una parte dei dati che sono dispendiosa toodetermine e rimangono ancora aggiornato per un periodo di tempo ragionevole. Si consideri, ad esempio, un servizio creato da una compagnia aerea che fornisce informazioni sulla prenotazione dei voli, lo stato dei voli e così via. Se l'utente hello è un membro del programma di punti di hello airlines, hanno anche informazioni relative allo stato corrente di tootheir e chilometraggio accumulati. Queste informazioni relative agli utenti potrebbero essere archiviate in un altro sistema, ma potrebbe essere auspicabile tooinclude nelle risposte restituiva sullo stato di volo e le prenotazioni. Questa operazione può essere eseguita attraverso un processo denominato memorizzazione di frammenti. Hello rappresentazione primario può essere restituito dal server di origine hello utilizzando un tipo di token tooindicate in cui le informazioni relative agli utenti di hello sono toobe inserito. 

Prendere in considerazione hello dopo la risposta JSON da una API back-end.

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

E la risorsa secondaria `/userprofile/{userid}` che presenta un aspetto simile al seguente.

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

In ordine toodetermine hello utente appropriati informazioni tooinclude, è necessario tooidentify l'identità utente finale di hello. Questo meccanismo dipende dall'implementazione. Ad esempio, si utilizza hello `Subject` attestazione di un `JWT` token. 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

Il valore `enduserid` viene memorizzato in una variabile di contesto per usarlo in seguito. passaggio successivo Hello è toodetermine se una richiesta precedente già recuperate informazioni utente hello e memorizzato nella cache di hello. A tale scopo si usa hello `cache-lookup-value` criteri.

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

Se è presente alcuna voce nella cache di hello che corrisponde al valore della chiave toohello, quindi no `userprofile` verrà creata la variabile di contesto. Verifica riuscita hello di ricerca di hello utilizzando hello `choose` criterio di flusso di controllo.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

Se hello `userprofile` variabile di contesto non esiste, quindi è in corso toohave toomake HTTP richiesta tooretrieve è.

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

Utilizziamo hello `enduserid` tooconstruct hello URL toohello utente risorsa per il profilo. Una volta che la risposta hello, è possibile pull del testo del corpo hello fuori risposta hello e archiviarlo in una variabile di contesto.

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid us con toomake questa richiesta HTTP, quando l'utente stesso hello effettua un'altra richiesta, che è possibile archiviare profilo utente hello nella cache di hello.

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

Valore hello è memorizzare nella cache di hello mediante hello esatta stessa chiave che si è tentato originariamente tooretrieve con. Hello durata che si sceglie il valore di hello toostore dovrebbe essere basata sulla frequenza hello utenti come tolleranza d'errore e modifica delle informazioni di tooout di informazioni sulla data. 

È importante toorealize che il recupero dalla cache di hello è ancora un out-of-process, la richiesta di rete e potenzialmente comunque possibile aggiungere decine di millisecondi toohello richiesta. vantaggi di Hello provengono quando determinante informazioni del profilo utente hello richiederà un tempo rispetto a quello di scadenza tooneeding toodo le query di database o le informazioni di aggregazione da più sistemi back-end.

Hello ultimo passaggio nel processo di hello è hello tooupdate ha restituito una risposta con le informazioni del profilo utente.

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

Si è deciso tooinclude hello tra virgolette come parte del token hello in modo che anche quando non viene eseguita la sostituzione hello, risposta hello è ancora valido per JSON. Si tratta principalmente toomake il debug.

Quando si combinano contemporaneamente tutti questi passaggi, risultato finale hello è un criterio simile hello segue quello.

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

Questo approccio di memorizzazione nella cache viene utilizzato principalmente in siti web in cui è composta HTML sul lato server hello in modo che sia possibile eseguirne il rendering come una singola pagina. Tuttavia, può anche essere utile sul lato di API in cui i client non client HTTP di memorizzazione nella cache o è consigliabile non tooput tale compito nel client hello.

Questo stesso tipo di frammento la memorizzazione nella cache può essere eseguito anche nei server web back-end di hello tramite un server di memorizzazione nella cache di Redis, tuttavia, utilizzando tooperform servizio Gestione API di hello questa operazione è utile quando frammenti memorizzati nella cache di hello provenienti da diversi sistemi back-end di hello risposte primarie.

## <a name="transparent-versioning"></a>Controllo delle versioni trasparente
È pratica comune per più versioni di implementazione diversa di un toobe API supportate in qualsiasi momento. Questo è probabilmente toosupport diversi ambienti, ad esempio sviluppo, test, produzione e così via, o potrebbe essere toosupport le versioni precedenti di tempo toogive hello API per le versioni dell'API consumer toomigrate toonewer. 

Un approccio toohandling questo invece della richiesta client sviluppatori toochange hello URL da `/v1/customers` troppo`/v2/customers` è toostore nei dati di profilo del consumer hello quale versione di hello API sono attualmente desidera toouse e chiamare hello appropriato URL di back-end. In ordine toodetermine hello back-end corretto URL toocall per un particolare client, è necessario tooquery alcuni dati di configurazione. Memorizzazione nella cache di dati di configurazione, è possibile ridurre al minimo il calo di prestazioni hello di eseguire la ricerca.

primo passaggio Hello è l'identificatore hello toodetermine utilizzato tooconfigure versione desiderata di hello. In questo esempio, si è deciso di chiave di sottoscrizione prodotto versione toohello tooassociate hello. 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

È quindi possibile eseguire un toosee ricerca cache se è già stato recuperato versione di hello client desiderato.

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

Quindi selezionare toosee se non c' nella cache di hello.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

Se non è presente, è possibile recuperarla.

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

Estrarre il testo del corpo di risposta hello dalla risposta hello.

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

Memorizzarlo nella cache di hello per utilizzi futuri.

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

E infine hello back-end URL tooselect hello versione dell'aggiornamento del servizio hello desiderata dal client hello.

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

Hello completamente criteri sono i seguenti.

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

Abilitazione del controllo del consumer API tootransparently quale versione di back-end si accede dai client senza dovere tooupdate e ridistribuire i client è una soluzione elegante che consente di risolvere numerosi problemi di controllo delle versioni delle API.

## <a name="tenant-isolation"></a>Isolamento dei tenant
Nelle distribuzioni multi-tenant di grandi dimensioni alcune aziende creano gruppi di tenant separati in distribuzioni distinte dell'hardware back-end. Consente di ridurre il numero di hello di clienti che sono interessati da un problema hardware sul back-end hello. Consente inoltre di nuovo toobe di versioni di software di implementazione in fasi. Idealmente, questa architettura di back-end deve essere trasparente tooAPI consumer. Questo può essere realizzato in un simile modo tootransparent il controllo delle versioni perché si basa su hello stessa tecnica di manipolazione hello URL di back-end usando lo stato di configurazione per ogni chiave API.  

Anziché restituire una versione preferita di hello API per ogni chiave di sottoscrizione, viene restituito un identificatore che si riferisce a un gruppo di componenti hardware tenant toohello assegnato. Tale identificatore può essere utilizzato tooconstruct hello back-end appropriata URL.

## <a name="summary"></a>Riepilogo
hello toouse di libertà Hello cache di gestione API di Azure per l'archiviazione di qualsiasi tipo di dati consente dati tooconfiguration accesso efficiente che possono influire sulla modalità di hello che viene elaborata una richiesta in ingresso. Può anche essere utilizzati toostore i frammenti di dati che è possono migliorare le risposte, restituite dall'API back-end.

## <a name="next-steps"></a>Passaggi successivi
Per commenti e suggerimenti in hello thread di Disqus per questo argomento se sono presenti altri scenari di questi criteri sono abilitati per è, o se sono presenti scenari desidera tooachieve ma non è attualmente possibile.

