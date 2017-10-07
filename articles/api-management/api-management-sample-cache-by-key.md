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
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="f8472-103">Memorizzazione nella cache personalizzata in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="f8472-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="f8472-104">Servizio gestione API di Azure include il supporto incorporato per [la memorizzazione nella cache di risposta HTTP](api-management-howto-cache.md) utilizzando l'URL della risorsa hello come chiave hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="f8472-105">Hello chiave può essere modificata da intestazioni di richiesta usando hello `vary-by` proprietà.</span><span class="sxs-lookup"><span data-stu-id="f8472-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="f8472-106">Ciò è utile per la memorizzazione nella cache delle risposte HTTP intere (noto anche come rappresentazioni), ma a volte risulta utile toojust cache una parte di una rappresentazione.</span><span class="sxs-lookup"><span data-stu-id="f8472-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="f8472-107">nuovo Hello [valore di ricerca cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) e [valore di archivio della cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) criteri offrono possibilità di hello toostore e recuperare dati arbitrari all'interno delle definizioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="f8472-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="f8472-108">Questa possibilità aggiunge inoltre toohello valore introdotto [richiesta di invio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) criteri perché è ora possibile memorizzare nella cache le risposte da servizi esterni.</span><span class="sxs-lookup"><span data-stu-id="f8472-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="f8472-109">Architettura</span><span class="sxs-lookup"><span data-stu-id="f8472-109">Architecture</span></span>
<span data-ttu-id="f8472-110">Servizio gestione API Usa una cache di dati condiviso per tenant in modo che, quando si scala toomultiple unità si riceveranno sempre accesso toohello stessi dati memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="f8472-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="f8472-111">Tuttavia, quando si lavora con una distribuzione con più aree sono indipendenti cache all'interno di ognuna delle regioni hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="f8472-112">Scadenza toothis, è importante toonot trattare cache di hello come archivio dati, in cui è l'unica fonte di hello di alcune delle informazioni contenute.</span><span class="sxs-lookup"><span data-stu-id="f8472-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="f8472-113">Se si ha e successivamente deciso tootake sfruttare la distribuzione con più aree di hello, i clienti con gli utenti che viaggiano perdano l'accesso ai dati memorizzati nella cache toothat.</span><span class="sxs-lookup"><span data-stu-id="f8472-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="f8472-114">Memorizzazione di frammenti</span><span class="sxs-lookup"><span data-stu-id="f8472-114">Fragment caching</span></span>
<span data-ttu-id="f8472-115">Esistono casi in cui viene restituite risposte contengono una parte dei dati che sono dispendiosa toodetermine e rimangono ancora aggiornato per un periodo di tempo ragionevole.</span><span class="sxs-lookup"><span data-stu-id="f8472-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="f8472-116">Si consideri, ad esempio, un servizio creato da una compagnia aerea che fornisce informazioni sulla prenotazione dei voli, lo stato dei voli e così via. Se l'utente hello è un membro del programma di punti di hello airlines, hanno anche informazioni relative allo stato corrente di tootheir e chilometraggio accumulati.</span><span class="sxs-lookup"><span data-stu-id="f8472-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="f8472-117">Queste informazioni relative agli utenti potrebbero essere archiviate in un altro sistema, ma potrebbe essere auspicabile tooinclude nelle risposte restituiva sullo stato di volo e le prenotazioni.</span><span class="sxs-lookup"><span data-stu-id="f8472-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="f8472-118">Questa operazione può essere eseguita attraverso un processo denominato memorizzazione di frammenti.</span><span class="sxs-lookup"><span data-stu-id="f8472-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="f8472-119">Hello rappresentazione primario può essere restituito dal server di origine hello utilizzando un tipo di token tooindicate in cui le informazioni relative agli utenti di hello sono toobe inserito.</span><span class="sxs-lookup"><span data-stu-id="f8472-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="f8472-120">Prendere in considerazione hello dopo la risposta JSON da una API back-end.</span><span class="sxs-lookup"><span data-stu-id="f8472-120">Consider hello following JSON response from a backend API.</span></span>

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

