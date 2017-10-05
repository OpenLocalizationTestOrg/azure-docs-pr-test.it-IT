---
title: Criteri di Gestione API di Azure | Documentazione Microsoft
description: Informazioni sui criteri disponibili per l'uso in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="67b27-103">Criteri in Gestione API</span><span class="sxs-lookup"><span data-stu-id="67b27-103">API Management policies</span></span>
<span data-ttu-id="67b27-104">Questa sezione fornisce un riferimento per i seguenti criteri di Gestione API.</span><span class="sxs-lookup"><span data-stu-id="67b27-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="67b27-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="67b27-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="67b27-106">I criteri di Gestione API sono una potente funzionalità del sistema che consente all'entità di pubblicazione di modificare il comportamento dell'API tramite la configurazione.</span><span class="sxs-lookup"><span data-stu-id="67b27-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="67b27-107">I criteri sono una raccolta di istruzioni che vengono eseguite in modo sequenziale in caso di richiesta o risposta di un'API.</span><span class="sxs-lookup"><span data-stu-id="67b27-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="67b27-108">Le istruzioni più comuni includono la conversione di formato da XML a JSON e la limitazione della frequenza delle chiamate per limitare la quantità di chiamate in ingresso da uno sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="67b27-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="67b27-109">Sono disponibili molti altri criteri predefiniti.</span><span class="sxs-lookup"><span data-stu-id="67b27-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="67b27-110">Le espressioni di criteri possono essere usate come valori di attributo o valori di testo in uno qualsiasi dei criteri di Gestione API, salvo diversamente specificato dai criteri.</span><span class="sxs-lookup"><span data-stu-id="67b27-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="67b27-111">Alcuni criteri, come [choose](api-management-advanced-policies.md#choose) e [set variable](api-management-advanced-policies.md#set-variable), sono basati su espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="67b27-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="67b27-112">Per altre informazioni, vedere [Criteri avanzati](api-management-advanced-policies.md#AdvancedPolicies) ed [Espressioni di criteri](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="67b27-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="67b27-113"><a name="ProxyPolicies"></a> Criteri</span><span class="sxs-lookup"><span data-stu-id="67b27-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="67b27-114">Criteri di limitazione dell'accesso</span><span class="sxs-lookup"><span data-stu-id="67b27-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="67b27-115">[check-header](api-management-access-restriction-policies.md#CheckHTTPHeader) : impone l'esistenza e/o il valore di un'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="67b27-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="67b27-116">[Limita frequenza delle chiamate per sottoscrizione](api-management-access-restriction-policies.md#LimitCallRate) : impedisce picchi di utilizzo delle API limitando la frequenza delle chiamate per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="67b27-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="67b27-117">[Limita frequenza delle chiamate per chiave](api-management-access-restriction-policies.md#LimitCallRateByKey) : impedisce picchi di utilizzo delle API limitando la frequenza delle chiamata, per ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="67b27-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="67b27-118">[ip-filter](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtra (permette/rifiuta) le chiamate provenienti da indirizzi IP e/o intervalli di indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="67b27-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="67b27-119">[Imposta quota di utilizzo per sottoscrizione](api-management-access-restriction-policies.md#SetUsageQuota) : consente di applicare una quota rinnovabile o permanente per il volume di chiamate e/o per la larghezza di banda, per sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="67b27-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="67b27-120">[Imposta quota di utilizzo per chiave](api-management-access-restriction-policies.md#SetUsageQuotaByKey) : consente di applicare una quota rinnovabile o permanente per il volume di chiamate e/o per la larghezza di banda, per chiave.</span><span class="sxs-lookup"><span data-stu-id="67b27-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="67b27-121">[validate-JWT](api-management-access-restriction-policies.md#ValidateJWT) : impone l'esistenza e la validità di un token JWT estratto da un'intestazione HTTP specificata o da un parametro di query specificato.</span><span class="sxs-lookup"><span data-stu-id="67b27-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="67b27-122">Criteri avanzati</span><span class="sxs-lookup"><span data-stu-id="67b27-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="67b27-123">[Flusso di controllo](api-management-advanced-policies.md#choose): applica in modo condizionale le istruzioni dei criteri in base ai risultati della valutazione di espressioni booleane.</span><span class="sxs-lookup"><span data-stu-id="67b27-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="67b27-124">[Inoltra richiesta](api-management-advanced-policies.md#ForwardRequest): inoltra la richiesta al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="67b27-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="67b27-125">[Registra in Hub eventi](api-management-advanced-policies.md#log-to-eventhub): invia messaggi nel formato specificato a una destinazione del messaggio definita da un'entità Logger.</span><span class="sxs-lookup"><span data-stu-id="67b27-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="67b27-126">[Riprova](api-management-advanced-policies.md#Retry): riprova l'esecuzione delle istruzioni dei criteri, se e fino a quando non viene soddisfatta la condizione.</span><span class="sxs-lookup"><span data-stu-id="67b27-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="67b27-127">L'esecuzione verrà ripetuta a specifici intervalli di tempo e per il numero di tentativi indicato.</span><span class="sxs-lookup"><span data-stu-id="67b27-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="67b27-128">[Restituisci risposta](api-management-advanced-policies.md#ReturnResponse) : l’esecuzione nella pipeline viene interrotta e viene restituita la risposta specificata direttamente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="67b27-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="67b27-129">[Invia richiesta unidirezionale](api-management-advanced-policies.md#SendOneWayRequest) : invia una richiesta all'URL specificato senza attendere una risposta.</span><span class="sxs-lookup"><span data-stu-id="67b27-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="67b27-130">[Invia richiesta](api-management-advanced-policies.md#SendRequest) : invia una richiesta all'URL specificato.</span><span class="sxs-lookup"><span data-stu-id="67b27-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="67b27-131">[Imposta variabile](api-management-advanced-policies.md#set-variable): rende persistente un valore in una variabile di contesto denominata e consente di accedervi in un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="67b27-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="67b27-132">[Imposta metodo di richiesta](api-management-advanced-policies.md#SetRequestMethod): consente di modificare il metodo HTTP per una richiesta.</span><span class="sxs-lookup"><span data-stu-id="67b27-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="67b27-133">[Imposta codice di stato](api-management-advanced-policies.md#SetStatus): modifica il codice di stato HTTP per il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="67b27-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="67b27-134">[Traccia](api-management-advanced-policies.md#Trace): aggiunge una stringa nell'output di [Controllo API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="67b27-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="67b27-135">[Attendi](api-management-advanced-policies.md#Wait): attende il completamento dei criteri inclusi per l'[invio della richiesta](api-management-advanced-policies.md#SendRequest), il [recupero del valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey) o il [flusso di controllo](api-management-advanced-policies.md#choose) prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="67b27-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="67b27-136">Criteri di autenticazione</span><span class="sxs-lookup"><span data-stu-id="67b27-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="67b27-137">[authentication-basic](api-management-authentication-policies.md#Basic) : consente di eseguire l'autenticazione con un servizio back-end tramite l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="67b27-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="67b27-138">[authentication-certificate](api-management-authentication-policies.md#ClientCertificate) : consente di eseguire l'autenticazione con un servizio back-end tramite certificati client.</span><span class="sxs-lookup"><span data-stu-id="67b27-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="67b27-139">Criteri di memorizzazione nella cache</span><span class="sxs-lookup"><span data-stu-id="67b27-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="67b27-140">[Recupera dalla cache](api-management-caching-policies.md#GetFromCache) : esegue una ricerca nella cache e restituisce una risposta valida memorizzata nella cache, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="67b27-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="67b27-141">[cache-lookup](api-management-caching-policies.md#StoreToCache) : memorizza nella cache la risposta in base alla configurazione del controllo cache specificata.</span><span class="sxs-lookup"><span data-stu-id="67b27-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="67b27-142">[Recupera valore dalla cache](api-management-caching-policies.md#GetFromCacheByKey) : recupera un elemento memorizzato nella cache per chiave.</span><span class="sxs-lookup"><span data-stu-id="67b27-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="67b27-143">[Archivia valore nella cache](api-management-caching-policies.md#StoreToCacheByKey) : archivia un elemento nella cache per chiave.</span><span class="sxs-lookup"><span data-stu-id="67b27-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="67b27-144">[Rimuovi valore dalla cache](api-management-caching-policies.md#RemoveCacheByKey) : rimuove un elemento dalla cache in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="67b27-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="67b27-145">Criteri tra domini</span><span class="sxs-lookup"><span data-stu-id="67b27-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="67b27-146">[Permetti chiamate tra i domini](api-management-cross-domain-policies.md#AllowCrossDomainCalls) : rende accessibile l'API da client Adobe Flash e Microsoft Silverlight basati su browser.</span><span class="sxs-lookup"><span data-stu-id="67b27-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="67b27-147">[CORS](api-management-cross-domain-policies.md#CORS) : aggiunge il supporto per CORS (Cross-Origin Resource Sharing) a un'operazione o a un'API per permettere le chiamate tra domini da client basati su browser.</span><span class="sxs-lookup"><span data-stu-id="67b27-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="67b27-148">[JSONP](api-management-cross-domain-policies.md#JSONP) : aggiunge il supporto per JSON con riempimento (JSONP) a un'operazione o a un'API per permettere le chiamate tra domini da client JavaScript basati su browser.</span><span class="sxs-lookup"><span data-stu-id="67b27-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="67b27-149">Criteri di trasformazione</span><span class="sxs-lookup"><span data-stu-id="67b27-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="67b27-150">[json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML) : converte il corpo della richiesta o della risposta da JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="67b27-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="67b27-151">[xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON) : converte il corpo della richiesta o della risposta da XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="67b27-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="67b27-152">[find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody) : trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.</span><span class="sxs-lookup"><span data-stu-id="67b27-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="67b27-153">[Maschera URL nel contenuto](api-management-transformation-policies.md#MaskURLSContent) : riscrive (maschera) i collegamenti nel corpo della risposta, in modo che facciano riferimento al collegamento equivalente tramite il gateway.</span><span class="sxs-lookup"><span data-stu-id="67b27-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="67b27-154">[set-backend-service](api-management-transformation-policies.md#SetBackendService) : consente di cambiare il servizio back-end per una richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="67b27-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="67b27-155">[set-body](api-management-transformation-policies.md#SetBody) : consente di impostare il corpo del messaggio per richieste in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="67b27-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="67b27-156">[Imposta intestazione HTTP](api-management-transformation-policies.md#SetHTTPheader) : assegna un valore a una intestazione di risposta e/o di richiesta esistente oppure aggiunge una nuova intestazione di risposta e/o di richiesta.</span><span class="sxs-lookup"><span data-stu-id="67b27-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="67b27-157">[Imposta parametro di stringa della query](api-management-transformation-policies.md#SetQueryStringParameter) : aggiunge, sostituisce il valore di o elimina il parametro di stringa della query di richiesta.</span><span class="sxs-lookup"><span data-stu-id="67b27-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="67b27-158">[rewrite-uri](api-management-transformation-policies.md#RewriteURL) : converte un URL di richiesta dal formato pubblico al formato previsto dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="67b27-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="67b27-159">[Trasforma XML usando una trasformazione XSLT](api-management-transformation-policies.md#XSLTransform): si applica una trasformazione da XSL a XML nel corpo della richiesta o della risposta.</span><span class="sxs-lookup"><span data-stu-id="67b27-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="67b27-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67b27-160">Next steps</span></span>
<span data-ttu-id="67b27-161">Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="67b27-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
