---
title: Memorizzazione nella cache personalizzata in Gestione API di Azure
description: Informazioni su come memorizzare elementi nella cache in base alla chiave in Gestione API di Azure
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
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="86e91-103">Memorizzazione nella cache personalizzata in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="86e91-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="86e91-104">Il servizio Gestione API di Azure prevede il supporto incorporato per la [memorizzazione nella cache delle risposte HTTP](api-management-howto-cache.md) usando l'URL della risorsa come chiave.</span><span class="sxs-lookup"><span data-stu-id="86e91-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="86e91-105">La chiave può essere modificata dalle intestazioni della richiesta usando le proprietà `vary-by` .</span><span class="sxs-lookup"><span data-stu-id="86e91-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="86e91-106">Questo risulta utile per la memorizzazione nella cache di intere risposte HTTP (note anche come rappresentazioni), ma talvolta è utile memorizzare nella cache anche solo una parte di una rappresentazione.</span><span class="sxs-lookup"><span data-stu-id="86e91-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="86e91-107">I nuovi criteri [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) e [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) consentono di archiviare e recuperare singoli dati arbitrari all'interno di definizioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="86e91-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="86e91-108">Questa possibilità migliora anche il criterio [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) introdotto in precedenza, dal momento che ora è possibile memorizzare nella cache le risposte provenienti da servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="86e91-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="86e91-109">Architettura</span><span class="sxs-lookup"><span data-stu-id="86e91-109">Architecture</span></span>
<span data-ttu-id="86e91-110">Il servizio Gestione API usa una cache di dati condivisa per tenant. In questo modo, man mano che aumenta il numero di unità, è sempre possibile accedere agli stessi dati memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="86e91-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="86e91-111">Quando si adotta una distribuzione in più aree, tuttavia, sono presenti cache indipendenti all'interno di ogni area.</span><span class="sxs-lookup"><span data-stu-id="86e91-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="86e91-112">Per questo motivo, è importante non considerare la cache come un archivio dati e l'unica fonte di alcune informazioni.</span><span class="sxs-lookup"><span data-stu-id="86e91-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="86e91-113">Così facendo, se successivamente si decide di usare la distribuzione in più aree, i clienti con utenti che viaggiano posso perdere l'accesso ai dati memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="86e91-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="86e91-114">Memorizzazione di frammenti</span><span class="sxs-lookup"><span data-stu-id="86e91-114">Fragment caching</span></span>
<span data-ttu-id="86e91-115">Esistono casi in cui le risposte restituite contengono una parte di dati costosa da determinare ma che rimane aggiornata per un periodo di tempo ragionevole.</span><span class="sxs-lookup"><span data-stu-id="86e91-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="86e91-116">Si consideri, ad esempio, un servizio creato da una compagnia aerea che fornisce informazioni sulla prenotazione dei voli, lo stato dei voli e così via. Se l'utente è membro del programma a punti della compagnia aerea, dovrà anche avere informazioni sul proprio stato e sulle miglia accumulate.</span><span class="sxs-lookup"><span data-stu-id="86e91-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="86e91-117">Le informazioni relative agli utenti possono essere archiviate in un sistema diverso, ma potrebbe essere utile includerle nelle risposte restituite con le informazioni sulle prenotazioni e lo stato dei voli.</span><span class="sxs-lookup"><span data-stu-id="86e91-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="86e91-118">Questa operazione può essere eseguita attraverso un processo denominato memorizzazione di frammenti.</span><span class="sxs-lookup"><span data-stu-id="86e91-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="86e91-119">La rappresentazione primaria può essere restituita dal server di origine usando un token per indicare la posizione per l'inserimento delle informazioni relative agli utenti.</span><span class="sxs-lookup"><span data-stu-id="86e91-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="86e91-120">Si consideri la seguente risposta JSON da un'API back-end.</span><span class="sxs-lookup"><span data-stu-id="86e91-120">Consider the following JSON response from a backend API.</span></span>

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

