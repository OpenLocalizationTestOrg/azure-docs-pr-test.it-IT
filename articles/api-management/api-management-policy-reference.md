---
title: Informazioni di riferimento per i criteri di Gestione API di Azure
description: Informazioni sui criteri disponibili per configurare Gestione API.
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: adc0c4415e10ddd0b4994cecef17f026546e91a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="6ef85-103">Informazioni di riferimento per i criteri di Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="6ef85-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="6ef85-104">Questa sezione include un indice dei criteri disponibili in [Informazioni di riferimento per i criteri di Gestione API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="6ef85-104">This section provides an index for the policies in the [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="6ef85-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="6ef85-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="6ef85-106">Le espressioni di criteri possono essere usate come valori di attributo o valori di testo in uno qualsiasi dei criteri di Gestione API, salvo diversamente specificato dai criteri.</span><span class="sxs-lookup"><span data-stu-id="6ef85-106">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="6ef85-107">Alcuni criteri quali [Flusso di controllo][Control flow] e [Imposta variabile][Set variable] sono basati su espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="6ef85-107">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="6ef85-108">Per altre informazioni, vedere [Criteri avanzati][Advanced policies] ed [Espressioni di criteri][Policy expressions]</span><span class="sxs-lookup"><span data-stu-id="6ef85-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="6ef85-109">Indice delle informazioni di riferimento per i criteri</span><span class="sxs-lookup"><span data-stu-id="6ef85-109">Policy reference index</span></span>
* <span data-ttu-id="6ef85-110">[Criteri per le restrizioni sull'accesso][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="6ef85-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="6ef85-111">[Controlla intestazione HTTP][Check HTTP header]: impone l'esistenza e/o il valore di un'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ef85-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="6ef85-112">[Limita frequenza delle chiamate per sottoscrizione][Limit call rate by subscription]: impedisce picchi di utilizzo delle API limitando la frequenza delle chiamate per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6ef85-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="6ef85-113">[Limita frequenza delle chiamate per chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey): impedisce picchi di utilizzo delle API limitando la frequenza delle chiamata, per ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="6ef85-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="6ef85-114">[Limita IP chiamanti][Restrict caller IPs]: filtra (permette/rifiuta) le chiamate provenienti da indirizzi IP e/o intervalli di indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="6ef85-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="6ef85-115">[Imposta quota di utilizzo per sottoscrizione][Set usage quota by subscription]: consente di applicare una quota rinnovabile o permanente per il volume di chiamate e/o per la larghezza di banda, per sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6ef85-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="6ef85-116">[Imposta quota di utilizzo per chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey): consente di applicare una quota rinnovabile o permanente per il volume di chiamate e/o per la larghezza di banda, per chiave.</span><span class="sxs-lookup"><span data-stu-id="6ef85-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="6ef85-117">[Convalida JWT][Validate JWT]: impone l'esistenza e la validità di un token JWT estratto da un'intestazione HTTP specificata o da un parametro di query specificato.</span><span class="sxs-lookup"><span data-stu-id="6ef85-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="6ef85-118">[Criteri avanzati][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="6ef85-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="6ef85-119">[Flusso di controllo][Control flow]: applica in modo condizionale le istruzioni dei criteri in base ai risultati della valutazione di [espressioni][expressions] booleane.</span><span class="sxs-lookup"><span data-stu-id="6ef85-119">[Control flow][Control flow] - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="6ef85-120">[Inoltra richiesta][Forward request]: inoltra la richiesta al servizio back-end.</span><span class="sxs-lookup"><span data-stu-id="6ef85-120">[Forward request][Forward request] - Forwards the request to the backend service.</span></span>
  * <span data-ttu-id="6ef85-121">[Registra in Hub eventi][Log to Event Hub]: invia messaggi nel formato specificato a una destinazione del messaggio definita da un'entità [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger).</span><span class="sxs-lookup"><span data-stu-id="6ef85-121">[Log to Event Hub][Log to Event Hub] - Sends messages in the specified format to a message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="6ef85-122">[Riprova](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry): riprova l'esecuzione delle istruzioni dei criteri, se e fino a quando non viene soddisfatta la condizione.</span><span class="sxs-lookup"><span data-stu-id="6ef85-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="6ef85-123">L'esecuzione verrà ripetuta a specifici intervalli di tempo e per il numero di tentativi indicato.</span><span class="sxs-lookup"><span data-stu-id="6ef85-123">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>
  * <span data-ttu-id="6ef85-124">[Restituisci risposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) : l’esecuzione nella pipeline viene interrotta e viene restituita la risposta specificata direttamente al chiamante.</span><span class="sxs-lookup"><span data-stu-id="6ef85-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>
  * <span data-ttu-id="6ef85-125">[Invia richiesta unidirezionale](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) : invia una richiesta all'URL specificato senza attendere una risposta.</span><span class="sxs-lookup"><span data-stu-id="6ef85-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="6ef85-126">[Invia richiesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) : invia una richiesta all'URL specificato.</span><span class="sxs-lookup"><span data-stu-id="6ef85-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request to the specified URL.</span></span>
  * <span data-ttu-id="6ef85-127">[Imposta metodo di richiesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) : consente di modificare il metodo HTTP per una richiesta.</span><span class="sxs-lookup"><span data-stu-id="6ef85-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>
  * <span data-ttu-id="6ef85-128">[Imposta stato](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus): modifica il codice di stato HTTP per il valore specificato.</span><span class="sxs-lookup"><span data-stu-id="6ef85-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes the HTTP status code to the specified value.</span></span>
  * <span data-ttu-id="6ef85-129">[Imposta variabile][Set variable]: rende persistente un valore in una variabile [context][context] denominata e consente di accedervi in un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="6ef85-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="6ef85-130">[Traccia](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace): aggiunge una stringa nell'output di [Controllo API](api-management-howto-api-inspector.md).</span><span class="sxs-lookup"><span data-stu-id="6ef85-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into the [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="6ef85-131">[Attendi](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait): attende il completamento dei criteri inclusi per l'invio della richiesta, il recupero del valore dalla cache o il flusso di controllo prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="6ef85-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies to complete before proceeding.</span></span>
* <span data-ttu-id="6ef85-132">[Criteri di autenticazione][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="6ef85-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="6ef85-133">[Autenticazione di base][Authenticate with Basic]: consente di eseguire l'autenticazione con un servizio di back-end tramite l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="6ef85-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="6ef85-134">[Autentica con certificato client][Authenticate with client certificate]: consente di eseguire l'autenticazione con un servizio back-end tramite certificati client.</span><span class="sxs-lookup"><span data-stu-id="6ef85-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="6ef85-135">[Criteri di memorizzazione nella cache][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="6ef85-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="6ef85-136">[Recupera dalla cache][Get from cache]: esegue una ricerca nella cache e restituisce una risposta valida memorizzata nella cache, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="6ef85-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="6ef85-137">[Archivia nella cache][Store to cache]: memorizza nella cache la risposta in base alla configurazione del controllo cache specificata.</span><span class="sxs-lookup"><span data-stu-id="6ef85-137">[Store to cache][Store to cache] - Caches response according to the specified cache control configuration.</span></span>
  * <span data-ttu-id="6ef85-138">[Recupera valore dalla cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey): recupera un elemento memorizzato nella cache per chiave.</span><span class="sxs-lookup"><span data-stu-id="6ef85-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="6ef85-139">[Archivia valore nella cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) : archivia un elemento nella cache per chiave.</span><span class="sxs-lookup"><span data-stu-id="6ef85-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in the cache by key.</span></span>
  * <span data-ttu-id="6ef85-140">[Rimuovi valore dalla cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey): rimuove un elemento dalla cache in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="6ef85-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>
* <span data-ttu-id="6ef85-141">[Criteri tra domini][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="6ef85-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="6ef85-142">[Permetti chiamate tra domini][Allow cross-domain calls]: rende accessibile l'API da client basati su browser Adobe Flash e Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="6ef85-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="6ef85-143">[CORS][CORS]: aggiunge il supporto per CORS (Cross-Origin Resource Sharing) a un'operazione o a un'API per permettere le chiamate tra domini da client basati su browser.</span><span class="sxs-lookup"><span data-stu-id="6ef85-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="6ef85-144">[JSONP][JSONP]: aggiunge il supporto per JSON con riempimento (JSONP) a un'operazione o a un'API per permettere le chiamate tra domini da client JavaScript basati su browser.</span><span class="sxs-lookup"><span data-stu-id="6ef85-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="6ef85-145">[Criteri di trasformazione][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="6ef85-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="6ef85-146">[Converti JSON in XML][Convert JSON to XML]: converte il corpo della richiesta o della risposta da JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="6ef85-146">[Convert JSON to XML][Convert JSON to XML] - Converts request or response body from JSON to XML.</span></span>
  * <span data-ttu-id="6ef85-147">[Converti XML in JSON][Convert XML to JSON]: converte il corpo della richiesta o della risposta da XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="6ef85-147">[Convert XML to JSON][Convert XML to JSON] - Converts request or response body from XML to JSON.</span></span>
  * <span data-ttu-id="6ef85-148">[Trova e sostituisci stringa nel corpo][Find and replace string in body]: trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.</span><span class="sxs-lookup"><span data-stu-id="6ef85-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="6ef85-149">[Maschera URL nel contenuto][Mask URLs in content]: riscrive (maschera) i collegamenti nel corpo della risposta, in modo che facciano riferimento al collegamento equivalente tramite il gateway.</span><span class="sxs-lookup"><span data-stu-id="6ef85-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>
  * <span data-ttu-id="6ef85-150">[Imposta servizio back-end][Set backend service]: cambia il servizio back-end per una richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="6ef85-150">[Set backend service][Set backend service] - Changes the backend service for an incoming request.</span></span>
  * <span data-ttu-id="6ef85-151">[Imposta corpo][Set body]: consente di impostare il corpo del messaggio per le richieste in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="6ef85-151">[Set body][Set body] - Sets the message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="6ef85-152">[Imposta intestazione HTTP][Set HTTP header]: assegna un valore a una intestazione di risposta e/o di richiesta esistente oppure aggiunge una nuova intestazione di risposta e/o di richiesta.</span><span class="sxs-lookup"><span data-stu-id="6ef85-152">[Set HTTP header][Set HTTP header] - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="6ef85-153">[Imposta parametro di stringa di query][Set query string parameter]: aggiunge, sostituisce il valore o elimina il parametro di stringa della query di richiesta.</span><span class="sxs-lookup"><span data-stu-id="6ef85-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="6ef85-154">[Riscrivi URL][Rewrite URL]: converte un URL di richiesta dal formato pubblico al formato previsto dal servizio Web.</span><span class="sxs-lookup"><span data-stu-id="6ef85-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form to the form expected by the web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ef85-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6ef85-155">Next steps</span></span>
<span data-ttu-id="6ef85-156">Per altre informazioni sulle espressioni di criteri, vedere il video seguente.</span><span class="sxs-lookup"><span data-stu-id="6ef85-156">For more information on policy expressions, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log to Event Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store to cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON to XML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML to JSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


