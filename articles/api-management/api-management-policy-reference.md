---
title: aaaAzure API Gestione criteri di riferimento
description: Informazioni su hello criteri disponibili tooconfigure gestione API.
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
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="a3403-103">Informazioni di riferimento per i criteri di Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="a3403-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="a3403-104">In questa sezione viene fornito un indice per i criteri di hello in hello [riferimento ai criteri di gestione API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="a3403-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="a3403-105">Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="a3403-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="a3403-106">Espressioni di criteri possono essere utilizzate come valori di attributo o valori di testo in uno dei criteri di gestione API hello, salvo diversamente specificano criteri hello.</span><span class="sxs-lookup"><span data-stu-id="a3403-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="a3403-107">Alcuni criteri, ad esempio hello [flusso di controllo] [ Control flow] e [Imposta variabile] [ Set variable] criteri sono basati su espressioni di criteri.</span><span class="sxs-lookup"><span data-stu-id="a3403-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="a3403-108">Per altre informazioni, vedere [Criteri avanzati][Advanced policies] ed [Espressioni di criteri][Policy expressions]</span><span class="sxs-lookup"><span data-stu-id="a3403-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="a3403-109">Indice delle informazioni di riferimento per i criteri</span><span class="sxs-lookup"><span data-stu-id="a3403-109">Policy reference index</span></span>
* <span data-ttu-id="a3403-110">[Criteri per le restrizioni sull'accesso][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="a3403-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="a3403-111">[Controlla intestazione HTTP][Check HTTP header]: impone l'esistenza e/o il valore di un'intestazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="a3403-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="a3403-112">[Limita frequenza delle chiamate per sottoscrizione][Limit call rate by subscription]: impedisce picchi di utilizzo delle API limitando la frequenza delle chiamate per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a3403-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="a3403-113">[Limita frequenza delle chiamate per chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey): impedisce picchi di utilizzo delle API limitando la frequenza delle chiamata, per ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="a3403-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="a3403-114">[Limita IP chiamanti][Restrict caller IPs]: filtra (permette/rifiuta) le chiamate provenienti da indirizzi IP e/o intervalli di indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="a3403-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="a3403-115">[Quota di utilizzo di set da sottoscrizione] [ Set usage quota by subscription] -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in base a una per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a3403-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="a3403-116">[Quota di utilizzo di set da chiave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -consente tooenforce una quota rinnovabile o permanente chiamata volume e/o della larghezza di banda, in una base per ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="a3403-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="a3403-117">[Convalida JWT][Validate JWT]: impone l'esistenza e la validità di un token JWT estratto da un'intestazione HTTP specificata o da un parametro di query specificato.</span><span class="sxs-lookup"><span data-stu-id="a3403-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="a3403-118">[Criteri avanzati][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="a3403-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="a3403-119">[Flusso di controllo] [ Control flow] : in modo condizionale istruzioni dei criteri in base ai risultati di hello di valutazione di hello Boolean applica [espressioni][expressions].</span><span class="sxs-lookup"><span data-stu-id="a3403-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="a3403-120">[Inoltro della richiesta] [ Forward request] -inoltra servizio back-end di hello richiesta toohello.</span><span class="sxs-lookup"><span data-stu-id="a3403-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="a3403-121">[Log tooEvent Hub] [ Log tooEvent Hub] -invia messaggi hello destinazione del messaggio tooa specificato formato definito da un [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entità.</span><span class="sxs-lookup"><span data-stu-id="a3403-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="a3403-122">[Ripetere](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -esecuzione di tentativi di hello racchiuso tra istruzioni dei criteri, se e fino a quando non viene soddisfatta la condizione hello.</span><span class="sxs-lookup"><span data-stu-id="a3403-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="a3403-123">Esecuzione viene ripetuto in intervalli di tempo specificati hello e backup toohello specificato numero di tentativi.</span><span class="sxs-lookup"><span data-stu-id="a3403-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="a3403-124">[Restituire una risposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -hello di esecuzione e restituisce pipeline interruzioni specificato risposta direttamente toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="a3403-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="a3403-125">[Inviare una richiesta unidirezionale](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -invia una richiesta toohello URL specificato senza attendere una risposta.</span><span class="sxs-lookup"><span data-stu-id="a3403-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="a3403-126">[Invio richiesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -invia una richiesta toohello URL specificato.</span><span class="sxs-lookup"><span data-stu-id="a3403-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="a3403-127">[Impostare il metodo di richiesta](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -consente di determinare il metodo HTTP hello toochange per una richiesta.</span><span class="sxs-lookup"><span data-stu-id="a3403-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="a3403-128">[Impostare lo stato](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -toohello di codice stato HTTP hello modifiche valore specificato.</span><span class="sxs-lookup"><span data-stu-id="a3403-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="a3403-129">[Imposta variabile][Set variable]: rende persistente un valore in una variabile [context][context] denominata e consente di accedervi in un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="a3403-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="a3403-130">[Traccia](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -aggiunge una stringa hello [API controllo](api-management-howto-api-inspector.md) output.</span><span class="sxs-lookup"><span data-stu-id="a3403-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="a3403-131">[Attesa](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) : richiesta di attesa per la trasmissione tra parentesi, ottenere valore dalla cache o controllare toocomplete criteri flusso prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="a3403-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="a3403-132">[Criteri di autenticazione][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="a3403-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="a3403-133">[Autenticazione di base][Authenticate with Basic]: consente di eseguire l'autenticazione con un servizio di back-end tramite l'autenticazione di base.</span><span class="sxs-lookup"><span data-stu-id="a3403-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="a3403-134">[Autentica con certificato client][Authenticate with client certificate]: consente di eseguire l'autenticazione con un servizio back-end tramite certificati client.</span><span class="sxs-lookup"><span data-stu-id="a3403-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="a3403-135">[Criteri di memorizzazione nella cache][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="a3403-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="a3403-136">[Recupera dalla cache][Get from cache]: esegue una ricerca nella cache e restituisce una risposta valida memorizzata nella cache, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="a3403-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="a3403-137">[Archiviare toocache] [ Store toocache] -risposta cache in base toohello specificato configurazione del controllo della cache.</span><span class="sxs-lookup"><span data-stu-id="a3403-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="a3403-138">[Recupera valore dalla cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) : recupera un elemento memorizzato nella cache per chiave.</span><span class="sxs-lookup"><span data-stu-id="a3403-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="a3403-139">[Valore di memorizzare nella cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -archiviare un elemento nella cache di hello dalla chiave.</span><span class="sxs-lookup"><span data-stu-id="a3403-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="a3403-140">[Rimuovi valore dalla cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -rimuovere un elemento nella cache di hello dalla chiave.</span><span class="sxs-lookup"><span data-stu-id="a3403-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="a3403-141">[Criteri tra domini][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="a3403-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="a3403-142">[Consentire le chiamate tra domini] [ Allow cross-domain calls] -rende accessibile hello API da client Adobe Flash e Microsoft Silverlight basati su browser.</span><span class="sxs-lookup"><span data-stu-id="a3403-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="a3403-143">[CORS] [ CORS] -aggiunge la condivisione di risorse multiorigine (CORS) supporta l'operazione di tooan o chiama un'API tooallow tra domini da client basati su browser.</span><span class="sxs-lookup"><span data-stu-id="a3403-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="a3403-144">[JSONP] [ JSONP] - aggiunge JSON con riempimento (JSONP) supporto tooan operazione o chiama un'API tooallow tra domini da client JavaScript basati su browser.</span><span class="sxs-lookup"><span data-stu-id="a3403-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="a3403-145">[Criteri di trasformazione][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="a3403-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="a3403-146">[Convertire JSON tooXML] [ Convert JSON tooXML] - richiesta converte o corpo della risposta da JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="a3403-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="a3403-147">[Convertire XML tooJSON] [ Convert XML tooJSON] - richiesta converte o corpo della risposta da XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="a3403-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="a3403-148">[Trova e sostituisci stringa nel corpo][Find and replace string in body]: trova una sottostringa di richiesta o risposta e la sostituisce con una sottostringa diversa.</span><span class="sxs-lookup"><span data-stu-id="a3403-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="a3403-149">[Maschera URL nel contenuto] [ Mask URLs in content] -riscrive (maschera) i collegamenti nella risposta hello corpo in modo che facciano riferimento toohello collegamento equivalente tramite il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="a3403-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="a3403-150">[Impostare il servizio back-end] [ Set backend service] -Modifica servizio back-end hello per una richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="a3403-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="a3403-151">[Impostare corpo] [ Set body] -imposta corpo del messaggio hello per le richieste in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="a3403-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="a3403-152">[Intestazione HTTP set] [ Set HTTP header] - assegna una risposta di valore tooan esistente e/o l'intestazione della richiesta o aggiunge una nuova intestazione di risposta e/o di richiesta.</span><span class="sxs-lookup"><span data-stu-id="a3403-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="a3403-153">[Imposta parametro di stringa di query][Set query string parameter]: aggiunge, sostituisce il valore o elimina il parametro di stringa della query di richiesta.</span><span class="sxs-lookup"><span data-stu-id="a3403-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="a3403-154">[Riscrittura URL] [ Rewrite URL] -converte un URL di richiesta dal formato pubblico toohello formato previsto dal servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="a3403-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3403-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3403-155">Next steps</span></span>
<span data-ttu-id="a3403-156">Per ulteriori informazioni sulle espressioni di criteri, vedere hello video seguenti.</span><span class="sxs-lookup"><span data-stu-id="a3403-156">For more information on policy expressions, see hello following video.</span></span>

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
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
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