<span data-ttu-id="86e91-121">E la risorsa secondaria `/userprofile/{userid}` che presenta un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="86e91-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="86e91-122">Per determinare quali informazioni dell'utente includere, è necessario identificare l'utente finale.</span><span class="sxs-lookup"><span data-stu-id="86e91-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="86e91-123">Questo meccanismo dipende dall'implementazione.</span><span class="sxs-lookup"><span data-stu-id="86e91-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="86e91-124">Nell'esempio viene usata l'attestazione `Subject` di un token `JWT`.</span><span class="sxs-lookup"><span data-stu-id="86e91-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="86e91-125">Il valore `enduserid` viene memorizzato in una variabile di contesto per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="86e91-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="86e91-126">Il passaggio successivo consiste nel determinare se una richiesta precedente ha già recuperato le informazioni utente e le ha archiviate nella cache.</span><span class="sxs-lookup"><span data-stu-id="86e91-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="86e91-127">A tale scopo viene usato il criterio `cache-lookup-value` .</span><span class="sxs-lookup"><span data-stu-id="86e91-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="86e91-128">Se non sono presenti voci nella cache che corrispondono al valore della chiave, non viene creata alcuna variabile di contesto `userprofile` .</span><span class="sxs-lookup"><span data-stu-id="86e91-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="86e91-129">Per verificare l'esito della ricerca viene usato il criterio del flusso di controllo `choose` .</span><span class="sxs-lookup"><span data-stu-id="86e91-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="86e91-130">Se la variabile di contesto `userprofile` non esiste, sarà necessario eseguire una richiesta HTTP per recuperarla.</span><span class="sxs-lookup"><span data-stu-id="86e91-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="86e91-131">Per creare l'URL per la risorsa del profilo utente si usa `enduserid` .</span><span class="sxs-lookup"><span data-stu-id="86e91-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="86e91-132">Dopo aver ottenuto la risposta, è possibile estrarre il corpo della risposta dalla risposta e archiviarlo nuovamente in una variabile di contesto.</span><span class="sxs-lookup"><span data-stu-id="86e91-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="86e91-133">Per evitare di dover eseguire nuovamente la richiesta HTTP quando lo stesso utente esegue un'altra richiesta, è possibile archiviare il profilo utente nella cache.</span><span class="sxs-lookup"><span data-stu-id="86e91-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="86e91-134">Il valore viene archiviato nella cache usando esattamente la stessa chiave con cui in origine si è cercato di recuperarlo.</span><span class="sxs-lookup"><span data-stu-id="86e91-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="86e91-135">La durata scelta per l'archiviazione del valore deve essere basata sulla frequenza di modifica delle informazioni e sulla tolleranza degli utenti rispetto alle informazioni non aggiornate.</span><span class="sxs-lookup"><span data-stu-id="86e91-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="86e91-136">È importante tenere presente che il recupero dalla cache è ancora una richiesta di rete out-of-process, che può aggiungere decine di millisecondi della richiesta.</span><span class="sxs-lookup"><span data-stu-id="86e91-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="86e91-137">I vantaggi sono evidenti quando per determinare le informazioni relative al profilo utente è necessario molto più tempo a causa della necessità di eseguire query di database o aggregare le informazioni da più sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="86e91-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="86e91-138">Il passaggio finale del processo consiste nell'aggiornare la risposta restituita con le informazioni sul profilo utente.</span><span class="sxs-lookup"><span data-stu-id="86e91-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="86e91-139">Si è scelto di includere le virgolette come parte del token in modo che anche quando non si verifica la sostituzione, la risposta rimane un oggetto JSON valido.</span><span class="sxs-lookup"><span data-stu-id="86e91-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="86e91-140">Lo scopo principale era semplificare il debug.</span><span class="sxs-lookup"><span data-stu-id="86e91-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="86e91-141">Quando si combinano insieme tutti questi passaggi, il risultato finale è un criterio simile a quello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="86e91-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
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

