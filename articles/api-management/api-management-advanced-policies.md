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
# <a name="api-management-advanced-policies"></a><span data-ttu-id="779c6-103">Criteri avanzati di gestione API</span><span class="sxs-lookup"><span data-stu-id="779c6-103">API Management advanced policies</span></span>
<span data-ttu-id="779c6-104">In questo argomento fornisce un riferimento per i seguenti criteri di gestione API hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="779c6-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="779c6-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="779c6-106"><a name="AdvancedPolicies"></a>Criteri avanzati</span><span class="sxs-lookup"><span data-stu-id="779c6-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="779c6-107">[Flusso di controllo](api-management-advanced-policies.md#choose) : in modo condizionale istruzioni dei criteri in base ai risultati di hello di valutazione di hello Boolean applica [espressioni](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="779c6-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="779c6-108">[Inoltro della richiesta](#ForwardRequest) -inoltra servizio back-end di hello richiesta toohello.</span><span class="sxs-lookup"><span data-stu-id="779c6-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="779c6-109">[Limita la concorrenza](#LimitConcurrency) -impedisce racchiuso tra i criteri di esecuzione di più di hello numero specificato di richieste in un momento.</span><span class="sxs-lookup"><span data-stu-id="779c6-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="779c6-110">[Log tooEvent Hub](#log-to-eventhub) -invia messaggi hello specificato formato tooan Hub di eventi definito da un'entità del Logger.</span><span class="sxs-lookup"><span data-stu-id="779c6-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="779c6-111">[Simulare risposta](#mock-response) -esecuzione nella pipeline viene interrotta e restituisce una risposta simulata direttamente toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="779c6-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="779c6-112">[Ripetere](#Retry) -esecuzione di tentativi di hello racchiuso tra istruzioni dei criteri, se e fino a quando non viene soddisfatta la condizione hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="779c6-113">Esecuzione viene ripetuto in intervalli di tempo specificati hello e backup toohello specificato numero di tentativi.</span><span class="sxs-lookup"><span data-stu-id="779c6-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="779c6-114">[Restituire una risposta](#ReturnResponse) -hello di esecuzione e restituisce pipeline interruzioni specificato risposta direttamente toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="779c6-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="779c6-115">[Inviare una richiesta unidirezionale](#SendOneWayRequest) -invia una richiesta toohello URL specificato senza attendere una risposta.</span><span class="sxs-lookup"><span data-stu-id="779c6-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="779c6-116">[Invio richiesta](#SendRequest) -invia una richiesta toohello URL specificato.</span><span class="sxs-lookup"><span data-stu-id="779c6-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="779c6-117">[Impostazione del proxy HTTP](#SetHttpProxy) -consente le richieste di tooroute inoltrati tramite un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="779c6-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="779c6-118">[Impostare il metodo di richiesta](#SetRequestMethod) -consente di determinare il metodo HTTP hello toochange per una richiesta.</span><span class="sxs-lookup"><span data-stu-id="779c6-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="779c6-119">[Impostare il codice di stato](#SetStatus) -toohello di codice stato HTTP hello modifiche valore specificato.</span><span class="sxs-lookup"><span data-stu-id="779c6-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="779c6-120">[Imposta variabile](api-management-advanced-policies.md#set-variable): rende persistente un valore in una variabile di [contesto](api-management-policy-expressions.md#ContextVariables) denominata e consente di accedervi in un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="779c6-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="779c6-121">[Traccia](#Trace) -aggiunge una stringa hello [API controllo](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span><span class="sxs-lookup"><span data-stu-id="779c6-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="779c6-122">[Attesa](#Wait) -attende racchiusi [richiesta di invio](api-management-advanced-policies.md#SendRequest), [ottenere valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey), o [flusso di controllo](api-management-advanced-policies.md#choose) toocomplete criteri prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="779c6-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="779c6-123"><a name="choose"></a>Flusso di controllo</span><span class="sxs-lookup"><span data-stu-id="779c6-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="779c6-124">Hello `choose` criteri si applicano criteri racchiuse costruiscono istruzioni in base hello risultato della valutazione di espressioni booleane, simile tooan if-then-else o un'opzione in un linguaggio di programmazione.</span><span class="sxs-lookup"><span data-stu-id="779c6-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="779c6-125"><a name="ChoosePolicyStatement"></a>Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
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
  
 <span data-ttu-id="779c6-126">Hello il criterio di flusso di controllo deve contenere almeno un `<when/>` elemento.</span><span class="sxs-lookup"><span data-stu-id="779c6-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="779c6-127">Hello `<otherwise/>` elemento è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="779c6-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="779c6-128">Le condizioni nella `<when/>` elementi vengono valutati nell'ordine di visualizzazione nel criterio hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="779c6-129">Le istruzioni del criterio racchiuse hello innanzitutto `<when/>` elemento con attributo di condizione `true` verranno applicate.</span><span class="sxs-lookup"><span data-stu-id="779c6-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="779c6-130">Criteri racchiuso tra parentesi hello `<otherwise/>` elemento, se presente, verrà applicato se in tutti di hello `<when/>` sono attributi dell'elemento condizione `false`.</span><span class="sxs-lookup"><span data-stu-id="779c6-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="779c6-131">esempi</span><span class="sxs-lookup"><span data-stu-id="779c6-131">Examples</span></span>  
  
####  <span data-ttu-id="779c6-132"><a name="ChooseExample"></a>Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="779c6-133">Hello esempio seguente viene illustrato un [set-variable](api-management-advanced-policies.md#set-variable) due criteri di flusso di controllo e i criteri.</span><span class="sxs-lookup"><span data-stu-id="779c6-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="779c6-134">Hello set variabile criteri si trovano in hello sezione in ingresso e crea un `isMobile` booleano [contesto](api-management-policy-expressions.md#ContextVariables) variabile impostata tootrue se hello `User-Agent` richiesta intestazione contiene testo hello `iPad` o `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="779c6-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="779c6-135">criterio del flusso di controllo prima Hello è anche hello sezione in ingresso e applica in modo condizionale uno dei due [impostare il parametro di stringa di query](api-management-transformation-policies.md#SetQueryStringParameter) criteri in base al valore di hello di hello `isMobile` variabile di contesto.</span><span class="sxs-lookup"><span data-stu-id="779c6-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="779c6-136">criterio del flusso di controllo secondo Hello nella sezione in uscita hello e applica in modo condizionale hello [convertire XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) criteri quando `isMobile` è troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="779c6-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="779c6-137">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-137">Example</span></span>  
 <span data-ttu-id="779c6-138">Questo esempio viene illustrato come tooperform contenuto applicando un filtro per la rimozione degli elementi di dati dalla risposta hello ricevuto dal servizio back-end hello quando si utilizza hello `Starter` prodotto.</span><span class="sxs-lookup"><span data-stu-id="779c6-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="779c6-139">Per una dimostrazione della configurazione e l'utilizzo di questo criterio, vedere [Cloud coprire episodio 177: più API le funzionalità di gestione con Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e far avanzare rapidamente too34:30.</span><span class="sxs-lookup"><span data-stu-id="779c6-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="779c6-140">Inizia dal 31:50 toosee Cenni preliminari [hello scuro Sky previsione API](https://developer.forecast.io/) utilizzato per questa dimostrazione.</span><span class="sxs-lookup"><span data-stu-id="779c6-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-141">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-141">Elements</span></span>  
  
|<span data-ttu-id="779c6-142">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-142">Element</span></span>|<span data-ttu-id="779c6-143">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-143">Description</span></span>|<span data-ttu-id="779c6-144">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-145">choose</span><span class="sxs-lookup"><span data-stu-id="779c6-145">choose</span></span>|<span data-ttu-id="779c6-146">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-146">Root element.</span></span>|<span data-ttu-id="779c6-147">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-147">Yes</span></span>|  
|<span data-ttu-id="779c6-148">when</span><span class="sxs-lookup"><span data-stu-id="779c6-148">when</span></span>|<span data-ttu-id="779c6-149">Hello toouse condizione per hello `if` o `ifelse` parti di hello `choose` criteri.</span><span class="sxs-lookup"><span data-stu-id="779c6-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="779c6-150">Se hello `choose` criteri ha più `when` sezioni, vengono valutati in sequenza.</span><span class="sxs-lookup"><span data-stu-id="779c6-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="779c6-151">Una volta hello `condition` di un oggetto quando l'elemento restituisce troppo`true`e non per ulteriormente `when` condizioni vengono valutate.</span><span class="sxs-lookup"><span data-stu-id="779c6-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="779c6-152">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-152">Yes</span></span>|  
|<span data-ttu-id="779c6-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="779c6-153">otherwise</span></span>|<span data-ttu-id="779c6-154">Contiene hello criteri frammento toobe utilizzati se nessuna delle hello `when` condizioni restituiscono troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="779c6-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="779c6-155">No</span><span class="sxs-lookup"><span data-stu-id="779c6-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-156">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-156">Attributes</span></span>  
  
|<span data-ttu-id="779c6-157">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-157">Attribute</span></span>|<span data-ttu-id="779c6-158">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-158">Description</span></span>|<span data-ttu-id="779c6-159">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="779c6-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="779c6-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="779c6-161">espressione booleana Hello o costante tooevaluated quando hello contenente `when` viene valutata l'istruzione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="779c6-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="779c6-162">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-162">Yes</span></span>|  
  
###  <span data-ttu-id="779c6-163"><a name="ChooseUsage"></a>Uso</span><span class="sxs-lookup"><span data-stu-id="779c6-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="779c6-164">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-165">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-166">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="779c6-167"><a name="ForwardRequest"></a>Inoltra richiesta</span><span class="sxs-lookup"><span data-stu-id="779c6-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="779c6-168">Hello `forward-request` criterio inoltra hello in arrivo richiesta toohello servizio back-end specificato nella richiesta di hello [contesto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="779c6-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="779c6-169">Hello URL del servizio back-end specificato nel hello API [impostazioni](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) e può essere modificato utilizzando hello [impostare servizio back-end](api-management-transformation-policies.md) criteri.</span><span class="sxs-lookup"><span data-stu-id="779c6-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="779c6-170">Rimozione di richiesta di hello non vengono inoltrati criteri toohello back-end del servizio e hello nella sezione in uscita hello i risultati dei criteri vengono valutati immediatamente dopo il completamento di hello dei criteri di hello in hello in ingresso di sezione.</span><span class="sxs-lookup"><span data-stu-id="779c6-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-171">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="779c6-172">Esempi</span><span class="sxs-lookup"><span data-stu-id="779c6-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="779c6-173">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-173">Example</span></span>  
 <span data-ttu-id="779c6-174">Hello seguente criterio a livello di API inoltra tutte le richieste di servizio back-end toohello con un intervallo di timeout di 60 secondi.</span><span class="sxs-lookup"><span data-stu-id="779c6-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="779c6-175">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-175">Example</span></span>  
 <span data-ttu-id="779c6-176">Questo criterio a livello di operazione Usa hello `base` criteri back-end di elemento tooinherit hello dall'ambito di livello padre API hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="779c6-177">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-177">Example</span></span>  
 <span data-ttu-id="779c6-178">Questo criterio a livello di operazione in modo esplicito inoltra tutte le richieste toohello back-end del servizio con un timeout di 120 e non eredita padre hello criteri livello back-end dell'API.</span><span class="sxs-lookup"><span data-stu-id="779c6-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="779c6-179">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-179">Example</span></span>  
 <span data-ttu-id="779c6-180">Questo criterio a livello di operazione non inoltra le richieste di servizio back-end toohello.</span><span class="sxs-lookup"><span data-stu-id="779c6-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-181">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-181">Elements</span></span>  
  
|<span data-ttu-id="779c6-182">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-182">Element</span></span>|<span data-ttu-id="779c6-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-183">Description</span></span>|<span data-ttu-id="779c6-184">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="779c6-185">forward-request</span></span>|<span data-ttu-id="779c6-186">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-186">Root element.</span></span>|<span data-ttu-id="779c6-187">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-188">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-188">Attributes</span></span>  
  
|<span data-ttu-id="779c6-189">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-189">Attribute</span></span>|<span data-ttu-id="779c6-190">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-190">Description</span></span>|<span data-ttu-id="779c6-191">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-191">Required</span></span>|<span data-ttu-id="779c6-192">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="779c6-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="779c6-193">timeout="integer"</span></span>|<span data-ttu-id="779c6-194">intervallo di timeout Hello in secondi prima del servizio back-end di hello chiamata toohello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="779c6-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="779c6-195">No</span><span class="sxs-lookup"><span data-stu-id="779c6-195">No</span></span>|<span data-ttu-id="779c6-196">No timeout</span><span class="sxs-lookup"><span data-stu-id="779c6-196">No timeout</span></span>|  
|<span data-ttu-id="779c6-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="779c6-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="779c6-198">Specifica se i reindirizzamenti dal servizio back-end hello sono seguiti dal gateway hello o restituiti toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="779c6-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="779c6-199">No</span><span class="sxs-lookup"><span data-stu-id="779c6-199">No</span></span>|<span data-ttu-id="779c6-200">false</span><span class="sxs-lookup"><span data-stu-id="779c6-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-201">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-201">Usage</span></span>  
 <span data-ttu-id="779c6-202">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-203">**Sezioni del criterio:** back-end</span><span class="sxs-lookup"><span data-stu-id="779c6-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="779c6-204">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="779c6-205"><a name="LimitConcurrency"></a>Limita concorrenza</span><span class="sxs-lookup"><span data-stu-id="779c6-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="779c6-206">Hello `limit-concurrency` criteri impedisce l'esecuzione di più di hello numero specificato di richieste in un determinato momento criteri tra parentesi.</span><span class="sxs-lookup"><span data-stu-id="779c6-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="779c6-207">In caso di superamento limite hello, le nuove richieste vengono aggiunti tooa coda, fino a raggiungere hello lunghezza massima della coda.</span><span class="sxs-lookup"><span data-stu-id="779c6-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="779c6-208">Al momento di esaurimento della coda, le nuove richieste avranno immediatamente esito negativo.</span><span class="sxs-lookup"><span data-stu-id="779c6-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="779c6-209"><a name="LimitConcurrencyStatement"></a>Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="779c6-210">esempi</span><span class="sxs-lookup"><span data-stu-id="779c6-210">Examples</span></span>  
  
####  <span data-ttu-id="779c6-211"><a name="ChooseExample"></a>Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="779c6-212">Hello esempio seguente viene illustrato come toolimit numero di richieste inoltrate back-end tooa in base al valore di hello di una variabile di contesto.</span><span class="sxs-lookup"><span data-stu-id="779c6-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="779c6-213">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-213">Elements</span></span>  
  
|<span data-ttu-id="779c6-214">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-214">Element</span></span>|<span data-ttu-id="779c6-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-215">Description</span></span>|<span data-ttu-id="779c6-216">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="779c6-217">limita concorrenza</span><span class="sxs-lookup"><span data-stu-id="779c6-217">limit-concurrency</span></span>|<span data-ttu-id="779c6-218">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-218">Root element.</span></span>|<span data-ttu-id="779c6-219">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-220">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-220">Attributes</span></span>  
  
|<span data-ttu-id="779c6-221">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-221">Attribute</span></span>|<span data-ttu-id="779c6-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-222">Description</span></span>|<span data-ttu-id="779c6-223">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-223">Required</span></span>|<span data-ttu-id="779c6-224">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="779c6-225">key</span><span class="sxs-lookup"><span data-stu-id="779c6-225">key</span></span>|<span data-ttu-id="779c6-226">Stringa.</span><span class="sxs-lookup"><span data-stu-id="779c6-226">A string.</span></span> <span data-ttu-id="779c6-227">Espressione consentita.</span><span class="sxs-lookup"><span data-stu-id="779c6-227">Expression allowed.</span></span> <span data-ttu-id="779c6-228">Specifica l'ambito di concorrenza hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="779c6-229">Può essere condivisa da più criteri.</span><span class="sxs-lookup"><span data-stu-id="779c6-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="779c6-230">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-230">Yes</span></span>|<span data-ttu-id="779c6-231">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-231">N/A</span></span>|  
|<span data-ttu-id="779c6-232">numero max</span><span class="sxs-lookup"><span data-stu-id="779c6-232">max-count</span></span>|<span data-ttu-id="779c6-233">Un intero.</span><span class="sxs-lookup"><span data-stu-id="779c6-233">An integer.</span></span> <span data-ttu-id="779c6-234">Specifica un numero massimo di richieste non sono consentiti criteri hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="779c6-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="779c6-235">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-235">Yes</span></span>|<span data-ttu-id="779c6-236">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-236">N/A</span></span>|  
|<span data-ttu-id="779c6-237">timeout</span><span class="sxs-lookup"><span data-stu-id="779c6-237">timeout</span></span>|<span data-ttu-id="779c6-238">Un intero.</span><span class="sxs-lookup"><span data-stu-id="779c6-238">An integer.</span></span> <span data-ttu-id="779c6-239">Espressione consentita.</span><span class="sxs-lookup"><span data-stu-id="779c6-239">Expression allowed.</span></span> <span data-ttu-id="779c6-240">Specifica il numero di hello di secondi durante una richiesta deve attendere tooenter un ambito prima che si verifichi "403 eccessivo numero di richieste"</span><span class="sxs-lookup"><span data-stu-id="779c6-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="779c6-241">No</span><span class="sxs-lookup"><span data-stu-id="779c6-241">No</span></span>|<span data-ttu-id="779c6-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="779c6-242">Infinity</span></span>|  
|<span data-ttu-id="779c6-243">lunghezza massima della coda</span><span class="sxs-lookup"><span data-stu-id="779c6-243">max-queue-length</span></span>|<span data-ttu-id="779c6-244">Un intero.</span><span class="sxs-lookup"><span data-stu-id="779c6-244">An integer.</span></span> <span data-ttu-id="779c6-245">Espressione consentita.</span><span class="sxs-lookup"><span data-stu-id="779c6-245">Expression allowed.</span></span> <span data-ttu-id="779c6-246">Specifica una lunghezza massima della coda hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="779c6-247">Le richieste in ingresso tentativo tooenter questo criterio verrà interrotta con "403 eccessivo numero di richieste" immediatamente quando è esaurita coda hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="779c6-248">No</span><span class="sxs-lookup"><span data-stu-id="779c6-248">No</span></span>|<span data-ttu-id="779c6-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="779c6-249">Infinity</span></span>|  
  
###  <span data-ttu-id="779c6-250"><a name="ChooseUsage"></a>Uso</span><span class="sxs-lookup"><span data-stu-id="779c6-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="779c6-251">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-252">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-253">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="779c6-254"><a name="log-to-eventhub"></a>Log tooEvent Hub</span><span class="sxs-lookup"><span data-stu-id="779c6-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="779c6-255">Hello `log-to-eventhub` criteri invia messaggi hello specificato formato tooan Hub di eventi definiti da un'entità del Logger.</span><span class="sxs-lookup"><span data-stu-id="779c6-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="779c6-256">Come suggerisce il nome, i criteri di hello vengono utilizzati per il salvataggio selezionati informazioni sul contesto di richiesta o risposta per l'analisi online o offline.</span><span class="sxs-lookup"><span data-stu-id="779c6-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="779c6-257">Per una Guida dettagliata sulla configurazione di un hub eventi e la registrazione eventi, vedere [come eventi di gestione API toolog con hub eventi di Azure](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="779c6-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-258">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="779c6-259">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-259">Example</span></span>  
 <span data-ttu-id="779c6-260">Qualsiasi stringa può essere utilizzata come toobe valore hello registrato nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="779c6-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="779c6-261">In questo esempio hello data e ora, nome del servizio di distribuzione, id richiesta, l'indirizzo ip e nome dell'operazione per tutte le chiamate in ingresso sono hub eventi connesso toohello Logger registrato con hello `contoso-logger` id.</span><span class="sxs-lookup"><span data-stu-id="779c6-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-262">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-262">Elements</span></span>  
  
|<span data-ttu-id="779c6-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-263">Element</span></span>|<span data-ttu-id="779c6-264">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-264">Description</span></span>|<span data-ttu-id="779c6-265">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="779c6-266">log-to-eventhub</span></span>|<span data-ttu-id="779c6-267">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-267">Root element.</span></span> <span data-ttu-id="779c6-268">valore Hello di questo elemento è l'hub di eventi tooyour toolog stringa hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="779c6-269">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-270">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-270">Attributes</span></span>  
  
|<span data-ttu-id="779c6-271">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-271">Attribute</span></span>|<span data-ttu-id="779c6-272">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-272">Description</span></span>|<span data-ttu-id="779c6-273">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="779c6-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="779c6-274">logger-id</span></span>|<span data-ttu-id="779c6-275">id Hello di hello Logger registrato con il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="779c6-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="779c6-276">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-276">Yes</span></span>|  
|<span data-ttu-id="779c6-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="779c6-277">partition-id</span></span>|<span data-ttu-id="779c6-278">Specifica l'indice di hello della partizione hello in cui i messaggi vengono inviati.</span><span class="sxs-lookup"><span data-stu-id="779c6-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="779c6-279">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="779c6-279">Optional.</span></span> <span data-ttu-id="779c6-280">Questo attributo non può essere usato se si usa `partition-key`.</span><span class="sxs-lookup"><span data-stu-id="779c6-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="779c6-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="779c6-281">partition-key</span></span>|<span data-ttu-id="779c6-282">Specifica il valore di hello utilizzato per l'assegnazione di partizione quando vengono inviati messaggi.</span><span class="sxs-lookup"><span data-stu-id="779c6-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="779c6-283">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="779c6-283">Optional.</span></span> <span data-ttu-id="779c6-284">Questo attributo non può essere usato se si usa `partition-id`.</span><span class="sxs-lookup"><span data-stu-id="779c6-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-285">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-285">Usage</span></span>  
 <span data-ttu-id="779c6-286">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-287">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-288">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="779c6-289"><a name="mock-response"></a> Restituisci risposta</span><span class="sxs-lookup"><span data-stu-id="779c6-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="779c6-290">Hello `mock-response`, come nome hello implica, viene utilizzato toomock API e operazioni.</span><span class="sxs-lookup"><span data-stu-id="779c6-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="779c6-291">Interrompe l'esecuzione della pipeline normale e restituisce un chiamante toohello risposta simulati.</span><span class="sxs-lookup"><span data-stu-id="779c6-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="779c6-292">criteri di Hello tenta sempre di risposte tooreturn di più alta fedeltà.</span><span class="sxs-lookup"><span data-stu-id="779c6-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="779c6-293">Include esempi di contenuto di risposta ogni volta che è possibile.</span><span class="sxs-lookup"><span data-stu-id="779c6-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="779c6-294">Nelle situazioni in cui vengono forniti schemi ma non esempi, genera risposte di esempio dagli schemi.</span><span class="sxs-lookup"><span data-stu-id="779c6-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="779c6-295">Se non sono presenti né esempi né schemi, restituisce risposte senza contenuto.</span><span class="sxs-lookup"><span data-stu-id="779c6-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-296">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="779c6-297">esempi</span><span class="sxs-lookup"><span data-stu-id="779c6-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="779c6-298">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-298">Elements</span></span>  
  
|<span data-ttu-id="779c6-299">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-299">Element</span></span>|<span data-ttu-id="779c6-300">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-300">Description</span></span>|<span data-ttu-id="779c6-301">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="779c6-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="779c6-302">mock-response</span></span>|<span data-ttu-id="779c6-303">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-303">Root element.</span></span>|<span data-ttu-id="779c6-304">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-305">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-305">Attributes</span></span>  
  
|<span data-ttu-id="779c6-306">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-306">Attribute</span></span>|<span data-ttu-id="779c6-307">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-307">Description</span></span>|<span data-ttu-id="779c6-308">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-308">Required</span></span>|<span data-ttu-id="779c6-309">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="779c6-310">status-code</span><span class="sxs-lookup"><span data-stu-id="779c6-310">status-code</span></span>|<span data-ttu-id="779c6-311">Specifica il codice di stato di risposta ed è esempio corrispondente utilizzato tooselect o nello schema.</span><span class="sxs-lookup"><span data-stu-id="779c6-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="779c6-312">No</span><span class="sxs-lookup"><span data-stu-id="779c6-312">No</span></span>|<span data-ttu-id="779c6-313">200</span><span class="sxs-lookup"><span data-stu-id="779c6-313">200</span></span>|  
|<span data-ttu-id="779c6-314">content-type</span><span class="sxs-lookup"><span data-stu-id="779c6-314">content-type</span></span>|<span data-ttu-id="779c6-315">Specifica `Content-Type` valore dell'intestazione di risposta e viene utilizzato tooselect esempio corrispondente o nello schema.</span><span class="sxs-lookup"><span data-stu-id="779c6-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="779c6-316">No</span><span class="sxs-lookup"><span data-stu-id="779c6-316">No</span></span>|<span data-ttu-id="779c6-317">None</span><span class="sxs-lookup"><span data-stu-id="779c6-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-318">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-318">Usage</span></span>  
 <span data-ttu-id="779c6-319">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-320">**Sezioni del criterio:** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="779c6-321">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="779c6-322"><a name="Retry"></a> Riprova</span><span class="sxs-lookup"><span data-stu-id="779c6-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="779c6-323">Hello `retry` criteri esegue i relativi criteri figlio una volta e quindi ripete l'esecuzione fino al tentativo di hello `condition` diventa `false` o ripetere `count` è esaurita.</span><span class="sxs-lookup"><span data-stu-id="779c6-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-324">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="779c6-325">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-325">Example</span></span>  
 <span data-ttu-id="779c6-326">In hello forewarding richiesta di esempio seguente viene ripetuta backup tooten volte utilizzando l'algoritmo di tentativi esponenziali.</span><span class="sxs-lookup"><span data-stu-id="779c6-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="779c6-327">Poiché `first-fast-retry` è impostato toofalse, tutti i tentativi sono algoritmo dei tentativi exponsntial toohello soggetto.</span><span class="sxs-lookup"><span data-stu-id="779c6-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-328">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-328">Elements</span></span>  
  
|<span data-ttu-id="779c6-329">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-329">Element</span></span>|<span data-ttu-id="779c6-330">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-330">Description</span></span>|<span data-ttu-id="779c6-331">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-332">retry</span><span class="sxs-lookup"><span data-stu-id="779c6-332">retry</span></span>|<span data-ttu-id="779c6-333">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-333">Root element.</span></span> <span data-ttu-id="779c6-334">Può contenere tutti gli altri criteri come elementi figlio.</span><span class="sxs-lookup"><span data-stu-id="779c6-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="779c6-335">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-336">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-336">Attributes</span></span>  
  
|<span data-ttu-id="779c6-337">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-337">Attribute</span></span>|<span data-ttu-id="779c6-338">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-338">Description</span></span>|<span data-ttu-id="779c6-339">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-339">Required</span></span>|<span data-ttu-id="779c6-340">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="779c6-341">condition</span><span class="sxs-lookup"><span data-stu-id="779c6-341">condition</span></span>|<span data-ttu-id="779c6-342">Valore letterale booleano o [espressione](api-management-policy-expressions.md) che specifica se i tentativi devono essere interrotti (`false`) o devono continuare (`true`).</span><span class="sxs-lookup"><span data-stu-id="779c6-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="779c6-343">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-343">Yes</span></span>|<span data-ttu-id="779c6-344">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-344">N/A</span></span>|  
|<span data-ttu-id="779c6-345">count</span><span class="sxs-lookup"><span data-stu-id="779c6-345">count</span></span>|<span data-ttu-id="779c6-346">Un numero positivo che specifica hello il numero massimo di tentativi tooattempt.</span><span class="sxs-lookup"><span data-stu-id="779c6-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="779c6-347">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-347">Yes</span></span>|<span data-ttu-id="779c6-348">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-348">N/A</span></span>|  
|<span data-ttu-id="779c6-349">interval</span><span class="sxs-lookup"><span data-stu-id="779c6-349">interval</span></span>|<span data-ttu-id="779c6-350">Un numero positivo, in secondi, specificando l'intervallo di attesa hello tra tentativi hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="779c6-351">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-351">Yes</span></span>|<span data-ttu-id="779c6-352">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-352">N/A</span></span>|  
|<span data-ttu-id="779c6-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="779c6-353">max-interval</span></span>|<span data-ttu-id="779c6-354">Un numero positivo, in secondi, specificando l'intervallo di attesa massimo hello tra tentativi hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="779c6-355">È tooimplement utilizzato un algoritmo di tentativi esponenziali.</span><span class="sxs-lookup"><span data-stu-id="779c6-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="779c6-356">No</span><span class="sxs-lookup"><span data-stu-id="779c6-356">No</span></span>|<span data-ttu-id="779c6-357">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-357">N/A</span></span>|  
|<span data-ttu-id="779c6-358">delta</span><span class="sxs-lookup"><span data-stu-id="779c6-358">delta</span></span>|<span data-ttu-id="779c6-359">Un numero positivo, in secondi, specificare l'incremento di intervallo di attesa hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="779c6-360">È utilizzato tooimplement hello tentativi lineare ed esponenziale algoritmi.</span><span class="sxs-lookup"><span data-stu-id="779c6-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="779c6-361">No</span><span class="sxs-lookup"><span data-stu-id="779c6-361">No</span></span>|<span data-ttu-id="779c6-362">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-362">N/A</span></span>|  
|<span data-ttu-id="779c6-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="779c6-363">first-fast-retry</span></span>|<span data-ttu-id="779c6-364">Se impostato troppo `true` , primo tentativo di hello viene eseguita immediatamente.</span><span class="sxs-lookup"><span data-stu-id="779c6-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="779c6-365">No</span><span class="sxs-lookup"><span data-stu-id="779c6-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="779c6-366">Quando solo hello `interval` è specificato, **fissa** intervallo tentativi vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="779c6-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="779c6-367">Quando solo hello `interval` e `delta` vengono specificati un **lineare** viene utilizzato l'algoritmo di tentativi di intervallo, in cui il tempo di attesa tra tentativi viene calcolato hello in base formula - seguente `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="779c6-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="779c6-368">Quando hello `interval`, `max-interval` e `delta` vengono specificati, **esponenziale** viene applicato l'algoritmo dei tentativi di intervallo, in cui crescono in modo esponenziale il tempo di attesa hello tra i tentativi di hello dal valore hello `interval`valore toohello `max-interval` in base a seguito di toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="779c6-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="779c6-369">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-369">Usage</span></span>  
 <span data-ttu-id="779c6-370">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="779c6-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="779c6-371">Si noti che le restrizioni sull'uso dei criteri figlio verranno ereditate da questo criterio.</span><span class="sxs-lookup"><span data-stu-id="779c6-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="779c6-372">**Sezioni del criterio:**in ingresso, in uscita, back-end, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-373">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="779c6-374"><a name="ReturnResponse"></a>Restituisci risposta</span><span class="sxs-lookup"><span data-stu-id="779c6-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="779c6-375">Hello `return-response` criteri interrompe l'esecuzione della pipeline e restituisce un'istanza predefinita o chiamante toohello risposta personalizzata.</span><span class="sxs-lookup"><span data-stu-id="779c6-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="779c6-376">La risposta predefinita è `200 OK`, senza corpo.</span><span class="sxs-lookup"><span data-stu-id="779c6-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="779c6-377">La risposta personalizzata può essere specificata tramite una variabile di contesto o le istruzioni del criterio.</span><span class="sxs-lookup"><span data-stu-id="779c6-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="779c6-378">Se vengono specificati entrambi, risposta hello contenuto all'interno di variabile di contesto hello viene modificato mediante le istruzioni dei criteri di hello prima della restituzione toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="779c6-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-379">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="779c6-380">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="779c6-381">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-381">Elements</span></span>  
  
|<span data-ttu-id="779c6-382">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-382">Element</span></span>|<span data-ttu-id="779c6-383">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-383">Description</span></span>|<span data-ttu-id="779c6-384">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-385">return-response</span><span class="sxs-lookup"><span data-stu-id="779c6-385">return-response</span></span>|<span data-ttu-id="779c6-386">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-386">Root element.</span></span>|<span data-ttu-id="779c6-387">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-387">Yes</span></span>|  
|<span data-ttu-id="779c6-388">set-header</span><span class="sxs-lookup"><span data-stu-id="779c6-388">set-header</span></span>|<span data-ttu-id="779c6-389">Istruzione del criterio.[set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="779c6-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="779c6-390">No</span><span class="sxs-lookup"><span data-stu-id="779c6-390">No</span></span>|  
|<span data-ttu-id="779c6-391">set-body</span><span class="sxs-lookup"><span data-stu-id="779c6-391">set-body</span></span>|<span data-ttu-id="779c6-392">Istruzione del criterio.[set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="779c6-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="779c6-393">No</span><span class="sxs-lookup"><span data-stu-id="779c6-393">No</span></span>|  
|<span data-ttu-id="779c6-394">set-status</span><span class="sxs-lookup"><span data-stu-id="779c6-394">set-status</span></span>|<span data-ttu-id="779c6-395">Istruzione del criterio [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="779c6-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="779c6-396">No</span><span class="sxs-lookup"><span data-stu-id="779c6-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-397">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-397">Attributes</span></span>  
  
|<span data-ttu-id="779c6-398">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-398">Attribute</span></span>|<span data-ttu-id="779c6-399">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-399">Description</span></span>|<span data-ttu-id="779c6-400">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="779c6-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="779c6-401">response-variable-name</span></span>|<span data-ttu-id="779c6-402">Hello nome di variabile di contesto hello a cui fa riferimento, ad esempio, un upstream [richiesta di invio](api-management-advanced-policies.md#SendRequest) criteri e che contiene un `Response` oggetto</span><span class="sxs-lookup"><span data-stu-id="779c6-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="779c6-403">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="779c6-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-404">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-404">Usage</span></span>  
 <span data-ttu-id="779c6-405">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-406">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-407">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="779c6-408"><a name="SendOneWayRequest"></a>Invia richiesta unidirezionale</span><span class="sxs-lookup"><span data-stu-id="779c6-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="779c6-409">Hello `send-one-way-request` criteri invia la richiesta di hello fornito toohello URL specificato senza attendere una risposta.</span><span class="sxs-lookup"><span data-stu-id="779c6-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-410">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="779c6-411">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-411">Example</span></span>  
 <span data-ttu-id="779c6-412">Questo criterio di esempio viene illustrato un esempio dell'utilizzo di hello `send-one-way-request` toosend criteri una messaggio tooa Slack chat room se hello codice di risposta HTTP è maggiore o uguale too500.</span><span class="sxs-lookup"><span data-stu-id="779c6-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="779c6-413">Per ulteriori informazioni su questo esempio, vedere [tramite servizi esterni dal servizio Gestione API di Azure hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="779c6-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-414">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-414">Elements</span></span>  
  
|<span data-ttu-id="779c6-415">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-415">Element</span></span>|<span data-ttu-id="779c6-416">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-416">Description</span></span>|<span data-ttu-id="779c6-417">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="779c6-418">send-one-way-request</span></span>|<span data-ttu-id="779c6-419">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-419">Root element.</span></span>|<span data-ttu-id="779c6-420">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-420">Yes</span></span>|  
|<span data-ttu-id="779c6-421">URL</span><span class="sxs-lookup"><span data-stu-id="779c6-421">url</span></span>|<span data-ttu-id="779c6-422">Hello l'URL della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-422">hello URL of hello request.</span></span>|<span data-ttu-id="779c6-423">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="779c6-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="779c6-424">statico</span><span class="sxs-lookup"><span data-stu-id="779c6-424">method</span></span>|<span data-ttu-id="779c6-425">metodo HTTP per la richiesta di hello Hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="779c6-426">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="779c6-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="779c6-427">intestazione</span><span class="sxs-lookup"><span data-stu-id="779c6-427">header</span></span>|<span data-ttu-id="779c6-428">Intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="779c6-428">Request header.</span></span> <span data-ttu-id="779c6-429">Usare più elementi di intestazione per più intestazioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="779c6-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="779c6-430">No</span><span class="sxs-lookup"><span data-stu-id="779c6-430">No</span></span>|  
|<span data-ttu-id="779c6-431">body</span><span class="sxs-lookup"><span data-stu-id="779c6-431">body</span></span>|<span data-ttu-id="779c6-432">corpo della richiesta Hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-432">hello request body.</span></span>|<span data-ttu-id="779c6-433">No</span><span class="sxs-lookup"><span data-stu-id="779c6-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-434">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-434">Attributes</span></span>  
  
|<span data-ttu-id="779c6-435">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-435">Attribute</span></span>|<span data-ttu-id="779c6-436">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-436">Description</span></span>|<span data-ttu-id="779c6-437">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-437">Required</span></span>|<span data-ttu-id="779c6-438">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="779c6-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="779c6-439">mode="string"</span></span>|<span data-ttu-id="779c6-440">Determina se si tratta di una nuova richiesta o una copia della richiesta corrente hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="779c6-441">In modalità in uscita, modalità = copia non viene inizializzato il corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="779c6-442">No</span><span class="sxs-lookup"><span data-stu-id="779c6-442">No</span></span>|<span data-ttu-id="779c6-443">Nuovo</span><span class="sxs-lookup"><span data-stu-id="779c6-443">New</span></span>|  
|<span data-ttu-id="779c6-444">name</span><span class="sxs-lookup"><span data-stu-id="779c6-444">name</span></span>|<span data-ttu-id="779c6-445">Specifica il nome di hello di hello intestazione toobe set.</span><span class="sxs-lookup"><span data-stu-id="779c6-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="779c6-446">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-446">Yes</span></span>|<span data-ttu-id="779c6-447">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-447">N/A</span></span>|  
|<span data-ttu-id="779c6-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="779c6-448">exists-action</span></span>|<span data-ttu-id="779c6-449">Specifica quali tootake azione quando l'intestazione hello è già specificato.</span><span class="sxs-lookup"><span data-stu-id="779c6-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="779c6-450">Questo attributo deve avere uno dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="779c6-451">-override - sostituisce hello valore dell'intestazione esistente hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="779c6-452">-skip: non sostituisce il valore dell'intestazione esistente di hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="779c6-453">-aggiungere - aggiunge hello valore toohello valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="779c6-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="779c6-454">-delete - rimuove l'intestazione di hello dalla richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="779c6-455">Quando impostato troppo`override` l'integrazione di più voci con hello stesso nome risultati nell'intestazione di hello viene impostato in base tooall le voci (elencate più volte); solo i valori elencati verranno impostati nel risultato hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="779c6-456">No</span><span class="sxs-lookup"><span data-stu-id="779c6-456">No</span></span>|<span data-ttu-id="779c6-457">override</span><span class="sxs-lookup"><span data-stu-id="779c6-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-458">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-458">Usage</span></span>  
 <span data-ttu-id="779c6-459">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-460">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-461">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="779c6-462"><a name="SendRequest"></a> Invio richiesta</span><span class="sxs-lookup"><span data-stu-id="779c6-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="779c6-463">Hello `send-request` criteri Invia richiesta hello fornito toohello specificato l'URL, in attesa non più di hello imposta il valore di timeout.</span><span class="sxs-lookup"><span data-stu-id="779c6-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-464">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="779c6-465">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-465">Example</span></span>  
 <span data-ttu-id="779c6-466">Questo esempio viene illustrato un modo tooverify un token di riferimento con un server di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="779c6-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="779c6-467">Per ulteriori informazioni su questo esempio, vedere [tramite servizi esterni dal servizio Gestione API di Azure hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="779c6-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-468">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-468">Elements</span></span>  
  
|<span data-ttu-id="779c6-469">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-469">Element</span></span>|<span data-ttu-id="779c6-470">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-470">Description</span></span>|<span data-ttu-id="779c6-471">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-472">send-request</span><span class="sxs-lookup"><span data-stu-id="779c6-472">send-request</span></span>|<span data-ttu-id="779c6-473">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-473">Root element.</span></span>|<span data-ttu-id="779c6-474">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-474">Yes</span></span>|  
|<span data-ttu-id="779c6-475">URL</span><span class="sxs-lookup"><span data-stu-id="779c6-475">url</span></span>|<span data-ttu-id="779c6-476">Hello l'URL della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-476">hello URL of hello request.</span></span>|<span data-ttu-id="779c6-477">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="779c6-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="779c6-478">statico</span><span class="sxs-lookup"><span data-stu-id="779c6-478">method</span></span>|<span data-ttu-id="779c6-479">metodo HTTP per la richiesta di hello Hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="779c6-480">No if mode=copy; otherwise yes.</span><span class="sxs-lookup"><span data-stu-id="779c6-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="779c6-481">intestazione</span><span class="sxs-lookup"><span data-stu-id="779c6-481">header</span></span>|<span data-ttu-id="779c6-482">Intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="779c6-482">Request header.</span></span> <span data-ttu-id="779c6-483">Usare più elementi di intestazione per più intestazioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="779c6-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="779c6-484">No</span><span class="sxs-lookup"><span data-stu-id="779c6-484">No</span></span>|  
|<span data-ttu-id="779c6-485">body</span><span class="sxs-lookup"><span data-stu-id="779c6-485">body</span></span>|<span data-ttu-id="779c6-486">corpo della richiesta Hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-486">hello request body.</span></span>|<span data-ttu-id="779c6-487">No</span><span class="sxs-lookup"><span data-stu-id="779c6-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-488">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-488">Attributes</span></span>  
  
|<span data-ttu-id="779c6-489">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-489">Attribute</span></span>|<span data-ttu-id="779c6-490">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-490">Description</span></span>|<span data-ttu-id="779c6-491">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-491">Required</span></span>|<span data-ttu-id="779c6-492">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="779c6-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="779c6-493">mode="string"</span></span>|<span data-ttu-id="779c6-494">Determina se si tratta di una nuova richiesta o una copia della richiesta corrente hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="779c6-495">In modalità in uscita, modalità = copia non viene inizializzato il corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="779c6-496">No</span><span class="sxs-lookup"><span data-stu-id="779c6-496">No</span></span>|<span data-ttu-id="779c6-497">Nuovo</span><span class="sxs-lookup"><span data-stu-id="779c6-497">New</span></span>|  
|<span data-ttu-id="779c6-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="779c6-498">response-variable-name="string"</span></span>|<span data-ttu-id="779c6-499">Se non è presente, viene usato `context.Response`.</span><span class="sxs-lookup"><span data-stu-id="779c6-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="779c6-500">No</span><span class="sxs-lookup"><span data-stu-id="779c6-500">No</span></span>|<span data-ttu-id="779c6-501">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-501">N/A</span></span>|  
|<span data-ttu-id="779c6-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="779c6-502">timeout="integer"</span></span>|<span data-ttu-id="779c6-503">intervallo di timeout Hello in secondi, prima chiamata hello toohello URL non riesce.</span><span class="sxs-lookup"><span data-stu-id="779c6-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="779c6-504">No</span><span class="sxs-lookup"><span data-stu-id="779c6-504">No</span></span>|<span data-ttu-id="779c6-505">60</span><span class="sxs-lookup"><span data-stu-id="779c6-505">60</span></span>|  
|<span data-ttu-id="779c6-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="779c6-506">ignore-error</span></span>|<span data-ttu-id="779c6-507">Se true e hello richiesta comporta un errore:</span><span class="sxs-lookup"><span data-stu-id="779c6-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="779c6-508">- Se è stato specificato response-variable-name, questo conterrà un valore null.</span><span class="sxs-lookup"><span data-stu-id="779c6-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="779c6-509">- Se response-variable-name non è stato specificato, context.Request non verrà aggiornato.</span><span class="sxs-lookup"><span data-stu-id="779c6-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="779c6-510">No</span><span class="sxs-lookup"><span data-stu-id="779c6-510">No</span></span>|<span data-ttu-id="779c6-511">false</span><span class="sxs-lookup"><span data-stu-id="779c6-511">false</span></span>|  
|<span data-ttu-id="779c6-512">name</span><span class="sxs-lookup"><span data-stu-id="779c6-512">name</span></span>|<span data-ttu-id="779c6-513">Specifica il nome di hello di hello intestazione toobe set.</span><span class="sxs-lookup"><span data-stu-id="779c6-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="779c6-514">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-514">Yes</span></span>|<span data-ttu-id="779c6-515">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-515">N/A</span></span>|  
|<span data-ttu-id="779c6-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="779c6-516">exists-action</span></span>|<span data-ttu-id="779c6-517">Specifica quali tootake azione quando l'intestazione hello è già specificato.</span><span class="sxs-lookup"><span data-stu-id="779c6-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="779c6-518">Questo attributo deve avere uno dei seguenti valori hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="779c6-519">-override - sostituisce hello valore dell'intestazione esistente hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="779c6-520">-skip: non sostituisce il valore dell'intestazione esistente di hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="779c6-521">-aggiungere - aggiunge hello valore toohello valore dell'intestazione esistente.</span><span class="sxs-lookup"><span data-stu-id="779c6-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="779c6-522">-delete - rimuove l'intestazione di hello dalla richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="779c6-523">Quando impostato troppo`override` l'integrazione di più voci con hello stesso nome risultati nell'intestazione di hello viene impostato in base tooall le voci (elencate più volte); solo i valori elencati verranno impostati nel risultato hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="779c6-524">No</span><span class="sxs-lookup"><span data-stu-id="779c6-524">No</span></span>|<span data-ttu-id="779c6-525">override</span><span class="sxs-lookup"><span data-stu-id="779c6-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-526">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-526">Usage</span></span>  
 <span data-ttu-id="779c6-527">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-528">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-529">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="779c6-530"><a name="SetHttpProxy"></a>Impostare il proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="779c6-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="779c6-531">Hello `proxy` criteri consentono di tooroute richieste inoltrate toobackends tramite un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="779c6-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="779c6-532">Solo HTTP (non HTTPS) è supportata tra il gateway hello e proxy hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="779c6-533">Solo autenticazione Basic e NTLM.</span><span class="sxs-lookup"><span data-stu-id="779c6-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-534">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="779c6-535">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-535">Example</span></span>  
<span data-ttu-id="779c6-536">Si noti hello utilizzo di [proprietà](api-management-howto-properties.md) come valori di tooavoid hello nome utente e password, l'archiviazione di informazioni riservate nel documento di criteri hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="779c6-537">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-537">Elements</span></span>  
  
|<span data-ttu-id="779c6-538">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-538">Element</span></span>|<span data-ttu-id="779c6-539">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-539">Description</span></span>|<span data-ttu-id="779c6-540">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-541">proxy</span><span class="sxs-lookup"><span data-stu-id="779c6-541">proxy</span></span>|<span data-ttu-id="779c6-542">Elemento radice</span><span class="sxs-lookup"><span data-stu-id="779c6-542">Root element</span></span>|<span data-ttu-id="779c6-543">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="779c6-544">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-544">Attributes</span></span>  
  
|<span data-ttu-id="779c6-545">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-545">Attribute</span></span>|<span data-ttu-id="779c6-546">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-546">Description</span></span>|<span data-ttu-id="779c6-547">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-547">Required</span></span>|<span data-ttu-id="779c6-548">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="779c6-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="779c6-549">url="string"</span></span>|<span data-ttu-id="779c6-550">URL del proxy in forma di hello di HTTP.</span><span class="sxs-lookup"><span data-stu-id="779c6-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="779c6-551">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-551">Yes</span></span>|<span data-ttu-id="779c6-552">N/D </span><span class="sxs-lookup"><span data-stu-id="779c6-552">N/A</span></span>|  
|<span data-ttu-id="779c6-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="779c6-553">username="string"</span></span>|<span data-ttu-id="779c6-554">Toobe nome utente utilizzato per l'autenticazione con il proxy di hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="779c6-555">No</span><span class="sxs-lookup"><span data-stu-id="779c6-555">No</span></span>|<span data-ttu-id="779c6-556">N/D </span><span class="sxs-lookup"><span data-stu-id="779c6-556">N/A</span></span>|  
|<span data-ttu-id="779c6-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="779c6-557">password="string"</span></span>|<span data-ttu-id="779c6-558">Toobe password utilizzata per l'autenticazione con il proxy di hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="779c6-559">No</span><span class="sxs-lookup"><span data-stu-id="779c6-559">No</span></span>|<span data-ttu-id="779c6-560">N/D </span><span class="sxs-lookup"><span data-stu-id="779c6-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="779c6-561">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-561">Usage</span></span>  
 <span data-ttu-id="779c6-562">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-563">**Sezioni del criterio:** inbound</span><span class="sxs-lookup"><span data-stu-id="779c6-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="779c6-564">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="779c6-565"><a name="SetRequestMethod"></a> Impostare il metodo di richiesta</span><span class="sxs-lookup"><span data-stu-id="779c6-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="779c6-566">Hello `set-method` criteri consentono di metodo di richiesta HTTP hello toochange per una richiesta.</span><span class="sxs-lookup"><span data-stu-id="779c6-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-567">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="779c6-568">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-568">Example</span></span>  
 <span data-ttu-id="779c6-569">Questo esempio di criterio che utilizza hello `set-method` criteri Mostra un esempio di invio di una messaggio tooa Slack chat room se hello codice di risposta HTTP è maggiore o uguale too500.</span><span class="sxs-lookup"><span data-stu-id="779c6-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="779c6-570">Per ulteriori informazioni su questo esempio, vedere [tramite servizi esterni dal servizio Gestione API di Azure hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="779c6-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-571">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-571">Elements</span></span>  
  
|<span data-ttu-id="779c6-572">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-572">Element</span></span>|<span data-ttu-id="779c6-573">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-573">Description</span></span>|<span data-ttu-id="779c6-574">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-575">set-method</span><span class="sxs-lookup"><span data-stu-id="779c6-575">set-method</span></span>|<span data-ttu-id="779c6-576">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-576">Root element.</span></span> <span data-ttu-id="779c6-577">valore Hello elemento hello specifica il metodo HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="779c6-578">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-579">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-579">Usage</span></span>  
 <span data-ttu-id="779c6-580">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-581">**Sezioni del criterio:** inbound, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="779c6-582">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="779c6-583"><a name="SetStatus"></a> Impostare il codice di stato</span><span class="sxs-lookup"><span data-stu-id="779c6-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="779c6-584">Hello `set-status` criteri set hello HTTP stato codice toohello valore specificato.</span><span class="sxs-lookup"><span data-stu-id="779c6-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-585">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="779c6-586">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-586">Example</span></span>  
 <span data-ttu-id="779c6-587">Questo esempio viene illustrato come tooreturn una risposta 401, se il token di autorizzazione hello non è valido.</span><span class="sxs-lookup"><span data-stu-id="779c6-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="779c6-588">Per ulteriori informazioni, vedere [tramite servizi esterni da hello servizio Gestione API di Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="779c6-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-589">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-589">Elements</span></span>  
  
|<span data-ttu-id="779c6-590">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-590">Element</span></span>|<span data-ttu-id="779c6-591">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-591">Description</span></span>|<span data-ttu-id="779c6-592">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-593">set-status</span><span class="sxs-lookup"><span data-stu-id="779c6-593">set-status</span></span>|<span data-ttu-id="779c6-594">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-594">Root element.</span></span>|<span data-ttu-id="779c6-595">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-596">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-596">Attributes</span></span>  
  
|<span data-ttu-id="779c6-597">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-597">Attribute</span></span>|<span data-ttu-id="779c6-598">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-598">Description</span></span>|<span data-ttu-id="779c6-599">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-599">Required</span></span>|<span data-ttu-id="779c6-600">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="779c6-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="779c6-601">code="integer"</span></span>|<span data-ttu-id="779c6-602">tooreturn codice di stato HTTP Hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="779c6-603">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-603">Yes</span></span>|<span data-ttu-id="779c6-604">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-604">N/A</span></span>|  
|<span data-ttu-id="779c6-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="779c6-605">reason="string"</span></span>|<span data-ttu-id="779c6-606">Descrizione del motivo di hello per la restituzione di codice di stato hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="779c6-607">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-607">Yes</span></span>|<span data-ttu-id="779c6-608">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-609">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-609">Usage</span></span>  
 <span data-ttu-id="779c6-610">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-611">**Sezioni del criterio:** outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-612">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="779c6-613"><a name="set-variable"></a>Impostare una variabile</span><span class="sxs-lookup"><span data-stu-id="779c6-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="779c6-614">Hello `set-variable` criteri dichiara un [contesto](api-management-policy-expressions.md#ContextVariables) variabile e assegna un valore specificato tramite un [espressione](api-management-policy-expressions.md) o un valore letterale stringa.</span><span class="sxs-lookup"><span data-stu-id="779c6-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="779c6-615">Se l'espressione di hello contiene un valore letterale verrà convertito tooa stringa e hello il tipo di valore hello sarà `System.String`.</span><span class="sxs-lookup"><span data-stu-id="779c6-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="779c6-616"><a name="set-variablePolicyStatement"></a>Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="779c6-617"><a name="set-variableExample"></a>Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="779c6-618">Hello esempio seguente viene illustrato un criterio di variabile set in hello in ingresso di sezione.</span><span class="sxs-lookup"><span data-stu-id="779c6-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="779c6-619">Questo criterio variabile set crea un `isMobile` booleano [contesto](api-management-policy-expressions.md#ContextVariables) variabile impostata tootrue se hello `User-Agent` richiesta intestazione contiene testo hello `iPad` o `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="779c6-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="779c6-620">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-620">Elements</span></span>  
  
|<span data-ttu-id="779c6-621">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-621">Element</span></span>|<span data-ttu-id="779c6-622">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-622">Description</span></span>|<span data-ttu-id="779c6-623">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="779c6-624">set-variable</span></span>|<span data-ttu-id="779c6-625">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-625">Root element.</span></span>|<span data-ttu-id="779c6-626">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-627">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-627">Attributes</span></span>  
  
|<span data-ttu-id="779c6-628">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-628">Attribute</span></span>|<span data-ttu-id="779c6-629">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-629">Description</span></span>|<span data-ttu-id="779c6-630">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="779c6-631">name</span><span class="sxs-lookup"><span data-stu-id="779c6-631">name</span></span>|<span data-ttu-id="779c6-632">nome Hello della variabile di hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-632">hello name of hello variable.</span></span>|<span data-ttu-id="779c6-633">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-633">Yes</span></span>|  
|<span data-ttu-id="779c6-634">value</span><span class="sxs-lookup"><span data-stu-id="779c6-634">value</span></span>|<span data-ttu-id="779c6-635">valore di Hello della variabile hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-635">hello value of hello variable.</span></span> <span data-ttu-id="779c6-636">Può essere un'espressione o un valore letterale.</span><span class="sxs-lookup"><span data-stu-id="779c6-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="779c6-637">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-638">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-638">Usage</span></span>  
 <span data-ttu-id="779c6-639">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-640">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-641">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="779c6-642"><a name="set-variableAllowedTypes"></a>Tipi consentiti</span><span class="sxs-lookup"><span data-stu-id="779c6-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="779c6-643">Le espressioni utilizzate in hello `set-variable` criteri devono restituire uno dei seguenti tipi di base hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="779c6-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="779c6-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="779c6-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="779c6-645">System.SByte</span></span>  
  
-   <span data-ttu-id="779c6-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="779c6-646">System.Byte</span></span>  
  
-   <span data-ttu-id="779c6-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="779c6-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="779c6-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="779c6-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="779c6-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="779c6-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="779c6-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="779c6-650">System.Int16</span></span>  
  
-   <span data-ttu-id="779c6-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="779c6-651">System.Int32</span></span>  
  
-   <span data-ttu-id="779c6-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="779c6-652">System.Int64</span></span>  
  
-   <span data-ttu-id="779c6-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="779c6-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="779c6-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="779c6-654">System.Single</span></span>  
  
-   <span data-ttu-id="779c6-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="779c6-655">System.Double</span></span>  
  
-   <span data-ttu-id="779c6-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="779c6-656">System.Guid</span></span>  
  
-   <span data-ttu-id="779c6-657">System.String</span><span class="sxs-lookup"><span data-stu-id="779c6-657">System.String</span></span>  
  
-   <span data-ttu-id="779c6-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="779c6-658">System.Char</span></span>  
  
-   <span data-ttu-id="779c6-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="779c6-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="779c6-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="779c6-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="779c6-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="779c6-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="779c6-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="779c6-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="779c6-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="779c6-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="779c6-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="779c6-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="779c6-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="779c6-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="779c6-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="779c6-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="779c6-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="779c6-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="779c6-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="779c6-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="779c6-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="779c6-669">System.Single?</span></span>  
  
-   <span data-ttu-id="779c6-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="779c6-670">System.Double?</span></span>  
  
-   <span data-ttu-id="779c6-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="779c6-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="779c6-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="779c6-672">System.String?</span></span>  
  
-   <span data-ttu-id="779c6-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="779c6-673">System.Char?</span></span>  
  
-   <span data-ttu-id="779c6-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="779c6-674">System.DateTime?</span></span>  

##  <span data-ttu-id="779c6-675"><a name="Trace"></a> Traccia</span><span class="sxs-lookup"><span data-stu-id="779c6-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="779c6-676">Hello `trace` criteri aggiunge una stringa in hello [API controllo](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span><span class="sxs-lookup"><span data-stu-id="779c6-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="779c6-677">Hello criteri verranno eseguiti solo quando la traccia è attivata, vale a dire `Ocp-Apim-Trace` intestazione della richiesta è presente e impostato troppo`true` e `Ocp-Apim-Subscription-Key` intestazione della richiesta è presente e contiene una chiave valida associata a hello amministratore account.</span><span class="sxs-lookup"><span data-stu-id="779c6-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-678">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="779c6-679">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-679">Elements</span></span>  
  
|<span data-ttu-id="779c6-680">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-680">Element</span></span>|<span data-ttu-id="779c6-681">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-681">Description</span></span>|<span data-ttu-id="779c6-682">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-683">trace</span><span class="sxs-lookup"><span data-stu-id="779c6-683">trace</span></span>|<span data-ttu-id="779c6-684">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-684">Root element.</span></span>|<span data-ttu-id="779c6-685">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-686">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-686">Attributes</span></span>  
  
|<span data-ttu-id="779c6-687">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-687">Attribute</span></span>|<span data-ttu-id="779c6-688">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-688">Description</span></span>|<span data-ttu-id="779c6-689">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-689">Required</span></span>|<span data-ttu-id="779c6-690">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="779c6-691">una sezione source</span><span class="sxs-lookup"><span data-stu-id="779c6-691">source</span></span>|<span data-ttu-id="779c6-692">Visualizzatore di tracce di stringa letterale toohello significativo e specificando origine hello del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="779c6-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="779c6-693">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-693">Yes</span></span>|<span data-ttu-id="779c6-694">N/D</span><span class="sxs-lookup"><span data-stu-id="779c6-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-695">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-695">Usage</span></span>  
 <span data-ttu-id="779c6-696">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="779c6-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="779c6-697">**Sezioni del criterio:** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="779c6-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="779c6-698">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="779c6-699"><a name="Wait"></a> Attesa</span><span class="sxs-lookup"><span data-stu-id="779c6-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="779c6-700">Hello `wait` criteri esegue i criteri figlio diretti in parallelo e attende che tutti o uno dei relativi toocomplete criteri figlio immediati prima che venga completato.</span><span class="sxs-lookup"><span data-stu-id="779c6-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="779c6-701">Hello attesa criteri possono avere come relativi criteri figlio immediati [richiesta di invio](api-management-advanced-policies.md#SendRequest), [ottenere valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey), e [flusso di controllo](api-management-advanced-policies.md#choose) criteri.</span><span class="sxs-lookup"><span data-stu-id="779c6-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="779c6-702">Istruzione del criterio</span><span class="sxs-lookup"><span data-stu-id="779c6-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="779c6-703">Esempio</span><span class="sxs-lookup"><span data-stu-id="779c6-703">Example</span></span>  
 <span data-ttu-id="779c6-704">Nell'esempio seguente hello sono disponibili due `choose` criteri come criteri figlio immediati di hello `wait` criteri.</span><span class="sxs-lookup"><span data-stu-id="779c6-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="779c6-705">Ognuno di questi criteri `choose` viene eseguito in parallelo.</span><span class="sxs-lookup"><span data-stu-id="779c6-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="779c6-706">Ogni `choose` criteri tenta tooretrieve valore memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="779c6-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="779c6-707">Se è presente un mancato riscontro nella cache, un servizio back-end viene chiamato il valore di hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="779c6-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="779c6-708">In questo hello esempio `wait` criteri non verrà completata fino al completamento di tutti i relativi criteri figlio immediati, poiché hello `for` attributo è impostato troppo`all`.</span><span class="sxs-lookup"><span data-stu-id="779c6-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="779c6-709">Nelle variabili di contesto hello in questo esempio (`execute-branch-one`, `value-one`, `execute-branch-two`, e `value-two`) vengono dichiarati di fuori ambito hello di questo criterio di esempio.</span><span class="sxs-lookup"><span data-stu-id="779c6-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="779c6-710">Elementi</span><span class="sxs-lookup"><span data-stu-id="779c6-710">Elements</span></span>  
  
|<span data-ttu-id="779c6-711">Elemento</span><span class="sxs-lookup"><span data-stu-id="779c6-711">Element</span></span>|<span data-ttu-id="779c6-712">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-712">Description</span></span>|<span data-ttu-id="779c6-713">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="779c6-714">wait</span><span class="sxs-lookup"><span data-stu-id="779c6-714">wait</span></span>|<span data-ttu-id="779c6-715">Elemento radice.</span><span class="sxs-lookup"><span data-stu-id="779c6-715">Root element.</span></span> <span data-ttu-id="779c6-716">Può contenere come elementi figlio solo i criteri `send-request`, `cache-lookup-value` e `choose`.</span><span class="sxs-lookup"><span data-stu-id="779c6-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="779c6-717">Sì</span><span class="sxs-lookup"><span data-stu-id="779c6-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="779c6-718">Attributi</span><span class="sxs-lookup"><span data-stu-id="779c6-718">Attributes</span></span>  
  
|<span data-ttu-id="779c6-719">Attributo</span><span class="sxs-lookup"><span data-stu-id="779c6-719">Attribute</span></span>|<span data-ttu-id="779c6-720">Descrizione</span><span class="sxs-lookup"><span data-stu-id="779c6-720">Description</span></span>|<span data-ttu-id="779c6-721">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="779c6-721">Required</span></span>|<span data-ttu-id="779c6-722">Default</span><span class="sxs-lookup"><span data-stu-id="779c6-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="779c6-723">for</span><span class="sxs-lookup"><span data-stu-id="779c6-723">for</span></span>|<span data-ttu-id="779c6-724">Determina se hello `wait` criteri attende che tutti i toobe criteri figlio immediati completata o solo una.</span><span class="sxs-lookup"><span data-stu-id="779c6-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="779c6-725">I valori consentiti sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="779c6-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="779c6-726">-   `all`-attendere tutti figlio immediati criteri toocomplete</span><span class="sxs-lookup"><span data-stu-id="779c6-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="779c6-727">-i - attendere qualsiasi toocomplete criterio figlio immediati.</span><span class="sxs-lookup"><span data-stu-id="779c6-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="779c6-728">Una volta completato il primo criterio di figlio immediati hello, hello `wait` criteri completa e viene terminata l'esecuzione di tutti gli altri criteri figlio immediati.</span><span class="sxs-lookup"><span data-stu-id="779c6-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="779c6-729">No</span><span class="sxs-lookup"><span data-stu-id="779c6-729">No</span></span>|<span data-ttu-id="779c6-730">tutti</span><span class="sxs-lookup"><span data-stu-id="779c6-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="779c6-731">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="779c6-731">Usage</span></span>  
 <span data-ttu-id="779c6-732">Questo criterio può essere utilizzato hello seguenti criteri [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="779c6-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="779c6-733">**Sezioni del criterio:** inbound, outbound, back-end</span><span class="sxs-lookup"><span data-stu-id="779c6-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="779c6-734">**Ambiti del criterio:** tutti gli ambiti</span><span class="sxs-lookup"><span data-stu-id="779c6-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="779c6-735">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="779c6-735">Next steps</span></span>
<span data-ttu-id="779c6-736">Per altre informazioni sull'uso di questi criteri, vedere:</span><span class="sxs-lookup"><span data-stu-id="779c6-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="779c6-737">Criteri in Gestione API</span><span class="sxs-lookup"><span data-stu-id="779c6-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="779c6-738">Espressioni di criteri</span><span class="sxs-lookup"><span data-stu-id="779c6-738">Policy expressions</span></span>](api-management-policy-expressions.md)
