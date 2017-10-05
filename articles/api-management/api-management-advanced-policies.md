---
title: Criteri avanzati di Gestione API di Azure | Microsoft Docs
description: Informazioni sui criteri avanzati disponibili per l'uso in Gestione API di Azure.
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
ms.openlocfilehash: 0c65ac74316421a0258f01143baa25ffecb5be3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="2ace5-103">Criteri avanzati di gestione API</span><span class="sxs-lookup"><span data-stu-id="2ace5-103">API Management advanced policies</span></span>
<span data-ttu-id="2ace5-104">Questo argomento fornisce un riferimento per i criteri di Gestione API seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="2ace5-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="2ace5-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="2ace5-106"><a name="AdvancedPolicies"></a>Criteri avanzati</span><span class="sxs-lookup"><span data-stu-id="2ace5-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="2ace5-107">[Controlla flusso](api-management-advanced-policies.md#choose): applica in modo condizionale le istruzioni dei criteri sulla base dei risultati della valutazione di [espressioni](api-management-policy-expressions.md) booleane.</span><span class="sxs-lookup"><span data-stu-id="2ace5-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="2ace5-108">[Inoltra richiesta](#ForwardRequest) : inoltra la richiesta al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="2ace5-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>

-   <span data-ttu-id="2ace5-109">[Limita la concorrenza](#LimitConcurrency): previene ai criteri racchiusi l’esecuzione di un numero maggiore di richieste contemporaneamente rispetto a quello specificato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than the specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="2ace5-110">[Registra in Hub eventi](#log-to-eventhub): invia messaggi nel formato specificato a un Hub eventi definito da un'entità Logger.</span><span class="sxs-lookup"><span data-stu-id="2ace5-110">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="2ace5-111">[Restituisci risposta](#mock-response): interrompe l'esecuzione della pipeline e restituisce una risposta fittizia direttamente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="2ace5-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="2ace5-112">[Riprova](#Retry) : riprova l'esecuzione delle istruzioni dei criteri, se e fino a quando non viene soddisfatta la condizione.</span><span class="sxs-lookup"><span data-stu-id="2ace5-112">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="2ace5-113">L'esecuzione verrà ripetuta a specifici intervalli di tempo e per il numero di tentativi indicato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-113">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="2ace5-114">[Restituisci risposta](#ReturnResponse) : l’esecuzione nella pipeline viene interrotta e viene restituita la risposta specificata direttamente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="2ace5-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span> 
  
-   <span data-ttu-id="2ace5-115">[Invia richiesta unidirezionale](#SendOneWayRequest) : invia una richiesta all'URL specificato senza attendere una risposta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-115">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="2ace5-116">[Invia richiesta](#SendRequest) : invia una richiesta all'URL specificato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-116">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  

-   <span data-ttu-id="2ace5-117">[Imposta proxy HTTP](#SetHttpProxy): consente di indirizzare le richieste inoltrate tramite un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ace5-117">[Set HTTP proxy](#SetHttpProxy) - Allows you to route forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="2ace5-118">[Imposta metodo di richiesta](#SetRequestMethod) : consente di modificare il metodo HTTP per una richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-118">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="2ace5-119">[Imposta codice di stato](#SetStatus): modifica il codice di stato HTTP per il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-119">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="2ace5-120">[Imposta variabile](api-management-advanced-policies.md#set-variable): rende persistente un valore in una variabile di [contesto](api-management-policy-expressions.md#ContextVariables) denominata e consente di accedervi in un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="2ace5-121">[Traccia](#Trace): aggiunge una stringa nell'output di [Controllo API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="2ace5-121">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="2ace5-122">[Attendi](#Wait): attende il completamento dei criteri inclusi per l'[invio della richiesta](api-management-advanced-policies.md#SendRequest), il [recupero del valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey) o il [flusso di controllo](api-management-advanced-policies.md#choose) prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="2ace5-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <span data-ttu-id="2ace5-123"><a name="choose"></a>Flusso di controllo</span><span class="sxs-lookup"><span data-stu-id="2ace5-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="2ace5-124">Il criterio `choose` si applica alle istruzioni del criterio incluse in base al risultato della valutazione di espressioni booleane, simili a un costrutto if-then-else o switch in un linguaggio di programmazione.</span><span class="sxs-lookup"><span data-stu-id="2ace5-124">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="2ace5-125"><a name="ChoosePolicyStatement"></a>Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="2ace5-126">Il criterio del flusso di controllo deve contenere almeno un elemento `<when/>`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-126">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="2ace5-127">L'elemento `<otherwise/>` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-127">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="2ace5-128">Le condizioni negli elementi `<when/>` vengono valutate in ordine di visualizzazione all'interno del criterio.</span><span class="sxs-lookup"><span data-stu-id="2ace5-128">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="2ace5-129">Si applicano le istruzioni del criterio incluse all'interno del primo elemento `<when/>` con attributo di condizione uguale a `true`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-129">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="2ace5-130">I criteri inclusi all'interno dell'elemento `<otherwise/>`, se presente, vengono applicati se tutti gli attributi di condizione dell'elemento `<when/>` sono `false`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-130">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="2ace5-131">Esempi</span><span class="sxs-lookup"><span data-stu-id="2ace5-131">Examples</span></span>  
  
####  <span data-ttu-id="2ace5-132"><a name="ChooseExample"></a>Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="2ace5-133">L'esempio seguente illustra un criterio [set-variable](api-management-advanced-policies.md#set-variable) e due criteri di flusso di controllo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-133">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="2ace5-134">Il criterio di impostazione della variabile si trova nella sezione in ingresso e crea `isMobile`, una variabile di [contesto](api-management-policy-expressions.md#ContextVariables) booleana, che è impostata su true se l'intestazione della richiesta `User-Agent` contiene il testo `iPad` o `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-134">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="2ace5-135">Il primo criterio di flusso di controllo è disponibile anche nella sezione in ingresso e applica in modo condizionale uno dei due criteri [Imposta parametro di stringa della query](api-management-transformation-policies.md#SetQueryStringParameter) in base al valore della variabile di contesto `isMobile`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-135">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="2ace5-136">Il secondo criterio di flusso di controllo si trova nella sezione in uscita e applica in modo condizionale il criterio [Converti XML in JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) quando `isMobile` è impostato su `true`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-136">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="2ace5-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-137">Example</span></span>  
 <span data-ttu-id="2ace5-138">Questo esempio mostra come eseguire operazioni di filtro sui contenuti rimuovendo elementi di dati dalla risposta ricevuta dal servizio back-end quando si usa il prodotto `Starter`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-138">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="2ace5-139">Per una dimostrazione relativa alla configurazione e all'uso di questo criterio, vedere l'[episodio 177 di Cloud Cover su altre funzionalità di Gestione API con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e passare direttamente al minuto 34:30.</span><span class="sxs-lookup"><span data-stu-id="2ace5-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="2ace5-140">Iniziare dal minuto 31:50 per visualizzare una panoramica di [The Dark Sky Forecast API](https://developer.forecast.io/), l'API usata in questa dimostrazione.</span><span class="sxs-lookup"><span data-stu-id="2ace5-140">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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
  
### <a name="elements"></a><span data-ttu-id="2ace5-141">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-141">Elements</span></span>  
  
|<span data-ttu-id="2ace5-142">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-142">Element</span></span>|<span data-ttu-id="2ace5-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-143">Description</span></span>|<span data-ttu-id="2ace5-144">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-145">choose</span><span class="sxs-lookup"><span data-stu-id="2ace5-145">choose</span></span>|<span data-ttu-id="2ace5-146">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-146">Root element.</span></span>|<span data-ttu-id="2ace5-147">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-147">Yes</span></span>|  
|<span data-ttu-id="2ace5-148">when</span><span class="sxs-lookup"><span data-stu-id="2ace5-148">when</span></span>|<span data-ttu-id="2ace5-149">La condizione da usare per le parti `if` o `ifelse` del criterio `choose`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-149">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="2ace5-150">Se il criterio `choose` ha più sezioni `when`, vengono valutate in modo sequenziale.</span><span class="sxs-lookup"><span data-stu-id="2ace5-150">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="2ace5-151">Una volta che la `condition` di un elemento when risulta `true`, non vengono valutate altre condizioni `when`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-151">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="2ace5-152">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-152">Yes</span></span>|  
|<span data-ttu-id="2ace5-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="2ace5-153">otherwise</span></span>|<span data-ttu-id="2ace5-154">Contiene il frammento di criterio da usare se nessuna delle condizioni `when` viene valutata `true`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-154">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="2ace5-155">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-156">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-156">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-157">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-157">Attribute</span></span>|<span data-ttu-id="2ace5-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-158">Description</span></span>|<span data-ttu-id="2ace5-159">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="2ace5-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="2ace5-161">La costante o espressione booleana da valutare quando viene valutata l'istruzione del criterio contenente `when`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-161">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="2ace5-162">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-162">Yes</span></span>|  
  
###  <span data-ttu-id="2ace5-163"><a name="ChooseUsage"></a>Uso</span><span class="sxs-lookup"><span data-stu-id="2ace5-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="2ace5-164">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-164">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-165">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-166">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2ace5-167"><a name="ForwardRequest"></a>Inoltra richiesta</span><span class="sxs-lookup"><span data-stu-id="2ace5-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="2ace5-168">Il criterio `forward-request` inoltra la richiesta in ingresso al servizio back-end specificato nel [contesto](api-management-policy-expressions.md#ContextVariables) della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-168">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="2ace5-169">L'URL del servizio back-end è specificato nelle [impostazioni](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) API e può essere modificato tramite il criterio [imposta servizio back-end](api-management-transformation-policies.md).</span><span class="sxs-lookup"><span data-stu-id="2ace5-169">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2ace5-170">Se questo criterio viene rimosso, la richiesta non viene inoltrata al servizio back-end e i criteri nella sezione in uscita vengono valutati immediatamente dopo il completamento dei criteri nella sezione in ingresso.</span><span class="sxs-lookup"><span data-stu-id="2ace5-170">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-171">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="2ace5-172">Esempi</span><span class="sxs-lookup"><span data-stu-id="2ace5-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="2ace5-173">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-173">Example</span></span>  
 <span data-ttu-id="2ace5-174">Il criterio a livello di API seguente inoltra tutte le richieste al servizio back-end con un intervallo di timeout di 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="2ace5-174">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="2ace5-175">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-175">Example</span></span>  
 <span data-ttu-id="2ace5-176">Questo criterio a livello di operazione usa l'elemento `base` per ereditare il criterio di back-end dall'ambito di livello API padre.</span><span class="sxs-lookup"><span data-stu-id="2ace5-176">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="2ace5-177">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-177">Example</span></span>  
 <span data-ttu-id="2ace5-178">Questo criterio a livello di operazione inoltra in modo esplicito tutte le richieste al servizio back-end con un timeout di 120 e non eredita il criterio di back-end a livello API padre.</span><span class="sxs-lookup"><span data-stu-id="2ace5-178">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="2ace5-179">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-179">Example</span></span>  
 <span data-ttu-id="2ace5-180">Questo criterio a livello di operazione non inoltra le richieste al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="2ace5-180">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="2ace5-181">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-181">Elements</span></span>  
  
|<span data-ttu-id="2ace5-182">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-182">Element</span></span>|<span data-ttu-id="2ace5-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-183">Description</span></span>|<span data-ttu-id="2ace5-184">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="2ace5-185">forward-request</span></span>|<span data-ttu-id="2ace5-186">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-186">Root element.</span></span>|<span data-ttu-id="2ace5-187">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-188">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-188">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-189">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-189">Attribute</span></span>|<span data-ttu-id="2ace5-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-190">Description</span></span>|<span data-ttu-id="2ace5-191">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-191">Required</span></span>|<span data-ttu-id="2ace5-192">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2ace5-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="2ace5-193">timeout="integer"</span></span>|<span data-ttu-id="2ace5-194">Intervallo di timeout in secondi prima che la chiamata al servizio back-end abbia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-194">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="2ace5-195">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-195">No</span></span>|<span data-ttu-id="2ace5-196">No timeout</span><span class="sxs-lookup"><span data-stu-id="2ace5-196">No timeout</span></span>|  
|<span data-ttu-id="2ace5-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="2ace5-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="2ace5-198">Specifica se i reindirizzamenti dal servizio back-end sono seguiti dal gateway o restituiti al chiamante.</span><span class="sxs-lookup"><span data-stu-id="2ace5-198">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="2ace5-199">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-199">No</span></span>|<span data-ttu-id="2ace5-200">false</span><span class="sxs-lookup"><span data-stu-id="2ace5-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-201">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-201">Usage</span></span>  
 <span data-ttu-id="2ace5-202">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-203">**Sezioni del criterio:** back-end</span><span class="sxs-lookup"><span data-stu-id="2ace5-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="2ace5-204">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2ace5-205"><a name="LimitConcurrency"></a>Limita concorrenza</span><span class="sxs-lookup"><span data-stu-id="2ace5-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="2ace5-206">Il criterio `limit-concurrency` previene ai criteri racchiusi l’esecuzione di un numero maggiore di richieste in un dato momento rispetto a quello specificato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-206">The `limit-concurrency` policy prevents enclosed policies from executing by more than the specified number of requests at a given time.</span></span> <span data-ttu-id="2ace5-207">In caso di superamento della soglia, le nuove richieste vengono aggiunte a una coda, fino a raggiungere la lunghezza massima della coda.</span><span class="sxs-lookup"><span data-stu-id="2ace5-207">Upon exceeding the threshold, new requests are added to a queue, until the maximum queue length is achieved.</span></span> <span data-ttu-id="2ace5-208">Al momento di esaurimento della coda, le nuove richieste avranno immediatamente esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="2ace5-209"><a name="LimitConcurrencyStatement"></a>Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="2ace5-210">esempi</span><span class="sxs-lookup"><span data-stu-id="2ace5-210">Examples</span></span>  
  
####  <span data-ttu-id="2ace5-211"><a name="ChooseExample"></a>Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="2ace5-212">Nell'esempio seguente viene illustrato come limitare il numero di richieste inoltrate a un back-end in base al valore di una variabile di contesto.</span><span class="sxs-lookup"><span data-stu-id="2ace5-212">The following example demonstrates how to limit number of requests forwarded to a backend based on the value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="2ace5-213">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-213">Elements</span></span>  
  
|<span data-ttu-id="2ace5-214">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-214">Element</span></span>|<span data-ttu-id="2ace5-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-215">Description</span></span>|<span data-ttu-id="2ace5-216">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="2ace5-217">limita concorrenza</span><span class="sxs-lookup"><span data-stu-id="2ace5-217">limit-concurrency</span></span>|<span data-ttu-id="2ace5-218">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-218">Root element.</span></span>|<span data-ttu-id="2ace5-219">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-220">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-220">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-221">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-221">Attribute</span></span>|<span data-ttu-id="2ace5-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-222">Description</span></span>|<span data-ttu-id="2ace5-223">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-223">Required</span></span>|<span data-ttu-id="2ace5-224">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="2ace5-225">key</span><span class="sxs-lookup"><span data-stu-id="2ace5-225">key</span></span>|<span data-ttu-id="2ace5-226">Stringa.</span><span class="sxs-lookup"><span data-stu-id="2ace5-226">A string.</span></span> <span data-ttu-id="2ace5-227">Espressione consentita.</span><span class="sxs-lookup"><span data-stu-id="2ace5-227">Expression allowed.</span></span> <span data-ttu-id="2ace5-228">Specifica l'ambito di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="2ace5-228">Specifies the concurrency scope.</span></span> <span data-ttu-id="2ace5-229">Può essere condivisa da più criteri.</span><span class="sxs-lookup"><span data-stu-id="2ace5-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="2ace5-230">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-230">Yes</span></span>|<span data-ttu-id="2ace5-231">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-231">N/A</span></span>|  
|<span data-ttu-id="2ace5-232">numero max</span><span class="sxs-lookup"><span data-stu-id="2ace5-232">max-count</span></span>|<span data-ttu-id="2ace5-233">Un intero.</span><span class="sxs-lookup"><span data-stu-id="2ace5-233">An integer.</span></span> <span data-ttu-id="2ace5-234">Specifica un numero massimo di richieste autorizzate ad accedere al criterio.</span><span class="sxs-lookup"><span data-stu-id="2ace5-234">Specifies a maximum number of requests that are allowed to enter the policy.</span></span>|<span data-ttu-id="2ace5-235">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-235">Yes</span></span>|<span data-ttu-id="2ace5-236">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-236">N/A</span></span>|  
|<span data-ttu-id="2ace5-237">timeout</span><span class="sxs-lookup"><span data-stu-id="2ace5-237">timeout</span></span>|<span data-ttu-id="2ace5-238">Un intero.</span><span class="sxs-lookup"><span data-stu-id="2ace5-238">An integer.</span></span> <span data-ttu-id="2ace5-239">Espressione consentita.</span><span class="sxs-lookup"><span data-stu-id="2ace5-239">Expression allowed.</span></span> <span data-ttu-id="2ace5-240">Specifica il numero di secondi che una richiesta deve attendere per accedere a un ambito prima che si verifichi "403 numero eccessivo di richieste"</span><span class="sxs-lookup"><span data-stu-id="2ace5-240">Specifies the number of seconds a request should wait to enter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="2ace5-241">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-241">No</span></span>|<span data-ttu-id="2ace5-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="2ace5-242">Infinity</span></span>|  
|<span data-ttu-id="2ace5-243">lunghezza massima della coda</span><span class="sxs-lookup"><span data-stu-id="2ace5-243">max-queue-length</span></span>|<span data-ttu-id="2ace5-244">Un intero.</span><span class="sxs-lookup"><span data-stu-id="2ace5-244">An integer.</span></span> <span data-ttu-id="2ace5-245">Espressione consentita.</span><span class="sxs-lookup"><span data-stu-id="2ace5-245">Expression allowed.</span></span> <span data-ttu-id="2ace5-246">Specifica la lunghezza massima della coda.</span><span class="sxs-lookup"><span data-stu-id="2ace5-246">Specifies the maximum queue length.</span></span> <span data-ttu-id="2ace5-247">Le richieste in entrata che provano ad accedere a questo criterio verranno interrotta con "403 numero eccessivo di richieste" immediatamente quando la coda è esaurita.</span><span class="sxs-lookup"><span data-stu-id="2ace5-247">Incoming requests trying to enter this policy will be terminated with “403 Too Many Requests” immediately when the queue is exhausted.</span></span>|<span data-ttu-id="2ace5-248">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-248">No</span></span>|<span data-ttu-id="2ace5-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="2ace5-249">Infinity</span></span>|  
  
###  <span data-ttu-id="2ace5-250"><a name="ChooseUsage"></a>Uso</span><span class="sxs-lookup"><span data-stu-id="2ace5-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="2ace5-251">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-251">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-252">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-253">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="2ace5-254"><a name="log-to-eventhub"></a>Registra in Hub eventi</span><span class="sxs-lookup"><span data-stu-id="2ace5-254"><a name="log-to-eventhub"></a> Log to Event Hub</span></span>  
 <span data-ttu-id="2ace5-255">Il criterio `log-to-eventhub` invia messaggi nel formato specificato a un Hub eventi definito da un'entità Logger.</span><span class="sxs-lookup"><span data-stu-id="2ace5-255">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="2ace5-256">Come suggerisce il nome, il criterio viene usato per il salvataggio di informazioni selezionate sul contesto di richiesta o risposta per l'analisi online o offline.</span><span class="sxs-lookup"><span data-stu-id="2ace5-256">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2ace5-257">Per una guida dettagliata sulla configurazione di un hub eventi e la registrazione di eventi, vedere [Come registrare eventi nell'Hub eventi di Azure in Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="2ace5-257">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-258">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2ace5-259">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-259">Example</span></span>  
 <span data-ttu-id="2ace5-260">È possibile usare qualsiasi stringa come valore da registrare in Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2ace5-260">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="2ace5-261">In questo esempio la data e l'ora, il nome del servizio di distribuzione, l'ID della richiesta, l'indirizzo IP e il nome dell'operazione per tutte le chiamate in entrata vengono registrati nel Logger dell'hub eventi registrato con l'ID `contoso-logger`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-261">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2ace5-262">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-262">Elements</span></span>  
  
|<span data-ttu-id="2ace5-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-263">Element</span></span>|<span data-ttu-id="2ace5-264">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-264">Description</span></span>|<span data-ttu-id="2ace5-265">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="2ace5-266">log-to-eventhub</span></span>|<span data-ttu-id="2ace5-267">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-267">Root element.</span></span> <span data-ttu-id="2ace5-268">Il valore di questo elemento è la stringa per la registrazione all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2ace5-268">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="2ace5-269">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-270">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-270">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-271">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-271">Attribute</span></span>|<span data-ttu-id="2ace5-272">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-272">Description</span></span>|<span data-ttu-id="2ace5-273">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="2ace5-274">logger-id</span></span>|<span data-ttu-id="2ace5-275">ID del Logger registrato con il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="2ace5-275">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="2ace5-276">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-276">Yes</span></span>|  
|<span data-ttu-id="2ace5-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="2ace5-277">partition-id</span></span>|<span data-ttu-id="2ace5-278">Specifica l'indice della partizione a cui i messaggi vengono inviati.</span><span class="sxs-lookup"><span data-stu-id="2ace5-278">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="2ace5-279">facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-279">Optional.</span></span> <span data-ttu-id="2ace5-280">Questo attributo non può essere usato se si usa `partition-key`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="2ace5-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="2ace5-281">partition-key</span></span>|<span data-ttu-id="2ace5-282">Specifica il valore usato per l'assegnazione della partizione quando vengono inviati i messaggi.</span><span class="sxs-lookup"><span data-stu-id="2ace5-282">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="2ace5-283">facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-283">Optional.</span></span> <span data-ttu-id="2ace5-284">Questo attributo non può essere usato se si usa `partition-id`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-285">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-285">Usage</span></span>  
 <span data-ttu-id="2ace5-286">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-286">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-287">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-288">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="2ace5-289"><a name="mock-response"></a> Restituisci risposta</span><span class="sxs-lookup"><span data-stu-id="2ace5-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="2ace5-290">Il criterio `mock-response`, come implica il nome, viene usato per restituire API e operazioni.</span><span class="sxs-lookup"><span data-stu-id="2ace5-290">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="2ace5-291">Interrompe la normale esecuzione della pipeline e restituisce una risposta fittizia direttamente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="2ace5-291">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="2ace5-292">Il criterio cerca sempre di restituire risposte della massima fedeltà.</span><span class="sxs-lookup"><span data-stu-id="2ace5-292">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="2ace5-293">Include esempi di contenuto di risposta ogni volta che è possibile.</span><span class="sxs-lookup"><span data-stu-id="2ace5-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="2ace5-294">Nelle situazioni in cui vengono forniti schemi ma non esempi, genera risposte di esempio dagli schemi.</span><span class="sxs-lookup"><span data-stu-id="2ace5-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="2ace5-295">Se non sono presenti né esempi né schemi, restituisce risposte senza contenuto.</span><span class="sxs-lookup"><span data-stu-id="2ace5-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-296">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="2ace5-297">esempi</span><span class="sxs-lookup"><span data-stu-id="2ace5-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="2ace5-298">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-298">Elements</span></span>  
  
|<span data-ttu-id="2ace5-299">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-299">Element</span></span>|<span data-ttu-id="2ace5-300">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-300">Description</span></span>|<span data-ttu-id="2ace5-301">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="2ace5-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="2ace5-302">mock-response</span></span>|<span data-ttu-id="2ace5-303">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-303">Root element.</span></span>|<span data-ttu-id="2ace5-304">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-305">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-305">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-306">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-306">Attribute</span></span>|<span data-ttu-id="2ace5-307">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-307">Description</span></span>|<span data-ttu-id="2ace5-308">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-308">Required</span></span>|<span data-ttu-id="2ace5-309">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="2ace5-310">status-code</span><span class="sxs-lookup"><span data-stu-id="2ace5-310">status-code</span></span>|<span data-ttu-id="2ace5-311">Specifica il codice di stato della risposta e viene usato per selezionare l'esempio o lo schema corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-311">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="2ace5-312">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-312">No</span></span>|<span data-ttu-id="2ace5-313">200</span><span class="sxs-lookup"><span data-stu-id="2ace5-313">200</span></span>|  
|<span data-ttu-id="2ace5-314">content-type</span><span class="sxs-lookup"><span data-stu-id="2ace5-314">content-type</span></span>|<span data-ttu-id="2ace5-315">Specifica il valore di intestazione della risposta `Content-Type` e viene usato per selezionare l'esempio o lo schema corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-315">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="2ace5-316">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-316">No</span></span>|<span data-ttu-id="2ace5-317">None</span><span class="sxs-lookup"><span data-stu-id="2ace5-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-318">Uso</span><span class="sxs-lookup"><span data-stu-id="2ace5-318">Usage</span></span>  
 <span data-ttu-id="2ace5-319">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-319">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-320">**Sezioni del criterio:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-321">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="2ace5-322"><a name="Retry"></a> Riprova</span><span class="sxs-lookup"><span data-stu-id="2ace5-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="2ace5-323">Il criterio `retry` esegue i criteri figlio una volta e quindi ritenta l'esecuzione degli stessi fino a quando il tentativo `condition` diventa `false` o fino a esaurimento del tentativo `count`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-323">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-324">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="2ace5-325">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-325">Example</span></span>  
 <span data-ttu-id="2ace5-326">Nella richiesta di esempio seguente l'inoltro viene ripetuto fino a dieci volte usando un algoritmo di ripetizione esponenziale.</span><span class="sxs-lookup"><span data-stu-id="2ace5-326">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="2ace5-327">Poiché `first-fast-retry` è impostato su false, tutti i tentativi sono soggetti all'algoritmo di ripetizione esponenziale.</span><span class="sxs-lookup"><span data-stu-id="2ace5-327">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2ace5-328">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-328">Elements</span></span>  
  
|<span data-ttu-id="2ace5-329">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-329">Element</span></span>|<span data-ttu-id="2ace5-330">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-330">Description</span></span>|<span data-ttu-id="2ace5-331">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-332">retry</span><span class="sxs-lookup"><span data-stu-id="2ace5-332">retry</span></span>|<span data-ttu-id="2ace5-333">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-333">Root element.</span></span> <span data-ttu-id="2ace5-334">Può contenere tutti gli altri criteri come elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="2ace5-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="2ace5-335">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-336">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-336">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-337">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-337">Attribute</span></span>|<span data-ttu-id="2ace5-338">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-338">Description</span></span>|<span data-ttu-id="2ace5-339">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-339">Required</span></span>|<span data-ttu-id="2ace5-340">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2ace5-341">condition</span><span class="sxs-lookup"><span data-stu-id="2ace5-341">condition</span></span>|<span data-ttu-id="2ace5-342">Valore letterale booleano o [espressione](api-management-policy-expressions.md) che specifica se i tentativi devono essere interrotti (`false`) o devono continuare (`true`).</span><span class="sxs-lookup"><span data-stu-id="2ace5-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="2ace5-343">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-343">Yes</span></span>|<span data-ttu-id="2ace5-344">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-344">N/A</span></span>|  
|<span data-ttu-id="2ace5-345">count</span><span class="sxs-lookup"><span data-stu-id="2ace5-345">count</span></span>|<span data-ttu-id="2ace5-346">Numero positivo che specifica il numero massimo di tentativi da eseguire.</span><span class="sxs-lookup"><span data-stu-id="2ace5-346">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="2ace5-347">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-347">Yes</span></span>|<span data-ttu-id="2ace5-348">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-348">N/A</span></span>|  
|<span data-ttu-id="2ace5-349">interval</span><span class="sxs-lookup"><span data-stu-id="2ace5-349">interval</span></span>|<span data-ttu-id="2ace5-350">Numero positivo in secondi che specifica l'intervallo di attesa tra i tentativi di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="2ace5-350">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="2ace5-351">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-351">Yes</span></span>|<span data-ttu-id="2ace5-352">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-352">N/A</span></span>|  
|<span data-ttu-id="2ace5-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="2ace5-353">max-interval</span></span>|<span data-ttu-id="2ace5-354">Un numero positivo che specifica l'intervallo di attesa massimo tra i tentativi di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="2ace5-354">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="2ace5-355">Viene usato per implementare un algoritmo di ripetizione esponenziale.</span><span class="sxs-lookup"><span data-stu-id="2ace5-355">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="2ace5-356">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-356">No</span></span>|<span data-ttu-id="2ace5-357">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-357">N/A</span></span>|  
|<span data-ttu-id="2ace5-358">delta</span><span class="sxs-lookup"><span data-stu-id="2ace5-358">delta</span></span>|<span data-ttu-id="2ace5-359">Numero positivo in secondi che specifica l'incremento dell'intervallo di attesa.</span><span class="sxs-lookup"><span data-stu-id="2ace5-359">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="2ace5-360">Viene usato per implementare gli algoritmi di ripetizione lineari ed esponenziali.</span><span class="sxs-lookup"><span data-stu-id="2ace5-360">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="2ace5-361">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-361">No</span></span>|<span data-ttu-id="2ace5-362">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-362">N/A</span></span>|  
|<span data-ttu-id="2ace5-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="2ace5-363">first-fast-retry</span></span>|<span data-ttu-id="2ace5-364">Se impostato su `true`, il primo tentativo di ripetizione viene eseguito immediatamente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-364">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="2ace5-365">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="2ace5-366">Se è specificato solo `interval`, vengono eseguiti tentativi a intervallo **fisso**.</span><span class="sxs-lookup"><span data-stu-id="2ace5-366">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="2ace5-367">Se vengono specificati solo `interval` e `delta`, viene usato un algoritmo di ripetizione a intervalli **lineari**, in cui il tempo di attesa tra i tentativi viene calcolato secondo la formula seguente: `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-367">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="2ace5-368">Se vengono specificati `interval`, `max-interval` e `delta`,viene applicato un algoritmo di ripetizione a intervalli **esponenziali**, in cui il tempo di attesa tra i tentativi cresce in modo esponenziale dal valore `interval` al valore `max-interval`, secondo la formula seguente: `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-368">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="2ace5-369">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-369">Usage</span></span>  
 <span data-ttu-id="2ace5-370">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-370">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="2ace5-371">Si noti che le restrizioni sull'uso dei criteri figlio verranno ereditate da questo criterio.</span><span class="sxs-lookup"><span data-stu-id="2ace5-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="2ace5-372">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-373">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2ace5-374"><a name="ReturnResponse"></a>Restituisci risposta</span><span class="sxs-lookup"><span data-stu-id="2ace5-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="2ace5-375">Il criterio `return-response` interrompe l'esecuzione della pipeline e restituisce al chiamante una risposta predefinita o personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2ace5-375">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="2ace5-376">La risposta predefinita è `200 OK`, senza corpo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="2ace5-377">La risposta personalizzata può essere specificata tramite una variabile di contesto o le istruzioni del criterio.</span><span class="sxs-lookup"><span data-stu-id="2ace5-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="2ace5-378">Quando entrambi sono specificati, la risposta contenuta all'interno della variabile di contesto viene modificata tramite le istruzioni del criterio prima di essere restituita al chiamante.</span><span class="sxs-lookup"><span data-stu-id="2ace5-378">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-379">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2ace5-380">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="2ace5-381">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-381">Elements</span></span>  
  
|<span data-ttu-id="2ace5-382">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-382">Element</span></span>|<span data-ttu-id="2ace5-383">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-383">Description</span></span>|<span data-ttu-id="2ace5-384">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-385">return-response</span><span class="sxs-lookup"><span data-stu-id="2ace5-385">return-response</span></span>|<span data-ttu-id="2ace5-386">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-386">Root element.</span></span>|<span data-ttu-id="2ace5-387">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-387">Yes</span></span>|  
|<span data-ttu-id="2ace5-388">set-header</span><span class="sxs-lookup"><span data-stu-id="2ace5-388">set-header</span></span>|<span data-ttu-id="2ace5-389">Istruzione del criterio.[set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="2ace5-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="2ace5-390">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-390">No</span></span>|  
|<span data-ttu-id="2ace5-391">set-body</span><span class="sxs-lookup"><span data-stu-id="2ace5-391">set-body</span></span>|<span data-ttu-id="2ace5-392">Istruzione del criterio.[set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="2ace5-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="2ace5-393">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-393">No</span></span>|  
|<span data-ttu-id="2ace5-394">set-status</span><span class="sxs-lookup"><span data-stu-id="2ace5-394">set-status</span></span>|<span data-ttu-id="2ace5-395">Istruzione del criterio [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="2ace5-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="2ace5-396">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-397">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-397">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-398">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-398">Attribute</span></span>|<span data-ttu-id="2ace5-399">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-399">Description</span></span>|<span data-ttu-id="2ace5-400">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="2ace5-401">response-variable-name</span></span>|<span data-ttu-id="2ace5-402">Nome della variabile di contesto a cui fa riferimento, ad esempio, un criterio di upstream [send-request](api-management-advanced-policies.md#SendRequest) e contenente un oggetto `Response`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-402">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="2ace5-403">facoltativo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-404">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-404">Usage</span></span>  
 <span data-ttu-id="2ace5-405">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-405">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-406">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-407">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2ace5-408"><a name="SendOneWayRequest"></a>Invia richiesta unidirezionale</span><span class="sxs-lookup"><span data-stu-id="2ace5-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="2ace5-409">Il criterio `send-one-way-request` invia la richiesta specificata all'URL specificato senza attendere una risposta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-409">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-410">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2ace5-411">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-411">Example</span></span>  
 <span data-ttu-id="2ace5-412">Questo criterio di esempio illustra come usare il criterio `send-one-way-request` per inviare un messaggio a una chat di Slack, se il codice della risposta HTTP è maggiore o uguale a 500.</span><span class="sxs-lookup"><span data-stu-id="2ace5-412">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="2ace5-413">Per altre informazioni relative a questo esempio, vedere [Uso di servizi esterni dal servizio Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="2ace5-413">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2ace5-414">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-414">Elements</span></span>  
  
|<span data-ttu-id="2ace5-415">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-415">Element</span></span>|<span data-ttu-id="2ace5-416">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-416">Description</span></span>|<span data-ttu-id="2ace5-417">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="2ace5-418">send-one-way-request</span></span>|<span data-ttu-id="2ace5-419">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-419">Root element.</span></span>|<span data-ttu-id="2ace5-420">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-420">Yes</span></span>|  
|<span data-ttu-id="2ace5-421">URL</span><span class="sxs-lookup"><span data-stu-id="2ace5-421">url</span></span>|<span data-ttu-id="2ace5-422">URL della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-422">The URL of the request.</span></span>|<span data-ttu-id="2ace5-423">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="2ace5-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="2ace5-424">statico</span><span class="sxs-lookup"><span data-stu-id="2ace5-424">method</span></span>|<span data-ttu-id="2ace5-425">Metodo HTTP usato nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-425">The HTTP method for the request.</span></span>|<span data-ttu-id="2ace5-426">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="2ace5-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="2ace5-427">intestazione</span><span class="sxs-lookup"><span data-stu-id="2ace5-427">header</span></span>|<span data-ttu-id="2ace5-428">Intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-428">Request header.</span></span> <span data-ttu-id="2ace5-429">Usare più elementi di intestazione per più intestazioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="2ace5-430">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-430">No</span></span>|  
|<span data-ttu-id="2ace5-431">body</span><span class="sxs-lookup"><span data-stu-id="2ace5-431">body</span></span>|<span data-ttu-id="2ace5-432">Corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-432">The request body.</span></span>|<span data-ttu-id="2ace5-433">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-434">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-434">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-435">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-435">Attribute</span></span>|<span data-ttu-id="2ace5-436">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-436">Description</span></span>|<span data-ttu-id="2ace5-437">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-437">Required</span></span>|<span data-ttu-id="2ace5-438">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2ace5-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="2ace5-439">mode="string"</span></span>|<span data-ttu-id="2ace5-440">Determina se questa è una nuova richiesta o una copia della richiesta corrente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-440">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="2ace5-441">In modalità in uscita, mode=copy non avvia il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-441">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="2ace5-442">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-442">No</span></span>|<span data-ttu-id="2ace5-443">Nuovo</span><span class="sxs-lookup"><span data-stu-id="2ace5-443">New</span></span>|  
|<span data-ttu-id="2ace5-444">name</span><span class="sxs-lookup"><span data-stu-id="2ace5-444">name</span></span>|<span data-ttu-id="2ace5-445">Specifica il nome dell'intestazione da impostare.</span><span class="sxs-lookup"><span data-stu-id="2ace5-445">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="2ace5-446">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-446">Yes</span></span>|<span data-ttu-id="2ace5-447">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-447">N/A</span></span>|  
|<span data-ttu-id="2ace5-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="2ace5-448">exists-action</span></span>|<span data-ttu-id="2ace5-449">Specifica l'azione da eseguire quando l'intestazione è già specificata.</span><span class="sxs-lookup"><span data-stu-id="2ace5-449">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="2ace5-450">Questo attributo deve avere uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-450">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="2ace5-451">-   override - sostituisce il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-451">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="2ace5-452">-   skip - non sostituisce il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-452">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="2ace5-453">-   append - aggiunge il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-453">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="2ace5-454">-   delete - elimina l'intestazione dalla richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-454">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="2ace5-455">Se è impostato su `override`, l'integrazione di più voci con lo stesso nome avrà come risultato l'impostazione dell'intestazione in base a tutte le voci, che saranno elencate più volte. Nel risultato saranno impostati solo i valori elencati.</span><span class="sxs-lookup"><span data-stu-id="2ace5-455">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="2ace5-456">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-456">No</span></span>|<span data-ttu-id="2ace5-457">override</span><span class="sxs-lookup"><span data-stu-id="2ace5-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-458">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-458">Usage</span></span>  
 <span data-ttu-id="2ace5-459">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-459">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-460">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-461">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2ace5-462"><a name="SendRequest"></a> Invio richiesta</span><span class="sxs-lookup"><span data-stu-id="2ace5-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="2ace5-463">Il criterio `send-request` invia la richiesta fornita all'URL specificato, attendendo non oltre il valore di timeout impostato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-463">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-464">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2ace5-465">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-465">Example</span></span>  
 <span data-ttu-id="2ace5-466">Questo esempio mostra un metodo per verificare un token di riferimento con un server di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="2ace5-466">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="2ace5-467">Per altre informazioni relative a questo esempio, vedere [Uso di servizi esterni dal servizio Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="2ace5-467">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
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
  
### <a name="elements"></a><span data-ttu-id="2ace5-468">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-468">Elements</span></span>  
  
|<span data-ttu-id="2ace5-469">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-469">Element</span></span>|<span data-ttu-id="2ace5-470">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-470">Description</span></span>|<span data-ttu-id="2ace5-471">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-472">send-request</span><span class="sxs-lookup"><span data-stu-id="2ace5-472">send-request</span></span>|<span data-ttu-id="2ace5-473">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-473">Root element.</span></span>|<span data-ttu-id="2ace5-474">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-474">Yes</span></span>|  
|<span data-ttu-id="2ace5-475">URL</span><span class="sxs-lookup"><span data-stu-id="2ace5-475">url</span></span>|<span data-ttu-id="2ace5-476">URL della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-476">The URL of the request.</span></span>|<span data-ttu-id="2ace5-477">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="2ace5-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="2ace5-478">statico</span><span class="sxs-lookup"><span data-stu-id="2ace5-478">method</span></span>|<span data-ttu-id="2ace5-479">Metodo HTTP usato nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-479">The HTTP method for the request.</span></span>|<span data-ttu-id="2ace5-480">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="2ace5-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="2ace5-481">intestazione</span><span class="sxs-lookup"><span data-stu-id="2ace5-481">header</span></span>|<span data-ttu-id="2ace5-482">Intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-482">Request header.</span></span> <span data-ttu-id="2ace5-483">Usare più elementi di intestazione per più intestazioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="2ace5-484">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-484">No</span></span>|  
|<span data-ttu-id="2ace5-485">body</span><span class="sxs-lookup"><span data-stu-id="2ace5-485">body</span></span>|<span data-ttu-id="2ace5-486">Corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-486">The request body.</span></span>|<span data-ttu-id="2ace5-487">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-488">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-488">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-489">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-489">Attribute</span></span>|<span data-ttu-id="2ace5-490">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-490">Description</span></span>|<span data-ttu-id="2ace5-491">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-491">Required</span></span>|<span data-ttu-id="2ace5-492">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2ace5-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="2ace5-493">mode="string"</span></span>|<span data-ttu-id="2ace5-494">Determina se questa è una nuova richiesta o una copia della richiesta corrente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-494">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="2ace5-495">In modalità in uscita, mode=copy non avvia il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-495">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="2ace5-496">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-496">No</span></span>|<span data-ttu-id="2ace5-497">Nuovo</span><span class="sxs-lookup"><span data-stu-id="2ace5-497">New</span></span>|  
|<span data-ttu-id="2ace5-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="2ace5-498">response-variable-name="string"</span></span>|<span data-ttu-id="2ace5-499">Se non è presente, viene usato `context.Response`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="2ace5-500">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-500">No</span></span>|<span data-ttu-id="2ace5-501">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-501">N/A</span></span>|  
|<span data-ttu-id="2ace5-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="2ace5-502">timeout="integer"</span></span>|<span data-ttu-id="2ace5-503">Intervallo di timeout in secondi prima che la chiamata all'URL abbia esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-503">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="2ace5-504">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-504">No</span></span>|<span data-ttu-id="2ace5-505">60</span><span class="sxs-lookup"><span data-stu-id="2ace5-505">60</span></span>|  
|<span data-ttu-id="2ace5-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-506">ignore-error</span></span>|<span data-ttu-id="2ace5-507">Se impostato su true e la richiesta restituisce un errore:</span><span class="sxs-lookup"><span data-stu-id="2ace5-507">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="2ace5-508">- Se è stato specificato response-variable-name, questo conterrà un valore null.</span><span class="sxs-lookup"><span data-stu-id="2ace5-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="2ace5-509">- Se response-variable-name non è stato specificato, context.Request non verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="2ace5-510">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-510">No</span></span>|<span data-ttu-id="2ace5-511">false</span><span class="sxs-lookup"><span data-stu-id="2ace5-511">false</span></span>|  
|<span data-ttu-id="2ace5-512">name</span><span class="sxs-lookup"><span data-stu-id="2ace5-512">name</span></span>|<span data-ttu-id="2ace5-513">Specifica il nome dell'intestazione da impostare.</span><span class="sxs-lookup"><span data-stu-id="2ace5-513">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="2ace5-514">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-514">Yes</span></span>|<span data-ttu-id="2ace5-515">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-515">N/A</span></span>|  
|<span data-ttu-id="2ace5-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="2ace5-516">exists-action</span></span>|<span data-ttu-id="2ace5-517">Specifica l'azione da eseguire quando l'intestazione è già specificata.</span><span class="sxs-lookup"><span data-stu-id="2ace5-517">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="2ace5-518">Questo attributo deve avere uno dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-518">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="2ace5-519">-   override - sostituisce il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-519">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="2ace5-520">-   skip - non sostituisce il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-520">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="2ace5-521">-   append - aggiunge il valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="2ace5-521">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="2ace5-522">-   delete - elimina l'intestazione dalla richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-522">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="2ace5-523">Se è impostato su `override`, l'integrazione di più voci con lo stesso nome avrà come risultato l'impostazione dell'intestazione in base a tutte le voci, che saranno elencate più volte. Nel risultato saranno impostati solo i valori elencati.</span><span class="sxs-lookup"><span data-stu-id="2ace5-523">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="2ace5-524">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-524">No</span></span>|<span data-ttu-id="2ace5-525">override</span><span class="sxs-lookup"><span data-stu-id="2ace5-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-526">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-526">Usage</span></span>  
 <span data-ttu-id="2ace5-527">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-527">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-528">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-529">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2ace5-530"><a name="SetHttpProxy"></a>Impostare il proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="2ace5-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="2ace5-531">Il criterio `proxy` consente di indirizzare le richieste inoltrate ai back-end tramite un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ace5-531">The `proxy` policy allows you to route requests forwarded to backends via an HTTP proxy.</span></span> <span data-ttu-id="2ace5-532">È supportato solo HTTP (non HTTPS) tra il gateway e il proxy.</span><span class="sxs-lookup"><span data-stu-id="2ace5-532">Only HTTP (not HTTPS) is supported between the gateway and the proxy.</span></span> <span data-ttu-id="2ace5-533">Solo autenticazione Basic e NTLM.</span><span class="sxs-lookup"><span data-stu-id="2ace5-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-534">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="2ace5-535">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-535">Example</span></span>  
<span data-ttu-id="2ace5-536">Si noti l'utilizzo di [proprietà](api-management-howto-properties.md) come valori di nome utente e password per evitare di archiviare informazioni riservate nel documento dei criteri.</span><span class="sxs-lookup"><span data-stu-id="2ace5-536">Note the use of [properties](api-management-howto-properties.md) as values of the username and password to avoid storing sensitive information in the policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="2ace5-537">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-537">Elements</span></span>  
  
|<span data-ttu-id="2ace5-538">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-538">Element</span></span>|<span data-ttu-id="2ace5-539">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-539">Description</span></span>|<span data-ttu-id="2ace5-540">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-541">proxy</span><span class="sxs-lookup"><span data-stu-id="2ace5-541">proxy</span></span>|<span data-ttu-id="2ace5-542">Elemento radice</span><span class="sxs-lookup"><span data-stu-id="2ace5-542">Root element</span></span>|<span data-ttu-id="2ace5-543">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="2ace5-544">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-544">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-545">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-545">Attribute</span></span>|<span data-ttu-id="2ace5-546">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-546">Description</span></span>|<span data-ttu-id="2ace5-547">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-547">Required</span></span>|<span data-ttu-id="2ace5-548">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2ace5-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="2ace5-549">url="string"</span></span>|<span data-ttu-id="2ace5-550">URL del proxy nel formato http://host:port.</span><span class="sxs-lookup"><span data-stu-id="2ace5-550">Proxy URL in the form of http://host:port.</span></span>|<span data-ttu-id="2ace5-551">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-551">Yes</span></span>|<span data-ttu-id="2ace5-552">N/D </span><span class="sxs-lookup"><span data-stu-id="2ace5-552">N/A</span></span>|  
|<span data-ttu-id="2ace5-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="2ace5-553">username="string"</span></span>|<span data-ttu-id="2ace5-554">Nome utente da usare per l'autenticazione con il proxy.</span><span class="sxs-lookup"><span data-stu-id="2ace5-554">Username to be used for authentication with the proxy.</span></span>|<span data-ttu-id="2ace5-555">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-555">No</span></span>|<span data-ttu-id="2ace5-556">N/D </span><span class="sxs-lookup"><span data-stu-id="2ace5-556">N/A</span></span>|  
|<span data-ttu-id="2ace5-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="2ace5-557">password="string"</span></span>|<span data-ttu-id="2ace5-558">Password da usare per l'autenticazione con il proxy.</span><span class="sxs-lookup"><span data-stu-id="2ace5-558">Password to be used for authentication with the proxy.</span></span>|<span data-ttu-id="2ace5-559">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-559">No</span></span>|<span data-ttu-id="2ace5-560">N/D </span><span class="sxs-lookup"><span data-stu-id="2ace5-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="2ace5-561">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-561">Usage</span></span>  
 <span data-ttu-id="2ace5-562">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-562">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-563">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="2ace5-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="2ace5-564">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="2ace5-565"><a name="SetRequestMethod"></a> Impostare il metodo di richiesta</span><span class="sxs-lookup"><span data-stu-id="2ace5-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="2ace5-566">Il criterio `set-method` consente di modificare il metodo di richiesta HTTP per una richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ace5-566">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-567">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2ace5-568">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-568">Example</span></span>  
 <span data-ttu-id="2ace5-569">Questo criterio di esempio che usa il criterio `set-method` mostra un esempio di invio di un messaggio a una chat di Slack, se il codice della risposta HTTP è maggiore o uguale a 500.</span><span class="sxs-lookup"><span data-stu-id="2ace5-569">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="2ace5-570">Per altre informazioni relative a questo esempio, vedere [Uso di servizi esterni dal servizio Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="2ace5-570">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2ace5-571">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-571">Elements</span></span>  
  
|<span data-ttu-id="2ace5-572">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-572">Element</span></span>|<span data-ttu-id="2ace5-573">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-573">Description</span></span>|<span data-ttu-id="2ace5-574">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-575">set-method</span><span class="sxs-lookup"><span data-stu-id="2ace5-575">set-method</span></span>|<span data-ttu-id="2ace5-576">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-576">Root element.</span></span> <span data-ttu-id="2ace5-577">Il valore dell'elemento specifica il metodo HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ace5-577">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="2ace5-578">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-579">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-579">Usage</span></span>  
 <span data-ttu-id="2ace5-580">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-580">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-581">**Sezioni del criterio:** inbound, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-582">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2ace5-583"><a name="SetStatus"></a> Impostare il codice di stato</span><span class="sxs-lookup"><span data-stu-id="2ace5-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="2ace5-584">Il criterio `set-status` modifica il codice di stato HTTP sul valore specificato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-584">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-585">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2ace5-586">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-586">Example</span></span>  
 <span data-ttu-id="2ace5-587">Questo esempio illustra come restituire una risposta 401 se il token di autorizzazione non è valido.</span><span class="sxs-lookup"><span data-stu-id="2ace5-587">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="2ace5-588">Per altre informazioni, vedere [Uso di servizi esterni dal servizio Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="2ace5-588">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2ace5-589">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-589">Elements</span></span>  
  
|<span data-ttu-id="2ace5-590">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-590">Element</span></span>|<span data-ttu-id="2ace5-591">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-591">Description</span></span>|<span data-ttu-id="2ace5-592">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-593">set-status</span><span class="sxs-lookup"><span data-stu-id="2ace5-593">set-status</span></span>|<span data-ttu-id="2ace5-594">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-594">Root element.</span></span>|<span data-ttu-id="2ace5-595">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-596">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-596">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-597">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-597">Attribute</span></span>|<span data-ttu-id="2ace5-598">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-598">Description</span></span>|<span data-ttu-id="2ace5-599">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-599">Required</span></span>|<span data-ttu-id="2ace5-600">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2ace5-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="2ace5-601">code="integer"</span></span>|<span data-ttu-id="2ace5-602">Il codice di stato HTTP da restituire.</span><span class="sxs-lookup"><span data-stu-id="2ace5-602">The HTTP status code to return.</span></span>|<span data-ttu-id="2ace5-603">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-603">Yes</span></span>|<span data-ttu-id="2ace5-604">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-604">N/A</span></span>|  
|<span data-ttu-id="2ace5-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="2ace5-605">reason="string"</span></span>|<span data-ttu-id="2ace5-606">Descrizione del motivo per la restituzione del codice di stato.</span><span class="sxs-lookup"><span data-stu-id="2ace5-606">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="2ace5-607">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-607">Yes</span></span>|<span data-ttu-id="2ace5-608">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-609">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-609">Usage</span></span>  
 <span data-ttu-id="2ace5-610">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-610">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-611">**Sezioni del criterio:** outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-612">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="2ace5-613"><a name="set-variable"></a>Impostare una variabile</span><span class="sxs-lookup"><span data-stu-id="2ace5-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="2ace5-614">Il criterio `set-variable` dichiara una variabile di [contesto](api-management-policy-expressions.md#ContextVariables) e assegna a essa un valore specificato tramite un'[espressione](api-management-policy-expressions.md) o un valore letterale di stringa.</span><span class="sxs-lookup"><span data-stu-id="2ace5-614">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="2ace5-615">Se l'espressione contiene un valore letterale, questo verrà convertito in una stringa e il tipo di valore sarà `System.String`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-615">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="2ace5-616"><a name="set-variablePolicyStatement"></a>Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="2ace5-617"><a name="set-variableExample"></a>Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="2ace5-618">L'esempio seguente illustra un criterio di impostazione della variabile nella sezione in ingresso.</span><span class="sxs-lookup"><span data-stu-id="2ace5-618">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="2ace5-619">Il criterio di impostazione della variabile crea `isMobile`, una variabile di [contesto](api-management-policy-expressions.md#ContextVariables) booleana, che è impostata su true se l'intestazione della richiesta `User-Agent` contiene il testo `iPad` o `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="2ace5-620">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-620">Elements</span></span>  
  
|<span data-ttu-id="2ace5-621">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-621">Element</span></span>|<span data-ttu-id="2ace5-622">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-622">Description</span></span>|<span data-ttu-id="2ace5-623">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="2ace5-624">set-variable</span></span>|<span data-ttu-id="2ace5-625">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-625">Root element.</span></span>|<span data-ttu-id="2ace5-626">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-627">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-627">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-628">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-628">Attribute</span></span>|<span data-ttu-id="2ace5-629">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-629">Description</span></span>|<span data-ttu-id="2ace5-630">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-631">name</span><span class="sxs-lookup"><span data-stu-id="2ace5-631">name</span></span>|<span data-ttu-id="2ace5-632">Nome della variabile.</span><span class="sxs-lookup"><span data-stu-id="2ace5-632">The name of the variable.</span></span>|<span data-ttu-id="2ace5-633">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-633">Yes</span></span>|  
|<span data-ttu-id="2ace5-634">value</span><span class="sxs-lookup"><span data-stu-id="2ace5-634">value</span></span>|<span data-ttu-id="2ace5-635">Valore della variabile.</span><span class="sxs-lookup"><span data-stu-id="2ace5-635">The value of the variable.</span></span> <span data-ttu-id="2ace5-636">Può essere un'espressione o un valore letterale.</span><span class="sxs-lookup"><span data-stu-id="2ace5-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="2ace5-637">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-638">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-638">Usage</span></span>  
 <span data-ttu-id="2ace5-639">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-639">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-640">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-641">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="2ace5-642"><a name="set-variableAllowedTypes"></a>Tipi consentiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="2ace5-643">Le espressioni usate nel criterio `set-variable` devono restituire uno dei seguenti tipi di base.</span><span class="sxs-lookup"><span data-stu-id="2ace5-643">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="2ace5-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="2ace5-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="2ace5-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="2ace5-645">System.SByte</span></span>  
  
-   <span data-ttu-id="2ace5-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="2ace5-646">System.Byte</span></span>  
  
-   <span data-ttu-id="2ace5-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="2ace5-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="2ace5-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="2ace5-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="2ace5-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="2ace5-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="2ace5-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="2ace5-650">System.Int16</span></span>  
  
-   <span data-ttu-id="2ace5-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="2ace5-651">System.Int32</span></span>  
  
-   <span data-ttu-id="2ace5-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="2ace5-652">System.Int64</span></span>  
  
-   <span data-ttu-id="2ace5-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="2ace5-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="2ace5-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="2ace5-654">System.Single</span></span>  
  
-   <span data-ttu-id="2ace5-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="2ace5-655">System.Double</span></span>  
  
-   <span data-ttu-id="2ace5-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="2ace5-656">System.Guid</span></span>  
  
-   <span data-ttu-id="2ace5-657">System.String</span><span class="sxs-lookup"><span data-stu-id="2ace5-657">System.String</span></span>  
  
-   <span data-ttu-id="2ace5-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="2ace5-658">System.Char</span></span>  
  
-   <span data-ttu-id="2ace5-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="2ace5-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="2ace5-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2ace5-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="2ace5-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="2ace5-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="2ace5-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="2ace5-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="2ace5-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="2ace5-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="2ace5-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="2ace5-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="2ace5-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="2ace5-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="2ace5-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="2ace5-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="2ace5-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="2ace5-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="2ace5-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="2ace5-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="2ace5-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="2ace5-669">System.Single?</span></span>  
  
-   <span data-ttu-id="2ace5-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="2ace5-670">System.Double?</span></span>  
  
-   <span data-ttu-id="2ace5-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="2ace5-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="2ace5-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="2ace5-672">System.String?</span></span>  
  
-   <span data-ttu-id="2ace5-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="2ace5-673">System.Char?</span></span>  
  
-   <span data-ttu-id="2ace5-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="2ace5-674">System.DateTime?</span></span>  

##  <span data-ttu-id="2ace5-675"><a name="Trace"></a> Traccia</span><span class="sxs-lookup"><span data-stu-id="2ace5-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="2ace5-676">Il criterio `trace` aggiunge una stringa nell'output di [Controllo API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="2ace5-676">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="2ace5-677">Il criterio verrà eseguito solo quando la traccia è attivata, ad esempio quando è presente l'intestazione della richiesta `Ocp-Apim-Trace` ed è impostata su `true` e quando è presente l'intestazione della richiesta `Ocp-Apim-Subscription-Key` e contiene una chiave valida associata all'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="2ace5-677">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-678">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="2ace5-679">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-679">Elements</span></span>  
  
|<span data-ttu-id="2ace5-680">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-680">Element</span></span>|<span data-ttu-id="2ace5-681">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-681">Description</span></span>|<span data-ttu-id="2ace5-682">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-683">trace</span><span class="sxs-lookup"><span data-stu-id="2ace5-683">trace</span></span>|<span data-ttu-id="2ace5-684">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-684">Root element.</span></span>|<span data-ttu-id="2ace5-685">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-686">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-686">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-687">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-687">Attribute</span></span>|<span data-ttu-id="2ace5-688">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-688">Description</span></span>|<span data-ttu-id="2ace5-689">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-689">Required</span></span>|<span data-ttu-id="2ace5-690">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2ace5-691">una sezione source</span><span class="sxs-lookup"><span data-stu-id="2ace5-691">source</span></span>|<span data-ttu-id="2ace5-692">Valore letterale della stringa significativo per il visualizzatore di tracce e che specifica l'origine del messaggio.</span><span class="sxs-lookup"><span data-stu-id="2ace5-692">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="2ace5-693">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-693">Yes</span></span>|<span data-ttu-id="2ace5-694">N/D</span><span class="sxs-lookup"><span data-stu-id="2ace5-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-695">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-695">Usage</span></span>  
 <span data-ttu-id="2ace5-696">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-696">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="2ace5-697">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="2ace5-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="2ace5-698">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="2ace5-699"><a name="Wait"></a> Attesa</span><span class="sxs-lookup"><span data-stu-id="2ace5-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="2ace5-700">Il criterio `wait` esegue i criteri figlio immediati in parallelo e attende che tutti o uno dei relativi criteri figlio immediati vengano completati prima di terminare la sua attività.</span><span class="sxs-lookup"><span data-stu-id="2ace5-700">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="2ace5-701">I criteri di attesa possono avere come criteri figlio immediati i criteri [Invio della richiesta](api-management-advanced-policies.md#SendRequest), [Recupero del valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey) e [Flusso di controllo](api-management-advanced-policies.md#choose).</span><span class="sxs-lookup"><span data-stu-id="2ace5-701">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2ace5-702">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="2ace5-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="2ace5-703">Esempio</span><span class="sxs-lookup"><span data-stu-id="2ace5-703">Example</span></span>  
 <span data-ttu-id="2ace5-704">L'esempio seguente contiene due criteri `choose` come criteri figlio immediato dei criteri `wait`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-704">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="2ace5-705">Ognuno di questi criteri `choose` viene eseguito in parallelo.</span><span class="sxs-lookup"><span data-stu-id="2ace5-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="2ace5-706">Ogni criterio `choose` tenta di recuperare un valore memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="2ace5-706">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="2ace5-707">Se si verifica un mancato riscontro nella cache, viene chiamato un servizio di back-end per fornire il valore.</span><span class="sxs-lookup"><span data-stu-id="2ace5-707">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="2ace5-708">In questo esempio il criterio `wait` non si completa fino al completamento di tutti i relativi criteri figlio immediati, poiché l'attributo `for` è impostato su `all`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-708">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="2ace5-709">In questo esempio le variabili di contesto (`execute-branch-one`, `value-one`, `execute-branch-two` e `value-two`) vengono dichiarate all'esterno dell'ambito di questo criterio di esempio.</span><span class="sxs-lookup"><span data-stu-id="2ace5-709">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="2ace5-710">Elementi</span><span class="sxs-lookup"><span data-stu-id="2ace5-710">Elements</span></span>  
  
|<span data-ttu-id="2ace5-711">Elemento</span><span class="sxs-lookup"><span data-stu-id="2ace5-711">Element</span></span>|<span data-ttu-id="2ace5-712">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-712">Description</span></span>|<span data-ttu-id="2ace5-713">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="2ace5-714">wait</span><span class="sxs-lookup"><span data-stu-id="2ace5-714">wait</span></span>|<span data-ttu-id="2ace5-715">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="2ace5-715">Root element.</span></span> <span data-ttu-id="2ace5-716">Può contenere come elementi figlio solo i criteri `send-request`, `cache-lookup-value` e `choose`.</span><span class="sxs-lookup"><span data-stu-id="2ace5-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="2ace5-717">Sì</span><span class="sxs-lookup"><span data-stu-id="2ace5-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2ace5-718">Attributi</span><span class="sxs-lookup"><span data-stu-id="2ace5-718">Attributes</span></span>  
  
|<span data-ttu-id="2ace5-719">Attributo</span><span class="sxs-lookup"><span data-stu-id="2ace5-719">Attribute</span></span>|<span data-ttu-id="2ace5-720">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ace5-720">Description</span></span>|<span data-ttu-id="2ace5-721">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="2ace5-721">Required</span></span>|<span data-ttu-id="2ace5-722">Default</span><span class="sxs-lookup"><span data-stu-id="2ace5-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="2ace5-723">for</span><span class="sxs-lookup"><span data-stu-id="2ace5-723">for</span></span>|<span data-ttu-id="2ace5-724">Determina se il criterio `wait` attende il completamento di tutti o solo uno dei criteri figlio immediati.</span><span class="sxs-lookup"><span data-stu-id="2ace5-724">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="2ace5-725">I valori consentiti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ace5-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="2ace5-726">-   `all`: consente di attendere il completamento di tutti i criteri figlio immediati</span><span class="sxs-lookup"><span data-stu-id="2ace5-726">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="2ace5-727">-   any: consente di attendere il completamento di uno dei criteri figlio immediati.</span><span class="sxs-lookup"><span data-stu-id="2ace5-727">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="2ace5-728">Dopo il completamento del primo criterio figlio immediato, il criterio `wait` si completa e l'esecuzione di qualsiasi altro criterio figlio immediato viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="2ace5-728">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="2ace5-729">No</span><span class="sxs-lookup"><span data-stu-id="2ace5-729">No</span></span>|<span data-ttu-id="2ace5-730">tutti</span><span class="sxs-lookup"><span data-stu-id="2ace5-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2ace5-731">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="2ace5-731">Usage</span></span>  
 <span data-ttu-id="2ace5-732">Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) del criterio seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ace5-732">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2ace5-733">**Sezioni del criterio:** inbound, outbound, back-end</span><span class="sxs-lookup"><span data-stu-id="2ace5-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="2ace5-734">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="2ace5-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="2ace5-735">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ace5-735">Next steps</span></span>
<span data-ttu-id="2ace5-736">Per altre informazioni sull'uso di questi criteri, vedere:</span><span class="sxs-lookup"><span data-stu-id="2ace5-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="2ace5-737">Criteri in Gestione API</span><span class="sxs-lookup"><span data-stu-id="2ace5-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="2ace5-738">Espressioni di criteri</span><span class="sxs-lookup"><span data-stu-id="2ace5-738">Policy expressions</span></span>](api-management-policy-expressions.md)