<span data-ttu-id="f8472-121">E la risorsa secondaria `/userprofile/{userid}` che presenta un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="f8472-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="f8472-122">In ordine toodetermine hello utente appropriati informazioni tooinclude, è necessario tooidentify l'identità utente finale di hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="f8472-123">Questo meccanismo dipende dall'implementazione.</span><span class="sxs-lookup"><span data-stu-id="f8472-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="f8472-124">Ad esempio, si utilizza hello `Subject` attestazione di un `JWT` token.</span><span class="sxs-lookup"><span data-stu-id="f8472-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="f8472-125">Il valore `enduserid` viene memorizzato in una variabile di contesto per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="f8472-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="f8472-126">passaggio successivo Hello è toodetermine se una richiesta precedente già recuperate informazioni utente hello e memorizzato nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="f8472-127">A tale scopo si usa hello `cache-lookup-value` criteri.</span><span class="sxs-lookup"><span data-stu-id="f8472-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="f8472-128">Se è presente alcuna voce nella cache di hello che corrisponde al valore della chiave toohello, quindi no `userprofile` verrà creata la variabile di contesto.</span><span class="sxs-lookup"><span data-stu-id="f8472-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="f8472-129">Verifica riuscita hello di ricerca di hello utilizzando hello `choose` criterio di flusso di controllo.</span><span class="sxs-lookup"><span data-stu-id="f8472-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="f8472-130">Se hello `userprofile` variabile di contesto non esiste, quindi è in corso toohave toomake HTTP richiesta tooretrieve è.</span><span class="sxs-lookup"><span data-stu-id="f8472-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

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

<span data-ttu-id="f8472-131">Utilizziamo hello `enduserid` tooconstruct hello URL toohello utente risorsa per il profilo.</span><span class="sxs-lookup"><span data-stu-id="f8472-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="f8472-132">Una volta che la risposta hello, è possibile pull del testo del corpo hello fuori risposta hello e archiviarlo in una variabile di contesto.</span><span class="sxs-lookup"><span data-stu-id="f8472-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="f8472-133">tooavoid us con toomake questa richiesta HTTP, quando l'utente stesso hello effettua un'altra richiesta, che è possibile archiviare profilo utente hello nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="f8472-134">Valore hello è memorizzare nella cache di hello mediante hello esatta stessa chiave che si è tentato originariamente tooretrieve con.</span><span class="sxs-lookup"><span data-stu-id="f8472-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="f8472-135">Hello durata che si sceglie il valore di hello toostore dovrebbe essere basata sulla frequenza hello utenti come tolleranza d'errore e modifica delle informazioni di tooout di informazioni sulla data.</span><span class="sxs-lookup"><span data-stu-id="f8472-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="f8472-136">È importante toorealize che il recupero dalla cache di hello è ancora un out-of-process, la richiesta di rete e potenzialmente comunque possibile aggiungere decine di millisecondi toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="f8472-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="f8472-137">vantaggi di Hello provengono quando determinante informazioni del profilo utente hello richiederà un tempo rispetto a quello di scadenza tooneeding toodo le query di database o le informazioni di aggregazione da più sistemi back-end.</span><span class="sxs-lookup"><span data-stu-id="f8472-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="f8472-138">Hello ultimo passaggio nel processo di hello è hello tooupdate ha restituito una risposta con le informazioni del profilo utente.</span><span class="sxs-lookup"><span data-stu-id="f8472-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="f8472-139">Si è deciso tooinclude hello tra virgolette come parte del token hello in modo che anche quando non viene eseguita la sostituzione hello, risposta hello è ancora valido per JSON.</span><span class="sxs-lookup"><span data-stu-id="f8472-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="f8472-140">Si tratta principalmente toomake il debug.</span><span class="sxs-lookup"><span data-stu-id="f8472-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="f8472-141">Quando si combinano contemporaneamente tutti questi passaggi, risultato finale hello è un criterio simile hello segue quello.</span><span class="sxs-lookup"><span data-stu-id="f8472-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

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