<span data-ttu-id="86e91-142">Questo approccio alla memorizzazione nella cache viene usato principalmente in siti web in cui il codice HTML viene composto sul lato server in modo che sia possibile eseguirne il rendering come una singola pagina.</span><span class="sxs-lookup"><span data-stu-id="86e91-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="86e91-143">Tuttavia, può risultare utile anche per le API in cui i client non possono eseguire la memorizzazione nella cache del codice HTTP sul lato client o non è consigliabile affidare tale compito al client.</span><span class="sxs-lookup"><span data-stu-id="86e91-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="86e91-144">Questo stesso tipo di memorizzazione di frammenti può essere eseguito anche nei server Web back-end usando un server di memorizzazione nella cache Redis. Tuttavia, usare il servizio Gestione API per eseguire questa operazione può risultare utile quando i frammenti memorizzati nella cache provengono da back-end diversi rispetto alle risposte primarie.</span><span class="sxs-lookup"><span data-stu-id="86e91-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="86e91-145">Controllo delle versioni trasparente</span><span class="sxs-lookup"><span data-stu-id="86e91-145">Transparent versioning</span></span>
<span data-ttu-id="86e91-146">Solitamente sono supportate più versioni diverse dell'implementazione di un'API in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="86e91-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="86e91-147">Ciò è dovuto probabilmente alla necessità di supportare ambienti diversi (ad esempio, ambienti di sviluppo, test, produzione e così via), oppure alla necessità di supportare versioni precedenti dell'API e consentire ai consumer dell'API di eseguire la migrazione a versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="86e91-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="86e91-148">Anziché richiedere agli sviluppatori di client di modificare l'URL da `/v1/customers` in `/v2/customers`, un possibile approccio alla gestione di questa situazione consiste nell'archiviare tra i dati del profilo del consumer la versione dell'API da usare e chiamare l'URL del back-end appropriato.</span><span class="sxs-lookup"><span data-stu-id="86e91-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="86e91-149">Per determinare l'URL del back-end corretto da chiamare per un determinato client, è necessario eseguire una query su alcuni dati di configurazione.</span><span class="sxs-lookup"><span data-stu-id="86e91-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="86e91-150">Con la memorizzazione nella cache di questi dati di configurazione, è possibile ridurre al minimo i problemi di prestazioni correlati alla ricerca.</span><span class="sxs-lookup"><span data-stu-id="86e91-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="86e91-151">Il primo passaggio consiste nel determinare l'identificatore usato per configurare la versione scelta.</span><span class="sxs-lookup"><span data-stu-id="86e91-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="86e91-152">In questo esempio, si è scelto di associare la versione alla chiave della sottoscrizione del prodotto.</span><span class="sxs-lookup"><span data-stu-id="86e91-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="86e91-153">Viene quindi eseguita una ricerca nella cache per verificare se è già stata recuperata la versione del client scelta.</span><span class="sxs-lookup"><span data-stu-id="86e91-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="86e91-154">Il codice seguente permette di verificare se è presente nella cache.</span><span class="sxs-lookup"><span data-stu-id="86e91-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="86e91-155">Se non è presente, è possibile recuperarla.</span><span class="sxs-lookup"><span data-stu-id="86e91-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="86e91-156">Estrarre il corpo della risposta dalla risposta.</span><span class="sxs-lookup"><span data-stu-id="86e91-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="86e91-157">Memorizzare nuovamente l'informazione nella cache per usarla in futuro.</span><span class="sxs-lookup"><span data-stu-id="86e91-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="86e91-158">Infine, aggiornare l'URL del back-end per selezionare la versione del servizio scelta dal client.</span><span class="sxs-lookup"><span data-stu-id="86e91-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="86e91-159">Il criterio completo sarà il seguente.</span><span class="sxs-lookup"><span data-stu-id="86e91-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
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

<span data-ttu-id="86e91-160">Consentire ai consumer delle API il controllo trasparente della versione del back-end accessibile dai client senza dover aggiornare e ridistribuire i client è una soluzione elegante che risolve diversi problemi di controllo delle versioni delle API.</span><span class="sxs-lookup"><span data-stu-id="86e91-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="86e91-161">Isolamento dei tenant</span><span class="sxs-lookup"><span data-stu-id="86e91-161">Tenant Isolation</span></span>
<span data-ttu-id="86e91-162">Nelle distribuzioni multi-tenant di grandi dimensioni alcune aziende creano gruppi di tenant separati in distribuzioni distinte dell'hardware back-end.</span><span class="sxs-lookup"><span data-stu-id="86e91-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="86e91-163">Questo approccio permette di ridurre al minimo il numero di clienti interessati da un problema hardware nel back-end.</span><span class="sxs-lookup"><span data-stu-id="86e91-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="86e91-164">Permette anche la distribuzione in più fasi delle nuove versioni dei software.</span><span class="sxs-lookup"><span data-stu-id="86e91-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="86e91-165">È preferibile che questa architettura di back-end sia trasparente per i consumer dell'API.</span><span class="sxs-lookup"><span data-stu-id="86e91-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="86e91-166">Questo approccio può essere realizzato in modo analogo al controllo delle versioni trasparente perché si basa sulla stessa tecnica di manipolazione dell'URL del back-end usando lo stato di configurazione per chiave dell'API.</span><span class="sxs-lookup"><span data-stu-id="86e91-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="86e91-167">Invece di restituire una versione preferita dell'API per ogni chiave della sottoscrizione, viene restituito un identificatore che mette in relazione un tenant con il gruppo di componenti hardware assegnato.</span><span class="sxs-lookup"><span data-stu-id="86e91-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="86e91-168">L'identificatore può essere usato per creare l'URL del back-end appropriato.</span><span class="sxs-lookup"><span data-stu-id="86e91-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="86e91-169">Summary</span><span class="sxs-lookup"><span data-stu-id="86e91-169">Summary</span></span>
<span data-ttu-id="86e91-170">La libertà di usare la cache di Gestione API di Azure per archiviare qualsiasi tipo di dati consente di accedere facilmente ai dati di configurazione che possono influenzare la modalità di elaborazione di una richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="86e91-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="86e91-171">La cache può anche essere usata per memorizzare frammenti di dati che possono integrare le risposte restituite da un'API back-end.</span><span class="sxs-lookup"><span data-stu-id="86e91-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86e91-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86e91-172">Next steps</span></span>
<span data-ttu-id="86e91-173">Se questi criteri hanno permesso di abilitare altri scenari o se si vuole realizzare scenari non ancora disponibili, è possibile lasciare i propri commenti e suggerimenti nel thread Disqus di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="86e91-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