<span data-ttu-id="f8472-142">Questo approccio di memorizzazione nella cache viene utilizzato principalmente in siti web in cui è composta HTML sul lato server hello in modo che sia possibile eseguirne il rendering come una singola pagina.</span><span class="sxs-lookup"><span data-stu-id="f8472-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="f8472-143">Tuttavia, può anche essere utile sul lato di API in cui i client non client HTTP di memorizzazione nella cache o è consigliabile non tooput tale compito nel client hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="f8472-144">Questo stesso tipo di frammento la memorizzazione nella cache può essere eseguito anche nei server web back-end di hello tramite un server di memorizzazione nella cache di Redis, tuttavia, utilizzando tooperform servizio Gestione API di hello questa operazione è utile quando frammenti memorizzati nella cache di hello provenienti da diversi sistemi back-end di hello risposte primarie.</span><span class="sxs-lookup"><span data-stu-id="f8472-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="f8472-145">Controllo delle versioni trasparente</span><span class="sxs-lookup"><span data-stu-id="f8472-145">Transparent versioning</span></span>
<span data-ttu-id="f8472-146">È pratica comune per più versioni di implementazione diversa di un toobe API supportate in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="f8472-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="f8472-147">Questo è probabilmente toosupport diversi ambienti, ad esempio sviluppo, test, produzione e così via, o potrebbe essere toosupport le versioni precedenti di tempo toogive hello API per le versioni dell'API consumer toomigrate toonewer.</span><span class="sxs-lookup"><span data-stu-id="f8472-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="f8472-148">Un approccio toohandling questo invece della richiesta client sviluppatori toochange hello URL da `/v1/customers` troppo`/v2/customers` è toostore nei dati di profilo del consumer hello quale versione di hello API sono attualmente desidera toouse e chiamare hello appropriato URL di back-end.</span><span class="sxs-lookup"><span data-stu-id="f8472-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="f8472-149">In ordine toodetermine hello back-end corretto URL toocall per un particolare client, è necessario tooquery alcuni dati di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f8472-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="f8472-150">Memorizzazione nella cache di dati di configurazione, è possibile ridurre al minimo il calo di prestazioni hello di eseguire la ricerca.</span><span class="sxs-lookup"><span data-stu-id="f8472-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="f8472-151">primo passaggio Hello è l'identificatore hello toodetermine utilizzato tooconfigure versione desiderata di hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="f8472-152">In questo esempio, si è deciso di chiave di sottoscrizione prodotto versione toohello tooassociate hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="f8472-153">È quindi possibile eseguire un toosee ricerca cache se è già stato recuperato versione di hello client desiderato.</span><span class="sxs-lookup"><span data-stu-id="f8472-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="f8472-154">Quindi selezionare toosee se non c' nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="f8472-155">Se non è presente, è possibile recuperarla.</span><span class="sxs-lookup"><span data-stu-id="f8472-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="f8472-156">Estrarre il testo del corpo di risposta hello dalla risposta hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="f8472-157">Memorizzarlo nella cache di hello per utilizzi futuri.</span><span class="sxs-lookup"><span data-stu-id="f8472-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="f8472-158">E infine hello back-end URL tooselect hello versione dell'aggiornamento del servizio hello desiderata dal client hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="f8472-159">Hello completamente criteri sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="f8472-159">hello completely policy is as follows.</span></span>

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

<span data-ttu-id="f8472-160">Abilitazione del controllo del consumer API tootransparently quale versione di back-end si accede dai client senza dovere tooupdate e ridistribuire i client è una soluzione elegante che consente di risolvere numerosi problemi di controllo delle versioni delle API.</span><span class="sxs-lookup"><span data-stu-id="f8472-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="f8472-161">Isolamento dei tenant</span><span class="sxs-lookup"><span data-stu-id="f8472-161">Tenant Isolation</span></span>
<span data-ttu-id="f8472-162">Nelle distribuzioni multi-tenant di grandi dimensioni alcune aziende creano gruppi di tenant separati in distribuzioni distinte dell'hardware back-end.</span><span class="sxs-lookup"><span data-stu-id="f8472-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="f8472-163">Consente di ridurre il numero di hello di clienti che sono interessati da un problema hardware sul back-end hello.</span><span class="sxs-lookup"><span data-stu-id="f8472-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="f8472-164">Consente inoltre di nuovo toobe di versioni di software di implementazione in fasi.</span><span class="sxs-lookup"><span data-stu-id="f8472-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="f8472-165">Idealmente, questa architettura di back-end deve essere trasparente tooAPI consumer.</span><span class="sxs-lookup"><span data-stu-id="f8472-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="f8472-166">Questo può essere realizzato in un simile modo tootransparent il controllo delle versioni perché si basa su hello stessa tecnica di manipolazione hello URL di back-end usando lo stato di configurazione per ogni chiave API.</span><span class="sxs-lookup"><span data-stu-id="f8472-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="f8472-167">Anziché restituire una versione preferita di hello API per ogni chiave di sottoscrizione, viene restituito un identificatore che si riferisce a un gruppo di componenti hardware tenant toohello assegnato.</span><span class="sxs-lookup"><span data-stu-id="f8472-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="f8472-168">Tale identificatore può essere utilizzato tooconstruct hello back-end appropriata URL.</span><span class="sxs-lookup"><span data-stu-id="f8472-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="f8472-169">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="f8472-169">Summary</span></span>
<span data-ttu-id="f8472-170">hello toouse di libertà Hello cache di gestione API di Azure per l'archiviazione di qualsiasi tipo di dati consente dati tooconfiguration accesso efficiente che possono influire sulla modalità di hello che viene elaborata una richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="f8472-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="f8472-171">Può anche essere utilizzati toostore i frammenti di dati che è possono migliorare le risposte, restituite dall'API back-end.</span><span class="sxs-lookup"><span data-stu-id="f8472-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8472-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f8472-172">Next steps</span></span>
<span data-ttu-id="f8472-173">Per commenti e suggerimenti in hello thread di Disqus per questo argomento se sono presenti altri scenari di questi criteri sono abilitati per è, o se sono presenti scenari desidera tooachieve ma non è attualmente possibile.</span><span class="sxs-lookup"><span data-stu-id="f8472-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

